# Tuần 28 — Trình bày dự án nổi bật

> Checklist gốc: [phase-4-interview.md](../../phase-4-interview.md#tuần-28--dự-án-nổi-bật) · Viết dự án của bạn vào [interview/answers.md](../../interview/answers.md#dự-án-nổi-bật)

## 1. Mục tiêu tuần này

- Chọn **3 dự án** và trình bày mỗi dự án trong **2–3 phút**.
- Trả lời được các câu hỏi **đào sâu** (deep-dive): "Why did you choose Kafka?", "What would you do differently?", "How did you measure that?"
- Biết vẽ/mô tả kiến trúc bằng lời: "On the left we have..., the request goes to..."

> Các câu hỏi kích hoạt phần này: *"Tell me about a project you're proud of."*, *"Walk me through a recent project."*, *"What's the most technically challenging thing you've worked on?"*, *"Describe the architecture of your current system."*

## 2. Khung trình bày: Context → Problem → Role → Solution → Result → Reflection

| Bước | Câu hỏi cần trả lời | Ví dụ câu mở |
| --- | --- | --- |
| **1. Context** | Sản phẩm là gì? Ai dùng? Quy mô? | "This was at my current company. We have a payment platform used by about..." |
| **2. Problem** | Vấn đề kinh doanh/kỹ thuật là gì? Vì sao quan trọng? | "The problem was that..." / "Users were complaining that..." |
| **3. My role** | **Bạn** làm gì cụ thể? (không phải team) | "I was the lead developer on this. I was responsible for..." |
| **4. Solution** | Kiến trúc, công nghệ, **vì sao** chọn | "We decided to... because... We also considered X, but..." |
| **5. Result** | Số liệu: latency, cost, users, bugs, time | "As a result, ... dropped from X to Y." |
| **6. Reflection** | Bài học, nếu làm lại sẽ làm gì khác | "Looking back, I would have... earlier." |

**Tỉ lệ thời gian (bản 2,5'):** Context+Problem 30s · Role 15s · Solution 60–75s · Result 20s · Reflection 15s.

**Lưu ý:** Phần **Solution** phải có **trade-off** ("We considered X, but chose Y because..."). Đây là điểm phân biệt Senior với Junior.

## 3. Template trống (copy vào answers.md)

```
Project name:
Context (product, users, scale):
Problem (why it mattered, numbers):
My role (team size, what I owned):
Solution (architecture, tech, why):
  - Alternative considered + why not:
Challenges during implementation:
Result (numbers!):
What I learned / what I'd do differently:
Possible follow-up questions + short answers:
  1.
  2.
  3.
```

**Nếu không nhớ số liệu chính xác:** dùng ước lượng trung thực: "roughly", "around", "about", "more than". Ví dụ: "around 30 percent", "from several seconds to under one second". Đừng bịa số cụ thể đến từng đơn vị.

## 4. Model answers

### 4.1. Dự án 1 — Tối ưu hiệu năng (Transaction History Service)

> "Let me tell you about the transaction history service at my current company.
>
> **Context:** We run a payment platform with around one million active users. One of the most-used screens in the mobile app is the transaction history, where users can see and search their past payments.
>
> **Problem:** As our data grew to more than 300 million rows, this screen became really slow. The p95 latency was about 800 milliseconds, sometimes several seconds during peak hours, and it was also putting a lot of load on our main PostgreSQL database — which affected the payment flow itself. That was the real risk.
>
> **My role:** I was the lead developer. I did the analysis, proposed the design, and worked with two other backend developers to implement it over about two months.
>
> **Solution:** First, I analyzed the slow queries using `EXPLAIN ANALYZE`, and found two problems: a missing composite index on user ID and created date, and offset-based pagination, which gets slower for older pages. So in phase one, we added the index and switched to keyset — or cursor-based — pagination. That alone gave us a big improvement.
>
> In phase two, we moved all read traffic for this screen to a read replica, so it no longer competed with payment writes. And we added a Redis cache for the first page of each user's history, because about 80 percent of requests only looked at the most recent transactions. We invalidate the cache when a new transaction event comes in from Kafka.
>
> We did consider Elasticsearch for the search feature, but it would add a new system to operate, and our search needs were simple, so we decided it wasn't worth the complexity at that point.
>
> **Result:** The p95 latency went from about 800 milliseconds to under 150, CPU on the primary database dropped by around 35 percent, and support tickets about slowness went down by about 70 percent.
>
> **Reflection:** Looking back, I'd add proper query monitoring much earlier. We only noticed the problem when users complained. Now we have slow-query alerts, so we catch these issues before they hit users."

**Câu hỏi đào sâu có thể gặp + trả lời ngắn:**

- *"How do you handle replication lag on the read replica?"* → "Good question. Replication lag was usually under 100 milliseconds. For the screen right after a payment, we read from the primary for a few seconds — a 'read-your-writes' approach — so the user always sees their new transaction."
- *"Why keyset pagination?"* → "With OFFSET, the database still has to scan and skip all the previous rows, so page 1000 is very slow. With keyset pagination we use `WHERE created_at < :lastSeen ORDER BY created_at DESC LIMIT 20`, which uses the index directly, so every page is equally fast."
- *"What about cache consistency?"* → "We used cache-aside with a short TTL of five minutes as a safety net, plus event-based invalidation. In the worst case, a user might see slightly stale data for a few seconds, which was acceptable for this screen — but not for the balance, which we never cache."

### 4.2. Dự án 2 — Tách monolith sang microservices (Notification Service)

> "Another project I'd like to mention is extracting our notification module from the monolith into a separate service.
>
> **Context:** We had a Spring Boot monolith that did everything — orders, payments, and notifications like email, SMS, and push.
>
> **Problem:** Notifications were sent synchronously inside the order transaction. So when the SMS provider was slow or down, the whole checkout became slow — and a few times, orders actually failed because of a timeout in the SMS call. That's obviously a bad user experience.
>
> **My role:** I designed the new service and wrote most of the code. I also wrote the migration plan and presented it to the team and our engineering manager.
>
> **Solution:** We made notifications asynchronous. The order service now publishes an `OrderCreated` event to Kafka after the transaction commits — we used the transactional outbox pattern so we never lose events or send events for rolled-back orders. The new notification service consumes the events, renders templates, and calls the providers. For failures, we have retries with exponential backoff and a dead-letter topic. We also made the consumer idempotent by storing the event ID, because Kafka gives at-least-once delivery.
>
> We considered using RabbitMQ, but the company already ran Kafka for other things, so we chose it to avoid operating another broker.
>
> **Result:** Checkout p99 latency dropped by about 40 percent, and we had zero order failures caused by notification providers after the release. It also let the team deploy notification changes independently, several times a week.
>
> **Reflection:** If I did it again, I'd invest more in observability from day one — distributed tracing across the Kafka hop took us a while to set up, and debugging was hard without it."

### 4.3. Dự án 3 — Fullstack / UI (Admin Dashboard)

> "The third one is more on the frontend side. I built an internal admin dashboard for our customer support team.
>
> **Context and problem:** Support agents had to use three different tools and sometimes even run SQL queries through developers to answer customer questions. It took them on average about eight minutes per ticket.
>
> **My role:** I was the only engineer on it for the first version, so I owned it end-to-end: talking with the support team, working with our designer on the UX, building the backend APIs in Spring Boot, and the frontend in React with TypeScript.
>
> **Solution:** I started by sitting with two support agents for half a day to watch how they worked. That helped a lot — I found out that 80 percent of their searches were by phone number or transaction ID, so we made one global search box the center of the UI. On the backend, I built a BFF — a backend-for-frontend — that aggregates data from four services, with role-based access control so agents only see what they need. Sensitive fields like card numbers are masked.
>
> **Result:** Average handling time went from about eight minutes to under three, and developers stopped getting SQL requests from support, which saved us several hours a week.
>
> **Reflection:** I learned how much value you get from talking directly to users before writing code."

## 5. Mô tả kiến trúc bằng lời (khi không có bảng vẽ)

> "Let me describe the architecture from left to right. **On the client side**, we have a mobile app and a web app. **All requests go through** an API gateway, which **handles** authentication and rate limiting. **Behind the gateway**, there are about fifteen Spring Boot services. **They communicate** synchronously over REST for queries, and asynchronously through Kafka for events. **Each service owns its own database** — mostly PostgreSQL, plus Redis for caching. **Everything runs on** Kubernetes on AWS, and we use Prometheus and Grafana for monitoring."

## 6. Cụm từ hữu ích (35)

| # | English | Nghĩa |
| --- | --- | --- |
| 1 | Let me tell you about... / I'd like to talk about... | Mở đầu |
| 2 | To give you some context, ... | Để bạn nắm bối cảnh |
| 3 | The main problem was that... | Vấn đề chính |
| 4 | This was a big deal because... | Điều này quan trọng vì |
| 5 | It was affecting... / It had an impact on... | Ảnh hưởng tới |
| 6 | I was responsible for... | Tôi chịu trách nhiệm |
| 7 | I owned the ... end-to-end. | Tôi phụ trách trọn vẹn |
| 8 | I worked closely with... | Làm việc chặt chẽ với |
| 9 | I took the lead on... | Tôi dẫn dắt phần |
| 10 | First, I analyzed / investigated... | Bước đầu tiên |
| 11 | It turned out that... | Hoá ra là |
| 12 | The root cause was... | Nguyên nhân gốc |
| 13 | We decided to go with X because... | Chúng tôi chọn X vì |
| 14 | We also considered Y, but... | Cũng cân nhắc Y nhưng |
| 15 | It wasn't worth the extra complexity. | Không đáng phức tạp thêm |
| 16 | The trade-off was... | Đánh đổi là |
| 17 | We rolled it out gradually / behind a feature flag. | Triển khai từ từ |
| 18 | One of the biggest challenges was... | Thử thách lớn nhất |
| 19 | To solve that, we... | Để giải quyết |
| 20 | As a result, ... | Kết quả là |
| 21 | ...went down / dropped from X to Y | Giảm từ X xuống Y |
| 22 | ...went up / increased by 30 percent | Tăng 30% |
| 23 | p95 latency / throughput / error rate | Chỉ số kỹ thuật |
| 24 | We measured it using... (Grafana, logs, APM) | Đo bằng |
| 25 | Looking back, I would have... | Nhìn lại, lẽ ra tôi đã |
| 26 | If I did it again, I'd... | Nếu làm lại |
| 27 | The biggest lesson for me was... | Bài học lớn nhất |
| 28 | Let me describe the architecture from left to right. | Mô tả kiến trúc |
| 29 | The request first goes to..., then... | Luồng request |
| 30 | Service A talks to service B via... | Giao tiếp giữa service |
| 31 | Each service owns its own database. | Mỗi service có DB riêng |
| 32 | Roughly / around / about... | Ước lượng |
| 33 | in production / in peak hours | Trên production / giờ cao điểm |
| 34 | Does that answer your question? / Should I go deeper into any part? | Kiểm tra với interviewer |
| 35 | I'm happy to go into more detail on... | Sẵn sàng nói sâu hơn |

## 7. Lỗi người Việt hay mắc

1. **Nói "we" cho mọi thứ** → interviewer không biết bạn làm gì. Dùng "**I** designed", "**I** proposed", "my teammate handled the frontend, and **I** focused on...".
2. **Kể công nghệ thay vì vấn đề:** "We used Spring Boot, Kafka, Redis, Docker, K8s..." — danh sách công nghệ không nói lên gì. Hãy nói **vì sao**.
3. **Không có kết quả đo được.** "It became faster" → "p95 dropped from 800ms to 150ms".
4. **Quá nhiều chi tiết nghiệp vụ** (tên màn hình, quy trình nội bộ) — người ngoài không hiểu. Đơn giản hoá: "It's basically like a bank statement screen."
5. **Không nói trade-off** → nghe như Junior.
6. **Dịch từ tiếng Việt:** "We have many problem about performance" → "We had **serious performance problems**." / "The system was very lag" → "The system was **very slow** / **laggy**" (lag là danh từ/động từ: "there was a lag").
7. **Thì quá khứ:** dự án đã xong → **past simple**: "I built", "we decided", "it reduced". Lỗi phổ biến: "I build" (hiện tại).
8. **Đọc sai từ kỹ thuật:** *cache* /kæʃ/ (như "cash", KHÔNG phải "cát-chê"), *queue* /kjuː/, *Kubernetes* /ˌkuːbərˈnetiːz/, *PostgreSQL* /ˈpəʊstɡres kjuː el/, *Redis* /ˈredɪs/, *SQL* /ˌes kjuː ˈel/ hoặc /ˈsiːkwəl/, *Nginx* /ˌendʒɪnˈeks/, *data* /ˈdeɪtə/.

## 8. Lịch luyện trong tuần

| Ngày | Việc cụ thể |
| --- | --- |
| T2 | Chọn 3 dự án (1 hiệu năng/kỹ thuật, 1 kiến trúc/microservices, 1 sản phẩm/fullstack hoặc teamwork). Điền template mục 3 cho cả 3. |
| T3 | Luyện dự án 1: nói 5 lần, bấm giờ 2–3'. Viết 3 câu hỏi đào sâu + trả lời ngắn. |
| T4 | Luyện dự án 2. Thử **vẽ kiến trúc** trên giấy/Excalidraw trong khi nói. |
| T5 | Gia sư: trình bày 1 dự án, nhờ gia sư hỏi "Why?" ít nhất 5 lần. |
| T6 | Luyện dự án 3. Ghi âm cả 3. |
| T7 | Nghe lại, sửa answers.md, ghi nhật ký. |

## 9. Prompt cho AI voice

```
You are a senior engineering manager interviewing me for a Senior Java Backend
Engineer role. My English is B1, so speak clearly and not too fast.

1. Ask me: "Tell me about a project you're proud of."
2. Let me speak for up to 3 minutes without interrupting.
3. Then do a deep-dive: ask 5 follow-up questions, one at a time, like a real
   senior interviewer. Focus on: why I chose that technology, what alternatives
   I considered, how I measured the result, what went wrong, and what exactly
   MY role was (not the team's).
4. Then ask me to describe the architecture of the system verbally.

After all questions, give feedback:
- Did I clearly separate my role from the team's role? (yes/no + example)
- Did I give measurable results?
- Did I explain trade-offs?
- My 5 biggest English mistakes, with corrections.
- A rewritten, improved 2-minute version of my project story.
```

## 10. Checklist tự đánh giá

- [ ] Có đủ 6 phần: Context → Problem → Role → Solution → Result → Reflection
- [ ] Context ngắn (dưới 30 giây), người ngoài ngành vẫn hiểu
- [ ] Nói rõ **vai trò của tôi** (dùng "I" ít nhất 5 lần)
- [ ] Có ít nhất 1 **trade-off** / phương án đã cân nhắc
- [ ] Có ít nhất 2 **con số** kết quả
- [ ] Thời lượng 2–3 phút
- [ ] Dùng **past simple** đúng cho việc đã xong
- [ ] Phát âm đúng tên công nghệ (cache, queue, Kubernetes...)
- [ ] Trả lời được 3 câu hỏi đào sâu mà không lúng túng
- [ ] Kết thúc bằng bài học / reflection

## 11. Tài liệu tham khảo

- Tech Interview Handbook (behavioral + project questions): https://www.techinterviewhandbook.org
- ByteByteGo — học cách giải thích kiến trúc rõ ràng: https://bytebytego.com · https://www.youtube.com/@ByteByteGo
- System Design Primer — từ vựng kiến trúc (cache, replica, queue): https://github.com/donnemartin/system-design-primer
