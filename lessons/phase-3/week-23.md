# Tuần 23 — Kiến trúc hệ thống

> Giai đoạn 3 · Tuần 6/9 · Checklist gốc: [phase-3-it-english.md](../../phase-3-it-english.md#tuần-23--kiến-trúc-hệ-thống)

## 1. Mục tiêu tuần

- Dùng chính xác 35+ thuật ngữ kiến trúc: *load balancer, horizontal scaling, replication, sharding, CDN, cache, message queue...*
- Vẽ và giải thích kiến trúc dự án gần nhất trong **5 phút** (T3), theo hướng **đi theo luồng request** (follow the request).
- Giải thích **Caching strategies** và **Message queues (Kafka, RabbitMQ)**.
- Trả lời câu hỏi kiểu system design: *"What happens if this component goes down?"*, *"How would you scale this?"*

## 2. Từ vựng IT

| # | Từ | IPA (Mỹ) | Cách đọc dễ nhớ | Nghĩa | Câu ví dụ |
| --- | --- | --- | --- | --- | --- |
| 1 | load balancer | /loʊd ˈbælənsər/ | "LÂUD BÉ-lần-sơ" | bộ cân bằng tải | The load balancer spreads traffic across three instances. |
| 2 | horizontal scaling (scale out) | | | thêm máy | We scale out by adding more pods. |
| 3 | vertical scaling (scale up) | | | tăng cấu hình máy | Scaling up the DB bought us six months. |
| 4 | instance / node | /ˈɪnstəns/, /noʊd/ | "ÍN-stần(s)", "NÂUD" | một máy/tiến trình chạy | Each instance is stateless. |
| 5 | stateless / stateful | /ˈsteɪtləs/ | "STÂYT-lợs" | không/có giữ trạng thái | Stateless services are easy to scale. |
| 6 | replication | /ˌrɛplɪˈkeɪʃən/ | "rep-li-KÂY-shần" | sao chép dữ liệu | We use replication for high availability. |
| 7 | primary / replica | /ˈrɛplɪkə/ | "PRAI-me-ri", "RÉ-pli-kờ" | bản chính / bản sao | Reads go to the replicas, writes go to the primary. |
| 8 | replication lag | /læɡ/ | "LÉG" | độ trễ sao chép | Because of replication lag, a user may not see their update immediately. |
| 9 | sharding / shard | /ˈʃɑːrdɪŋ/ | "SHAR-đing" | chia dữ liệu theo khóa ra nhiều DB | We shard users by user ID. |
| 10 | partition | /pɑːrˈtɪʃən/ | "par-TÍ-shần" | phân vùng | The Kafka topic has twelve partitions. |
| 11 | CDN (Content Delivery Network) | | "XI-ĐI-EN" | mạng phân phối nội dung | Images are served from a CDN. |
| 12 | edge location | /ɛdʒ/ | "ÉJ" | máy chủ gần người dùng | The CDN caches files at edge locations. |
| 13 | reverse proxy | /rɪˈvɝːs ˈprɑːksi/ | "ri-VƠS PRAK-si" | proxy đứng trước server | Nginx works as a reverse proxy. |
| 14 | API gateway | /ˈɡeɪtweɪ/ | "GÂYT-uây" | cổng vào chung cho API | The API gateway handles auth and rate limiting. |
| 15 | rate limiting | | | giới hạn tần suất | We return 429 when rate limiting kicks in. |
| 16 | high availability (HA) | /əˌveɪləˈbɪləti/ | "ơ-vây-lơ-BI-lơ-ri" | tính sẵn sàng cao | We run two zones for high availability. |
| 17 | single point of failure | | | điểm lỗi duy nhất | One Redis instance is a single point of failure. |
| 18 | failover | /ˈfeɪloʊvər/ | "FÂYL-âu-vơ" | chuyển sang bản dự phòng | Failover to the replica took 30 seconds. |
| 19 | cache hit / miss | /hɪt/, /mɪs/ | "HÍT", "MÍS" | trúng/trượt cache | Our cache hit rate is 95%. |
| 20 | TTL (time to live) | | "TI-TI-EO" | thời gian sống | Product data has a TTL of ten minutes. |
| 21 | eviction / LRU | /ɪˈvɪkʃən/ | "i-VÍK-shần", "EL-A-YU" | loại bỏ khỏi cache / ít dùng gần đây nhất | Redis evicts keys using an LRU policy. |
| 22 | cache invalidation | /ɪnˌvælɪˈdeɪʃən/ | "in-vé-li-ĐÂY-shần" | làm mất hiệu lực cache | Cache invalidation is the hard part. |
| 23 | cache-aside | | | app tự đọc DB rồi ghi cache | We use the cache-aside pattern. |
| 24 | write-through / write-back | | | ghi cache và DB cùng lúc / ghi DB sau | Write-back is fast but can lose data. |
| 25 | stale data | /steɪl/ | "STÊYL" | dữ liệu cũ | Users might see stale data for a few seconds. |
| 26 | message broker | /ˈmɛsɪdʒ ˈbroʊkər/ | "MÉ-sij BRÂU-kơ" | trung gian thông điệp | RabbitMQ is our message broker. |
| 27 | producer / consumer | /prəˈduːsər/, /kənˈsuːmər/ | "prơ-ĐU-sơ", "kần-SU-mơ" | bên gửi / bên nhận | The order service is the producer. |
| 28 | topic | /ˈtɑːpɪk/ | "TA-pik" | chủ đề (Kafka) | We publish to the `order-events` topic. |
| 29 | consumer group | | | nhóm consumer chia việc | Each consumer group gets every message once. |
| 30 | offset | /ˈɔːfsɛt/ | "OF-set" | vị trí đọc trong partition | The consumer commits its offset after processing. |
| 31 | at-least-once / exactly-once | | | giao ít nhất 1 lần / đúng 1 lần | Kafka is usually at-least-once, so consumers must be idempotent. |
| 32 | idempotent | /ˌaɪdəmˈpoʊtənt/ | "ai-đờm-PÂU-tần(t)" | gọi nhiều lần cùng kết quả | The payment handler is idempotent. |
| 33 | dead-letter queue (DLQ) | | "ĐI-EL-KIU" | hàng đợi thư lỗi | After three failures, the message goes to the DLQ. |
| 34 | pub/sub | /pʌb sʌb/ | "PÂB-SÂB" | mô hình xuất bản/đăng ký | Notifications use pub/sub. |
| 35 | backpressure | /ˈbækprɛʃər/ | "BÉK-pre-shơ" | áp lực ngược, hạn chế tốc độ | The queue gives us backpressure when consumers are slow. |
| 36 | throughput / latency | | (tuần 20) | lưu lượng / độ trễ | Kafka is built for high throughput. |
| 37 | availability zone / region | /ˈriːdʒən/ | "RI-giần" | vùng hạ tầng cloud | We deploy across three availability zones. |

## 3. Mẫu câu công việc

**Mở đầu trình bày kiến trúc**
1. Let me walk you through the architecture.
2. I'll follow a request from the user to the database.
3. At a high level, the system has four main parts.
4. Let me start with the big picture, then go into details.

**Mô tả thành phần và luồng**
5. Requests first hit the load balancer, which forwards them to the API gateway.
6. The gateway handles authentication and routes the request to the right service.
7. The order service writes to its own Postgres database.
8. After saving the order, it publishes an `OrderCreated` event to Kafka.
9. The notification service consumes that event and sends an email.
10. Static files are served from a CDN.
11. We cache product data in Redis with a ten-minute TTL.
12. All services are stateless, so we can scale them horizontally.

**Giải thích lý do (why)**
13. We chose this design because ...
14. The main reason was ...
15. We needed to handle traffic spikes during sales.
16. This decouples the order service from the email provider.
17. At our scale, a single primary database is enough.

**Nói về lỗi và mở rộng**
18. If the notification service goes down, messages wait in the queue.
19. The weakest point right now is ...
20. Redis is a single point of failure, so we're moving to a cluster.
21. If traffic grew ten times, the first bottleneck would be the database.
22. To scale reads, we'd add read replicas and more caching.
23. For writes, we would eventually need sharding.

**Nói khi vẽ sơ đồ**
24. Here's the client, here's the load balancer.
25. This arrow means a synchronous call; the dashed one is async.
26. Let me draw the database here.
27. This box is our main service.
28. Does the diagram make sense?

## 4. Hội thoại mẫu

### Hội thoại 1: Trình bày kiến trúc cho đồng nghiệp mới (rút gọn)

> **Nhat:** Let me walk you through the architecture of our e-commerce backend. I'll follow an order from the user to the database.
> **Huy:** Sounds good.
> **Nhat:** The user opens the web app. Static files, like JavaScript and images, come from CloudFront, our CDN. When the user places an order, the request goes to an AWS load balancer, then to the API gateway, which checks the JWT token.
> **Huy:** And then the order service?
> **Nhat:** Right. The order service is a Spring Boot app running on Kubernetes, usually four pods. It saves the order in Postgres, in one transaction, and then publishes an `OrderCreated` event to Kafka.
> **Huy:** Why Kafka and not a direct REST call to the email service?
> **Nhat:** Two reasons. First, the user doesn't have to wait for the email or the warehouse system. Second, if those services are down, the events wait in Kafka, and nothing is lost. We just process them later.
> **Huy:** What about the product pages? They must get a lot of traffic.
> **Nhat:** Yes, around ninety percent of traffic is reads. So we cache product data in Redis with a ten-minute TTL, and the database has two read replicas.
> **Huy:** Got it. What's the weakest part?
> **Nhat:** Honestly, the primary database. All writes go there. It's fine now, but if traffic grew ten times, that would be the first bottleneck.

### Hội thoại 2: Câu hỏi "what if" (giống phỏng vấn system design)

> **Interviewer:** What happens if Redis goes down?
> **Nhat:** Since we use the cache-aside pattern, the application falls back to the database. The site keeps working, but it's slower, and the database load goes up a lot.
> **Interviewer:** Could that take down the database?
> **Nhat:** It could, especially at peak time. That's called a cache stampede. To protect it, we have a timeout on Redis calls, rate limiting at the gateway, and we're moving to Redis in cluster mode with replicas, so a single node failure doesn't empty the cache.
> **Interviewer:** And if a consumer fails to process a message?
> **Nhat:** We retry three times with backoff. After that, the message goes to a dead-letter queue, and we get an alert. Our consumers are idempotent, so processing a message twice is safe.

## 5. Bài giải thích kỹ thuật mẫu

### 5.1 T4 — Caching strategies

> A cache is a fast storage layer, usually in memory, that keeps copies of data so we don't have to fetch it from a slower source, like a database or an external API, every time. Caching can happen at many levels: in the browser, at a CDN, inside the application, or in a shared cache like Redis.
>
> There are a few common strategies. The most popular is **cache-aside**, also called lazy loading. The application first checks the cache. On a cache hit, it returns the data. On a miss, it reads from the database, stores the result in the cache, and then returns it. It's simple, and only data that is actually requested gets cached.
>
> With **write-through**, every write goes to the cache and the database at the same time, so the cache is always fresh, but writes are slower. With **write-back**, or write-behind, we write to the cache first and update the database later, asynchronously. Writes are very fast, but we can lose data if the cache crashes.
>
> The hardest part is invalidation: keeping the cache consistent with the source. Common tools are a TTL, so entries expire automatically, deleting the key when the data changes, and an eviction policy like LRU when memory is full.
>
> So, caching is a trade-off between speed and freshness. Cache data that is read often and changes rarely, and always ask: how stale can this data be?

**5 cụm từ dùng lại:**
1. *X is a fast ... that keeps copies of ...*
2. *The most popular is ..., also called ...*
3. *On a hit, ... On a miss, ...*
4. *The hardest part is ...*
5. *X is a trade-off between ... and ...*

### 5.2 T6 — Message queues (Kafka, RabbitMQ)

> A message queue lets services communicate asynchronously. Instead of calling another service directly and waiting, a producer sends a message to a broker, and one or more consumers process it later. This decouples the services: the producer doesn't need to know who consumes the message, and if a consumer is slow or down, messages simply wait. Queues also absorb traffic spikes.
>
> RabbitMQ is a traditional message broker. Producers send messages to an exchange, which routes them to queues based on rules. A consumer takes a message, processes it, and sends an acknowledgment, and then the message is removed from the queue. RabbitMQ is great for task queues and flexible routing, for example "send this job to a worker".
>
> Kafka works differently. It's a distributed, append-only log. Messages are written to topics, which are split into partitions, and they are kept for a configured time, for example seven days, even after they are read. Each consumer group tracks its own position, called the offset. So many different services can read the same events independently, and you can even replay old events. Order is guaranteed only within a partition. Kafka is built for very high throughput and event streaming.
>
> With both tools, delivery is usually at-least-once, so the same message might arrive twice. That's why consumers should be idempotent. Failed messages often go to a dead-letter queue.
>
> In short: RabbitMQ for task distribution and routing; Kafka for high-volume event streams and replay.

**5 cụm từ dùng lại:**
1. *X lets services communicate asynchronously.*
2. *Instead of ..., a producer ...*
3. *X works differently. It's ...*
4. *X is guaranteed only within ...*
5. *That's why consumers should be ...*

### 5.3 T3 — Khung trình bày kiến trúc dự án 5 phút

| Phút | Nội dung | Câu mở |
| --- | --- | --- |
| 0:00–0:45 | Bối cảnh: sản phẩm gì, ai dùng, quy mô | "The project is ... It's used by about ... users." |
| 0:45–1:30 | Bức tranh lớn: 4–6 khối chính | "At a high level, there are ... main parts." |
| 1:30–3:00 | Đi theo 1 request quan trọng | "Let me follow an order from the user to the database." |
| 3:00–4:00 | Hai quyết định thiết kế và lý do | "We chose Kafka because ... The trade-off was ..." |
| 4:00–4:40 | Điểm yếu, cách mở rộng | "The weakest point is ... If traffic grew ten times, ..." |
| 4:40–5:00 | Vai trò của bạn | "My part was the order service and the Kafka integration." |

## 6. Mẫu viết

**Mô tả kiến trúc trong README / tài liệu thiết kế**

```
## Architecture overview

The system consists of four Spring Boot services behind an API gateway.

- **API Gateway** - authentication (JWT), rate limiting, routing.
- **Order Service** - owns orders; PostgreSQL (primary + 2 read replicas).
- **Catalog Service** - product data; cached in Redis (TTL 10 min, cache-aside).
- **Notification Service** - consumes `order-events` from Kafka; sends emails.

Communication: synchronous REST for queries; Kafka events for side effects.
Deployment: Kubernetes (EKS), 3 availability zones, HPA based on CPU.
Known limitations: single primary database for writes; no multi-region failover.
```

**Bảng quyết định công nghệ**

```
| Need                   | Choice      | Why                                  | Trade-off               |
| Async events           | Kafka       | Replay, multiple consumers, volume   | Ops complexity          |
| Hot product reads      | Redis       | Sub-ms reads, TTL support            | Stale data up to 10 min |
| Static assets          | CloudFront  | Lower latency worldwide              | Invalidation on deploy  |
```

## 7. Bài tập

1. **Ghép:** (a) sharding (b) replication (c) CDN (d) load balancer (e) failover — (1) phân phối file tĩnh từ máy chủ gần người dùng (2) chia dữ liệu ra nhiều DB theo khóa (3) chuyển sang bản dự phòng khi lỗi (4) chia traffic ra nhiều instance (5) sao chép dữ liệu sang nhiều node.
2. **Chọn chiến lược cache:** (a) Trang chi tiết sản phẩm, đọc nhiều, ít thay đổi. (b) Bộ đếm lượt xem, ghi rất nhiều, mất vài lượt cũng được. (c) Hồ sơ người dùng cần luôn mới ngay sau khi cập nhật.
3. **Kafka hay RabbitMQ?** (a) Gửi job resize ảnh cho nhiều worker. (b) 5 service khác nhau cần đọc cùng sự kiện đơn hàng, và cần replay khi deploy service mới. (c) Định tuyến message theo routing key phức tạp.
4. **Điền từ:** idempotent, stateless, replica, TTL, bottleneck. (a) Set a ___ of 60 seconds on this key. (b) Because the API is ___, any pod can handle any request. (c) The consumer must be ___ because messages can arrive twice. (d) Reads go to the ___. (e) The single database is our main ___.
5. **Viết** phần "Architecture overview" (6–8 dòng) cho dự án gần nhất của bạn, theo mẫu mục 6.
6. **Nói (T3):** vẽ kiến trúc dự án trên giấy, trình bày 5 phút theo khung 5.3, ghi âm hoặc quay video.
7. **Nói:** trả lời 3 câu "what if": (a) What if the database goes down? (b) What if traffic grows 10x? (c) What if a message is processed twice?

## 8. Tài liệu

- [ByteByteGo YouTube](https://www.youtube.com/@ByteByteGo) — kênh tốt nhất cho tuần này: tìm "caching strategies", "Kafka", "load balancer", "CDN".
- [ByteByteGo](https://bytebytego.com) — sách/blog System Design (một phần miễn phí).
- [Apache Kafka documentation](https://kafka.apache.org/documentation/) — đọc phần *Introduction*.
- [RabbitMQ tutorials](https://www.rabbitmq.com/tutorials) — phần "Work Queues" và "Routing" giải thích rất rõ.
- [roadmap.sh](https://roadmap.sh) — roadmap "System Design".
- [InfoQ](https://www.infoq.com) — đọc 1 case study kiến trúc (mục *Architecture & Design*), ghi 10 cụm từ hay.
- [GOTO Conferences](https://www.youtube.com/@GOTO-) — tìm "event-driven architecture".

## 9. Đáp án

**Bài 1:** a-2, b-5, c-1, d-4, e-3.

**Bài 2:** (a) cache-aside với TTL (b) write-back / write-behind (gộp ghi xuống DB định kỳ) (c) write-through, hoặc xóa key khi cập nhật (invalidate on write).

**Bài 3:** (a) RabbitMQ (task queue) — Kafka cũng làm được nhưng RabbitMQ đơn giản hơn (b) Kafka (c) RabbitMQ (exchange + routing key).

**Bài 4:** (a) TTL (b) stateless (c) idempotent (d) replica (e) bottleneck.

**Bài 7 (gợi ý):**
(a) "We have a replica in another availability zone. If the primary fails, we fail over automatically, which takes about 30 seconds. Some requests fail during that time, and the clients retry."
(b) "The stateless services can scale horizontally. The first bottleneck would be the primary database, so we'd add caching and read replicas first, and consider sharding for writes later."
(c) "Our consumers are idempotent. We store the event ID in a processed-events table, so if the same message arrives again, we skip it."

**Bài 5, 6:** tự chấm: theo đúng khung, có ít nhất 1 trade-off và 1 điểm yếu, ≤ 5 phút.
