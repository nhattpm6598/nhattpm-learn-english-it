# Tuần 34 — System design (2): Chat system, News feed, Notification service

> Checklist gốc: [phase-4-interview.md](../../phase-4-interview.md#tuần-34--system-design-2) · Khung 5 bước: xem [week-33.md](week-33.md#2-khung-5-bước-45-phút)

## 1. Mục tiêu tuần này

- Trình bày 3 bài kinh điển: **chat system**, **news feed**, **notification service**.
- Dùng tự nhiên từ vựng về **real-time, fan-out, queue, idempotency, delivery guarantees**.
- **Phỏng vấn thử #6** (system design).

> Nhắc lại khung: **Requirements → Estimation → High-level → Deep dive → Trade-offs**. Tuần này, mỗi bài có phần "deep dive" khác nhau — đó là chỗ phân biệt bạn với người chỉ học thuộc diagram.

## 2. Walkthrough 1: Design a chat system (như WhatsApp / Messenger)

### Requirements

> "Let me clarify the scope. Is it **one-to-one** chat only, or also **group chat**? … Both, with groups up to, say, 200 members. Do we need online/offline presence? … Yes. Read receipts? … Nice-to-have. Media like images? … Let's focus on text and mention media briefly. Message history should be stored permanently and synced across a user's devices.
>
> **Non-functional:** low latency — messages should arrive in under about 500 milliseconds when both users are online. Messages must **never be lost**, and within a conversation they must be shown **in order**. High availability."

### Estimation

> "Let's say **50 million daily active users**, each sending about **40 messages a day**. That's 2 billion messages per day, so about **23,000 messages per second** on average — call it 50,000 at peak. If a message is about 200 bytes with metadata, that's 400 GB per day, about **150 TB per year**. So storage must scale horizontally. And we'd have tens of millions of **concurrent connections**."

### High-level design

> "For real-time delivery, plain HTTP request-response isn't enough, because the server needs to push messages to the client. The options are **long polling**, **Server-Sent Events**, and **WebSockets**. For chat, I'd use **WebSockets** because communication is bidirectional and frequent, and it avoids the overhead of opening new connections.
>
> **Components:**
> - **Chat servers** (WebSocket servers): keep persistent connections with online clients. These are **stateful**, because each one holds connections.
> - A **session / presence service**, backed by Redis, which stores which chat server each online user is connected to, plus heartbeats for presence.
> - A **message service** that assigns message IDs and writes messages to the **message store**.
> - A **message queue / pub-sub** between chat servers, so a message received on server A can reach a user connected to server B.
> - A **push notification service** for offline users (APNs for iOS, FCM for Android).
> - Normal stateless **API services** behind a load balancer for login, profiles, group management, and fetching history.
>
> **Flow for a one-to-one message:** User A sends a message over the WebSocket to chat server 1. The server persists it via the message service — and only after it's stored, it sends an **ACK** back to A, so A knows the message is safe. Then it looks up where B is connected. If B is online on chat server 2, the message is routed there and pushed to B. If B is offline, we send a push notification, and when B comes back online, the client syncs all messages after its last received message ID."

### Deep dive: storage & ordering

> "**Storage:** the access pattern is mostly writes, and reads of the latest messages in a conversation. There are no complex joins. So I'd use a wide-column store like **Cassandra** or **HBase** — they scale writes horizontally. The partition key is `conversation_id`, and the clustering key is `message_id`, sorted descending, so 'get the latest 50 messages' is a single efficient query. Facebook Messenger used HBase, and Discord has written about storing messages in Cassandra and later ScyllaDB.
>
> **Ordering:** timestamps from different servers aren't reliable because of clock skew. Instead, we need message IDs that are **sortable within a conversation**. One option is a **Snowflake-style ID** — timestamp plus machine ID plus sequence — which is roughly time-ordered globally. To guarantee strict order within a conversation, we can use a **per-conversation sequence number**, for example from a counter in Redis, or by routing all messages of one conversation through the same partition of Kafka.
>
> **Delivery guarantees:** we aim for **at-least-once** delivery with retries, and the client **de-duplicates** using a client-generated message ID. So the end user effectively sees each message exactly once."

### Deep dive: group chat

> "For small groups up to 200 members, when a message arrives, the server **fans out** to every member: look up each member's connection and push. For very large groups or channels, fan-out on write gets expensive, so clients would instead **pull** new messages for those channels. That's similar to the news feed trade-off."

### Trade-offs & wrap-up

> "Main trade-offs:
> - WebSocket servers are **stateful**, which makes scaling and deployments harder: when a server restarts, clients must reconnect — with exponential backoff and jitter to avoid a thundering herd — and resync from their last message ID.
> - **Presence** at this scale is expensive. We can update presence with heartbeats every 30 seconds and only send presence updates to friends who are actually viewing the chat list, not to everyone.
> - **End-to-end encryption** changes the design a lot, since the server can't read messages — I'd mention it but treat it as out of scope.
>
> To summarize: WebSockets for real-time, a presence service to route messages, Cassandra partitioned by conversation for storage, per-conversation ordering, and at-least-once delivery with client-side de-duplication."

## 3. Walkthrough 2: Design a news feed (như Facebook / LinkedIn / Twitter)

### Requirements

> "Let me confirm the scope: users can create posts, follow other users, and see a **feed** of posts from people they follow. Is the feed **chronological** or **ranked**? … Let's start with reverse chronological and discuss ranking later. Do posts include images and videos? … Yes, but media is stored separately.
>
> **Non-functional:** feed loading should be fast — under about 200 milliseconds. It's very **read-heavy**. It's okay if a new post appears in followers' feeds after a few seconds — so **eventual consistency** is fine."

### Estimation

> "Say **200 million DAU**. Each user opens the feed about 10 times a day — that's 2 billion feed reads per day, about **23,000 reads per second**, maybe 50,000 at peak. Each user posts about once every few days, so maybe 50 million new posts per day, around **600 writes per second**. On average, a user follows about 200 people, but some celebrities have **tens of millions of followers** — that's going to matter."

### High-level design

> "**APIs:** `POST /v1/posts` and `GET /v1/feed?cursor=...&limit=20` — with cursor-based pagination.
>
> **Components:** post service with a post database; a social graph service — who follows whom; a **feed service** that builds and serves feeds; a **feed cache** in Redis; object storage plus a CDN for media.
>
> The core question is **when** we build the feed. There are two approaches:
>
> **Fan-out on write — the push model:** when a user posts, we immediately insert the post ID into the cached feed of every follower. Reading the feed is then very fast — just read a precomputed list from Redis. The downside is the **celebrity problem**: one post from someone with 50 million followers means 50 million writes. Also, we waste work for inactive users.
>
> **Fan-out on read — the pull model:** when a user opens the feed, we fetch recent posts from everyone they follow and merge them. Writes are cheap, but reads are slow and expensive, and reads are much more frequent.
>
> I'd use a **hybrid**: fan-out on write for normal users, and for celebrities — say, accounts with more than a million followers — we don't fan out. When a user loads their feed, we take the precomputed feed and merge in recent posts from the few celebrities they follow at read time. We can also skip fan-out for users who haven't been active for a month and build their feed on demand when they come back."

### Deep dive: fan-out pipeline & feed storage

> "When a post is created, the post service stores it and publishes a `PostCreated` event to **Kafka**. **Fan-out workers** consume the event, get the follower list from the graph service in batches, and push the post ID into each follower's feed list in Redis — for example, a Redis list or sorted set keyed by `feed:{userId}`, scored by timestamp, trimmed to the latest 500 or so entries.
>
> We only store **post IDs** in the feed, not the full post, to save memory. When serving the feed, we get 20 IDs, then **hydrate** them — batch-fetch the post content, author info, and like counts from their own caches. This way, if a post is edited, we don't need to update millions of feeds.
>
> Kafka also gives us **back-pressure**: if there's a spike, the queue grows and workers catch up, without affecting the post API."

### Trade-offs & wrap-up

> "- **Consistency:** followers see a new post after a short delay — acceptable here.
> - **Ranking:** to move from chronological to ranked, a ranking service scores candidate posts using features like engagement and the relationship with the author. That's a whole topic on its own.
> - **Deletes and privacy:** if a post is deleted, we filter it out at hydration time instead of removing it from every feed.
> - **Cache failure:** if Redis loses a feed, we can rebuild it with fan-out on read as a fallback.
>
> So the key decision is push versus pull, and the hybrid approach balances write cost for celebrities and read latency for everyone else."

## 4. Walkthrough 3: Design a notification service

### Requirements

> "Let me clarify: which channels do we support — **push** on iOS and Android, **SMS**, **email**, and **in-app**? … All of them. Who sends notifications — other internal services, like orders and payments? … Yes. Do we need user preferences, like opting out of marketing emails? … Yes. Scheduling? … Nice-to-have.
>
> **Non-functional:** reliable — we shouldn't lose important notifications like OTP codes or payment confirmations; **no duplicates** where possible — nobody wants five identical SMS; scalable to spikes, like a marketing campaign to all users; and the **sender services shouldn't be blocked** by slow providers. OTPs need low latency, but marketing messages can wait."

### Estimation

> "Let's say 10 million push notifications, 1 million SMS, and 5 million emails per day — about 200 per second on average, but campaigns can create spikes of maybe 50,000 per second for a short time. That's why we need queues."

### High-level design

> "1. Internal services call the **Notification API** — or publish an event — with `{ userId, type, templateId, params, idempotencyKey, priority }`.
> 2. The notification service **validates** the request, checks the **user's preferences** and opt-outs, loads **contact info** — device tokens, phone, email — and renders the **template**, with localization.
> 3. It saves a notification record with status `PENDING`, then puts a message into a **queue per channel** — for example, separate Kafka topics or SQS queues for push, SMS, and email. Separate queues mean a slow email provider doesn't delay push notifications.
> 4. **Channel workers** consume from their queue and call the third-party providers: **APNs** and **FCM** for push, an SMS gateway like Twilio, and an email provider like SES or SendGrid.
> 5. Workers update the status — `SENT`, `FAILED`, or `DELIVERED` when providers send callbacks — for tracking and analytics.
>
> I'd also separate **priority**: OTPs and transactional messages go to a high-priority queue with dedicated workers, so a marketing campaign of 10 million emails can't delay an OTP."

### Deep dive: reliability, retries, de-duplication

> "**Retries:** third-party providers fail sometimes. Workers retry with **exponential backoff and jitter**, and after N attempts, the message goes to a **dead-letter queue** for investigation. For important messages, we could fall back to another channel or provider — for example, SMS provider B if provider A is down.
>
> **De-duplication:** queues usually give **at-least-once** delivery, so a worker might process the same message twice. Each request has an **idempotency key**. Before sending, the worker checks whether that key was already sent — for example with a Redis `SET key NX` with a TTL, or a unique constraint in the database. It's not perfect — if the worker crashes right after the provider call but before recording it, we might still send twice — but it reduces duplicates to a very small number. Exactly-once sending to an external provider isn't really possible.
>
> **Rate limiting:** we respect provider limits, and limit per user too — for example, max three marketing pushes per day — so we don't annoy users.
>
> **Not losing events from senders:** if the order service must send a notification after an order is created, it should use the **transactional outbox pattern**, so the event is published only if the order transaction committed."

### Trade-offs & wrap-up

> "- Kafka versus a simpler queue like SQS or RabbitMQ: Kafka is great for throughput and replay, but per-message retries and delays are easier with SQS or RabbitMQ. If the company already runs Kafka, I'd use it with retry topics.
> - **Monitoring:** sent and failure rates per channel and provider, queue lag, and end-to-end latency for OTPs, with alerts.
> - **Security & privacy:** don't log phone numbers or message content with sensitive data; respect unsubscribe rules.
>
> To summarize: an API that validates, checks preferences, and renders templates; per-channel and per-priority queues; workers with retries, DLQ, and idempotency; and provider abstraction for failover."

## 5. Cụm từ hữu ích (35)

| # | English | Nghĩa |
| --- | --- | --- |
| 1 | real-time / near real-time | Thời gian thực / gần thực |
| 2 | persistent connection | Kết nối giữ lâu dài |
| 3 | bidirectional communication | Giao tiếp hai chiều |
| 4 | The server pushes ... to the client. | Server đẩy |
| 5 | The client polls every N seconds. | Client hỏi định kỳ |
| 6 | These servers are stateful, so ... | Có trạng thái |
| 7 | We route the message to the server where the user is connected. | Định tuyến |
| 8 | If the user is offline, we fall back to a push notification. | Dự phòng |
| 9 | The client acknowledges (ACKs) the message. | Xác nhận |
| 10 | at-least-once / at-most-once / exactly-once delivery | Đảm bảo giao |
| 11 | The client de-duplicates using the message ID. | Khử trùng lặp |
| 12 | clock skew | Lệch đồng hồ |
| 13 | partition key / clustering key | Khoá phân vùng |
| 14 | It's a write-heavy / read-heavy workload. | Tải nặng ghi / đọc |
| 15 | fan-out on write (push) vs. fan-out on read (pull) | Hai mô hình feed |
| 16 | the celebrity problem / hot key | Vấn đề tài khoản nhiều follower |
| 17 | a hybrid approach | Phương án lai |
| 18 | We precompute the feed. | Tính trước |
| 19 | We hydrate the post IDs with the full content. | Bổ sung dữ liệu |
| 20 | cursor-based pagination | Phân trang theo con trỏ |
| 21 | eventual consistency is acceptable here | Nhất quán cuối cùng chấp nhận được |
| 22 | back-pressure / the queue absorbs spikes | Hàng đợi hấp thụ đột biến |
| 23 | We decouple the sender from the provider. | Tách rời |
| 24 | a queue per channel / per priority | Hàng đợi theo kênh/ưu tiên |
| 25 | retry with exponential backoff and jitter | Thử lại giãn cách |
| 26 | dead-letter queue (DLQ) | Hàng đợi thư chết |
| 27 | idempotency key | Khoá idempotent |
| 28 | transactional outbox pattern | Mẫu outbox |
| 29 | failover to a secondary provider | Chuyển sang nhà cung cấp phụ |
| 30 | thundering herd | Đám đông đồng loạt kết nối lại |
| 31 | heartbeat | Tín hiệu sống |
| 32 | This doesn't scale for ... | Không mở rộng được cho |
| 33 | We can treat ... as out of scope. | Ngoài phạm vi |
| 34 | That's a whole topic on its own. | Đó là cả một chủ đề riêng |
| 35 | I'd monitor queue lag and failure rates. | Theo dõi độ trễ hàng đợi |

## 6. Lỗi người Việt hay mắc

1. **Nói "realtime" cho mọi thứ** mà không định nghĩa: hỏi "How real-time? Under one second? Five seconds?"
2. **Chỉ vẽ "happy path"**: không nói gì khi user offline, server restart, provider lỗi.
3. **Nói "exactly-once" quá dễ dàng.** Interviewer Senior sẽ hỏi lại. Nói đúng: "at-least-once + idempotency".
4. **Không giải thích vì sao chọn Cassandra/Kafka**, chỉ vì "big companies use it".
5. **Đọc từ:** *WebSocket* /ˈwebsɒkɪt/, *fan-out* /ˈfæn aʊt/, *idempotent* /ˌaɪdemˈpəʊtənt/ hoặc /ˌɪdəmˈpoʊtənt/, *asynchronous* /eɪˈsɪŋkrənəs/, *notification* /ˌnəʊtɪfɪˈkeɪʃn/, *presence* /ˈprezns/, *pagination* /ˌpædʒɪˈneɪʃn/, *Cassandra* /kəˈsændrə/.
6. **Lẫn "push notification" và "push model"** — nói rõ "the push model for the feed" vs. "mobile push notifications".

## 7. Lịch luyện trong tuần

| Ngày | Việc |
| --- | --- |
| T2 | **Chat system** — trình bày 35', vẽ diagram, ghi âm. |
| T3 | **News feed** — tập trung giải thích push vs pull vs hybrid trong 3 phút không vấp. |
| T4 | **Notification service** — tập trung phần retry/idempotency. |
| T5 | **Phỏng vấn thử #6** (prompt mục 8). |
| T6 | Xem lại, so sánh với tuần 33: bạn đã hỏi requirement tốt hơn chưa? Trade-off rõ hơn chưa? |
| T7 | Ôn + nhật ký. |

## 8. Prompt cho AI voice — Mock interview #6

```
You are a principal engineer running a 45-minute system design interview.
I'm a Senior Java backend candidate with B1 English.

Pick ONE question randomly: "Design a chat system like WhatsApp",
"Design a news feed like Facebook", or "Design a notification service
for an e-commerce platform".

Rules:
- Give only the one-sentence question at first. Answer my clarifying
  questions with realistic numbers.
- Let me drive. Interrupt only when a real interviewer would, e.g. to ask
  "Why did you choose this database?" or "What happens when this fails?"
- Do a deep dive on the hardest part (ordering & delivery for chat,
  celebrity fan-out for feed, retries & duplicates for notifications).
- At minute 40, ask me to summarize my design and main trade-offs.

Feedback:
- Structure (requirements, estimation, high-level, deep dive, trade-offs): 1-5 each.
- Technical mistakes or missing points.
- Better English phrases for 5 things I said.
- Would you pass me at Senior level? Why?
```

## 9. Checklist tự đánh giá

- [ ] Hỏi requirement cụ thể (group size, channels, chronological vs ranked)
- [ ] Ước lượng có QPS + storage + đặc điểm đặc biệt (concurrent connections, celebrities, spikes)
- [ ] Giải thích **vì sao** chọn WebSocket / Cassandra / Kafka
- [ ] Nói về trường hợp lỗi: offline, server restart, provider down
- [ ] Nói đúng về delivery guarantees (at-least-once + idempotency)
- [ ] Có ít nhất 1 phương án lai (hybrid) và giải thích trade-off
- [ ] Có tóm tắt cuối
- [ ] Phát âm đúng: WebSocket, idempotent, asynchronous, notification

## 10. Tài liệu tham khảo

- System Design Primer: https://github.com/donnemartin/system-design-primer
- ByteByteGo (có các bài chat, news feed, notification): https://bytebytego.com · https://www.youtube.com/@ByteByteGo
- Tech Interview Handbook: https://www.techinterviewhandbook.org
