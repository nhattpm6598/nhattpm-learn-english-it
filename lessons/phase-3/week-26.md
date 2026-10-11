# Tuần 26 — Tổng ôn: trình bày dự án 5 phút

> Giai đoạn 3 · Tuần 9/9 · Checklist gốc: [phase-3-it-english.md](../../phase-3-it-english.md#tuần-26--tổng-ôn)

## 1. Mục tiêu tuần

- Chọn **1 dự án lớn nhất**, viết dàn ý và trình bày trong **5 phút**: *Context → Architecture → My role → Challenges & decisions → Results → Lessons*.
- Trả lời được 10 câu hỏi đào sâu kiểu *"Why did you choose...?"*, *"What would you do differently?"*
- **Mốc kiểm tra (T6):** quay video 5 phút giải thích kiến trúc dự án, lưu link vào `log/progress.md`.
- Tự đánh giá: giải thích được **20 khái niệm kỹ thuật** từ tuần 18–25 (bảng ở mục 7).

**Lịch tuần này**

| Ngày | Việc | Dùng phần nào |
| --- | --- | --- |
| T2 | Viết dàn ý (outline) | Mục 6.1 |
| T3 | Luyện trình bày 5', ghi âm 2 lần | Mục 5.1, 3 |
| T4 | Luyện trả lời câu hỏi đào sâu | Mục 5.2 |
| T5 | Gia sư: trình bày và nhận góp ý | Mục 4, 6.2 |
| T6 | Quay video mốc kiểm tra | Mục 6.3 |
| T7 | Ôn + nhật ký giai đoạn | Mục 7 |

## 2. Từ vựng: trình bày dự án

| # | Từ / cụm | IPA (Mỹ) | Cách đọc dễ nhớ | Nghĩa | Câu ví dụ |
| --- | --- | --- | --- | --- | --- |
| 1 | context / background | /ˈkɑːntɛkst/ | "KAN-tékst" | bối cảnh | Let me give you some context first. |
| 2 | problem statement | /ˈprɑːbləm ˈsteɪtmənt/ | "PRA-blầm STÊYT-mần(t)" | mô tả vấn đề | The problem was simple: checkout was too slow. |
| 3 | goal / objective | /əbˈdʒɛktɪv/ | "ợb-GIÉK-tiv" | mục tiêu | Our goal was to handle 5x more traffic. |
| 4 | constraint | /kənˈstreɪnt/ | "kần-STRÊYNT" | ràng buộc | The main constraint was a three-month deadline. |
| 5 | requirement (functional / non-functional) | | | yêu cầu (chức năng / phi chức năng) | A key non-functional requirement was 99.9% availability. |
| 6 | stakeholder | /ˈsteɪkhoʊldər/ | "STÂYK-hâul-đơ" | bên liên quan | I worked closely with business stakeholders. |
| 7 | high-level overview | | | tổng quan | Here's a high-level overview of the system. |
| 8 | component | /kəmˈpoʊnənt/ | "kầm-PÂU-nần(t)" | thành phần | The system has four main components. |
| 9 | data flow | /ˈdeɪtə floʊ/ | "ĐÂY-rờ FLÂU" | luồng dữ liệu | Let me show you the data flow. |
| 10 | integration | /ˌɪntəˈɡreɪʃən/ | "in-tơ-GRÂY-shần" | tích hợp | The hardest part was the bank integration. |
| 11 | legacy system | /ˈlɛɡəsi/ | "LÉ-gơ-si" | hệ thống cũ | We had to keep the legacy system running. |
| 12 | trade-off | /ˈtreɪdɔːf/ | "TRÂY-đoóf" | đánh đổi | The trade-off was consistency versus speed. |
| 13 | bottleneck | /ˈbɑːtəlnɛk/ | "BA-rồ-nek" | nút thắt | We found the bottleneck with profiling. |
| 14 | challenge | /ˈtʃælɪndʒ/ | "CHÉ-linj" | thách thức | The biggest challenge was data migration. |
| 15 | approach | /əˈproʊtʃ/ | "ơ-PRÂUCH" | cách tiếp cận | Our approach was to migrate one module at a time. |
| 16 | ownership / owned | /ˈoʊnərʃɪp/ | "ÂU-nơ-ship" | quyền làm chủ | I owned the payment service end to end. |
| 17 | contribute / contribution | /kənˈtrɪbjuːt/ | "kần-TRÍ-biut" | đóng góp | My main contribution was the event pipeline. |
| 18 | outcome / result | /ˈaʊtkʌm/ | "AOT-kâm" | kết quả | The outcome was a 60% drop in latency. |
| 19 | impact | /ˈɪmpækt/ | "ÍM-pékt" | tác động | The business impact was fewer abandoned carts. |
| 20 | measurable / metric | /ˈmɛʒərəbəl/ | "MÉ-giơ-rơ-bồ" | đo được / chỉ số | We tracked three metrics. |
| 21 | roll out / rollout | /ˈroʊlaʊt/ | "RÂUL-aot" | phát hành dần | We rolled it out to 10% of users first. |
| 22 | in hindsight | /ˈhaɪndsaɪt/ | "HAIND-sait" | nhìn lại thì | In hindsight, we should have added tracing earlier. |
| 23 | lesson learned | | | bài học | The main lesson learned was to test with real data. |
| 24 | scalable / scale | /ˈskeɪləbəl/ | "SKÂY-lơ-bồ" | mở rộng được | The design is scalable to ten times the load. |
| 25 | maintainable | /meɪnˈteɪnəbəl/ | "mên-TÂY-nơ-bồ" | dễ bảo trì | We wanted code that was easy to maintain. |
| 26 | proof of concept | | | bản thử nghiệm | We built a proof of concept in one week. |
| 27 | iterate / iteration | /ˈɪtəreɪt/ | "Í-rơ-rêyt" | lặp, cải tiến dần | We iterated on the design with user feedback. |
| 28 | cross-functional team | | | team liên chức năng | I worked in a cross-functional team of eight. |
| 29 | take away / takeaway | /ˈteɪkəweɪ/ | "TÂYK-ơ-uây" | điều rút ra | My key takeaway is ... |
| 30 | to sum up / in summary | | | tóm lại | To sum up, ... |
| 31 | elaborate (on) | /ɪˈlæbəreɪt/ | "i-LÉ-bơ-rêyt" | nói chi tiết hơn | Could you elaborate on the caching part? |
| 32 | revisit | /ˌriːˈvɪzɪt/ | "ri-VÍ-zit" | xem lại | We decided to revisit the design after launch. |

## 3. Mẫu câu: khung trình bày 5 phút

**Mở đầu (0:00–0:30)**
1. Today I'd like to talk about [project], a [type of system] I worked on at [company].
2. I'll cover the context, the architecture, my role, a few challenges and the results.

**Bối cảnh (0:30–1:15)**
3. The company is a [type] with about [N] users.
4. The problem we wanted to solve was ...
5. Our main goals were ... and the main constraints were ...

**Kiến trúc (1:15–2:45)**
6. At a high level, the system has [N] main components.
7. Let me follow a typical request: ...
8. For communication between services, we used ...
9. We store ... in ..., because ...

**Vai trò (2:45–3:15)**
10. I was one of [N] backend engineers. My part was ...
11. I owned ... end to end, from design to production.
12. I also worked closely with the frontend team / the PO / QA.

**Thách thức và quyết định (3:15–4:15)**
13. The biggest challenge was ...
14. We considered two options: ... and ...
15. We chose ... because ... The trade-off was ...

**Kết quả và bài học (4:15–5:00)**
16. As a result, [metric] improved from ... to ...
17. In hindsight, I would ...
18. My key takeaway was ...
19. That's it from me. I'm happy to answer any questions.

**Khi bị hỏi giữa chừng / không biết câu trả lời**
20. Good question. Let me think for a second.
21. I wasn't directly involved in that part, but as far as I know, ...
22. I don't remember the exact number, but it was around ...
23. I'm not sure, to be honest. If I had to guess, I'd say ... but I'd verify it.
24. Could you rephrase the question? I want to make sure I understand.

## 4. Hội thoại mẫu

### Hội thoại 1: Sau phần trình bày, gia sư hỏi đào sâu

> **Tutor:** Thanks, that was clear. Why did you choose Kafka instead of RabbitMQ?
> **Nhat:** Good question. We had several consumers for the same order events: billing, warehouse, notifications and analytics. With Kafka, each one reads the topic independently with its own consumer group. We also wanted to replay events when we added a new service. RabbitMQ could do the first part, but replay would be much harder.
> **Tutor:** And what was the downside?
> **Nhat:** Operating Kafka. It's more complex than RabbitMQ. We solved that by using a managed service, Amazon MSK, so we didn't manage brokers ourselves.
> **Tutor:** Makes sense. What would you do differently?
> **Nhat:** In hindsight, I'd add distributed tracing from day one. In the first months, when an order got stuck, it took us a long time to find which service was the problem.

### Hội thoại 2: Góp ý cho phần trình bày (nhận feedback)

> **Tutor:** Can I give you some feedback on your presentation?
> **Nhat:** Yes, please. Be honest.
> **Tutor:** The structure was very good. But you spent almost three minutes on the architecture, and only twenty seconds on your own role.
> **Nhat:** That's a fair point. I think I'm a bit shy about talking about myself.
> **Tutor:** In interviews, that's the most important part. Use "I" more. You said "we" almost every time.
> **Nhat:** Got it. I'll say "I designed" and "I implemented" when it was really my work. Anything about my English?
> **Tutor:** A few final sounds: "designed", "used", "reduced". The "d" at the end was missing. And try to slow down a little when you give numbers.
> **Nhat:** Thanks, that's really helpful. I'll record it again tonight.

## 5. Bài mẫu

### 5.1 Bài trình bày dự án mẫu (khoảng 5 phút, ~650 từ)

> Đây là ví dụ. Thay toàn bộ thông tin bằng dự án thật của bạn. Đọc to với tốc độ khoảng 130 từ/phút.

> Today I'd like to talk about the order platform I worked on at ABC Commerce, an online marketplace in Vietnam with about two million monthly users. I'll cover the context, the architecture, my role, the main challenges, and the results.
>
> **Context.** When I joined, everything ran in one big Spring Boot monolith with one MySQL database. It worked well at the beginning, but during sales events, like eleven-eleven, traffic went up about ten times. Checkout became very slow, and twice the whole site went down. Also, five teams were working in the same codebase, so every release was risky and we could only deploy once a week. Our goal was to handle ten times the normal traffic during sales and to let teams deploy independently. The main constraint was that we couldn't stop the business: the migration had to happen with zero downtime.
>
> **Architecture.** We moved to an event-driven architecture. Let me follow an order. The user's request first goes through a load balancer to an API gateway, which handles authentication and rate limiting. Then it reaches the order service, a Spring Boot application running on Kubernetes. The order service saves the order in its own PostgreSQL database and, in the same transaction, writes an event to an outbox table. A separate process publishes that event to a Kafka topic. Then the payment, warehouse and notification services each consume the event and do their part. Product data, which is read very often, is cached in Redis. And static files are served from a CDN.
>
> **My role.** I was one of six backend engineers. I owned the order service and the Kafka integration end to end. I designed the event format, implemented the outbox pattern, and wrote the migration plan for moving order data out of the monolith. I also built the internal dashboard in React that the support team uses to track stuck orders.
>
> **Challenges and decisions.** The biggest challenge was consistency. In the monolith, creating an order and reserving stock happened in one database transaction. With separate services, we couldn't do that anymore. We considered two options: distributed transactions with two-phase commit, or eventual consistency with events and compensation. We chose events, because two-phase commit is slow and fragile. The trade-off was complexity: for example, if payment fails, we have to publish an event that releases the reserved stock. To make this safe, I made every consumer idempotent, so processing the same event twice has no effect.
>
> The second challenge was the migration itself. We used the strangler fig pattern: we moved one feature at a time, and the gateway routed traffic either to the monolith or to the new service. We rolled out each step to five percent of users first.
>
> **Results.** After the migration, p95 checkout latency dropped from about one point two seconds to around four hundred milliseconds. During the last eleven-eleven sale, we handled about eight times the normal traffic without any downtime. And teams went from one release a week to several releases a day.
>
> **Lessons.** In hindsight, I would add distributed tracing from day one. In the first months, finding a stuck order across four services took too long. My key takeaway is that microservices solve organizational and scaling problems, but they move the complexity into operations, so monitoring is not optional.
>
> That's it from me. I'm happy to answer any questions.

### 5.2 Câu hỏi đào sâu và câu trả lời mẫu (T4)

**1. Why did you choose PostgreSQL over MongoDB?**
> Our order data is very relational: orders, items, payments, refunds. We needed transactions and strong consistency for money. Postgres gives us that, and the team already knew it well. For the few flexible fields, we used a JSONB column.

**2. How did you handle failures between services?**
> Inside the order flow, we used events instead of direct calls, so a slow service doesn't block checkout. Consumers retry with exponential backoff, and after three failures the message goes to a dead-letter queue with an alert. For the few synchronous calls, we use timeouts and a circuit breaker with Resilience4j.

**3. How would you scale it ten times further?**
> The stateless services can scale horizontally on Kubernetes. The first bottleneck would be the order database. I'd first add read replicas and more caching for reads, then partition the order table by date. If writes were still the problem, I'd shard by customer ID. On the Kafka side, we'd increase the number of partitions.

**4. How did you test it?**
> Unit tests for the business logic, integration tests with Testcontainers for Postgres and Kafka, and contract tests between services. Before the sale, we ran load tests with k6 at ten times normal traffic on a staging environment.

**5. What was the hardest bug you faced?**
> Some orders were processed twice during a Kafka rebalance. A consumer had processed the message but hadn't committed the offset yet. That's at-least-once delivery. The fix was idempotency: we store the event ID in a processed-events table with a unique constraint, in the same transaction as the business update.

**6. What would you do differently?**
> I'd add distributed tracing from the start, and I'd invest earlier in a shared library for the outbox and idempotency logic. Each team implemented it slightly differently at first.

**7. How did you decide the service boundaries?**
> We followed business capabilities: orders, payments, inventory, notifications. Each service owns its data. A good sign was that most features only needed changes in one service.

**8. Did you disagree with anyone? How did you handle it?**
> Yes. A senior colleague wanted to split into fifteen small services at once. I was worried about the operational overhead for our team size. I suggested we start with four services and measure. We wrote an ADR with both options, and the team agreed on the smaller step.

**9. What was your biggest personal contribution?**
> The outbox pattern and the idempotent consumers. Before that, we sometimes lost events when the service crashed after saving an order. After my change, we had zero lost events in production.

**10. How did you deal with data consistency in reports?**
> Reports read from a separate read model that is updated from events, so they can be a few seconds behind. We agreed with the business that a delay of up to one minute was acceptable for reports.

## 6. Mẫu viết

### 6.1 Dàn ý trình bày (T2) — điền vào

```
PROJECT: ____________________   COMPANY/YEAR: __________   MY TITLE: __________

1. CONTEXT (45s)
   - Product / users / scale: ______________________________
   - Problem: ______________________________________________
   - Goals (with numbers): _________________________________
   - Constraints: __________________________________________

2. ARCHITECTURE (90s)  -> draw it!
   - Main components (4-6): ________________________________
   - Request flow: client -> ____ -> ____ -> ____ -> DB
   - Data storage + cache: _________________________________
   - Sync vs async communication: __________________________

3. MY ROLE (30-45s)  -> use "I"
   - I owned / designed / built: ___________________________

4. CHALLENGES & DECISIONS (60s)
   - Challenge 1: ________  Options: ______ vs ______  Chose: ______ because ______
   - Trade-off: ___________________________________________

5. RESULTS (30s)  -> numbers
   - _____ improved from _____ to _____

6. LESSONS (15s)
   - In hindsight, I would ________________________________
```

### 6.2 Phiếu tự chấm / gia sư chấm (T5)

| Tiêu chí | 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- | --- |
| Cấu trúc rõ (người nghe biết đang ở phần nào) | | | | | |
| Thời gian 4:30–5:30 | | | | | |
| Dùng "I" cho phần việc của mình | | | | | |
| Có ít nhất 2 con số kết quả | | | | | |
| Có ít nhất 1 trade-off | | | | | |
| Phát âm từ IT đúng (tuần 18) | | | | | |
| Âm cuối -ed, -s rõ | | | | | |
| Ít "uhm", ngắt nghỉ tự nhiên | | | | | |
| Trả lời câu hỏi đào sâu không bị đứng | | | | | |

### 6.3 Checklist quay video mốc kiểm tra (T6)

- [ ] Sơ đồ kiến trúc rõ ràng (giấy, bảng trắng, hoặc Excalidraw/draw.io trên màn hình).
- [ ] Quay 1 lần liên tục, không cắt ghép (giống phỏng vấn thật).
- [ ] Thời lượng 5 phút ± 30 giây.
- [ ] Xem lại, ghi 3 điểm làm tốt và 3 điểm cần sửa vào `log/progress.md`.
- [ ] Lưu link video (Google Drive / YouTube không công khai) vào `log/progress.md`.
- [ ] So sánh với bản ghi âm tự giới thiệu ở tuần 8: tiến bộ ở đâu?

### 6.4 Nhật ký giai đoạn (T7) — mẫu cho `log/progress.md`

```
## Phase 3 review (Weeks 18-26)
- Video: <link>
- Concepts I can explain confidently: 17/20
- Still weak: GC tuning, browser rendering details
- CV: done (reviewed by tutor on <date>)
- Biggest improvement: I can explain my project without notes.
- Focus for Phase 4: answering follow-up questions faster, behavioral questions (STAR).
```

## 7. Bài tập

1. **Tự kiểm tra 20 khái niệm.** Mỗi khái niệm nói 60–90 giây không nhìn bài. Đánh dấu ✓ nếu trôi chảy, ~ nếu còn ngập ngừng, ✗ nếu không nói được. Ôn lại bài mẫu của mục ✗.

   | # | Khái niệm | Tuần | | # | Khái niệm | Tuần |
   | --- | --- | --- | --- | --- | --- | --- |
   | 1 | What is an API? | 18 | | 11 | Logging, monitoring, alerting | 22 |
   | 2 | REST vs GraphQL | 18 | | 12 | Java garbage collection | 22 |
   | 3 | Scrum vs Kanban | 19 | | 13 | Load balancing & horizontal scaling | 23 |
   | 4 | Story points & velocity | 19 | | 14 | Replication vs sharding | 23 |
   | 5 | Monolith vs Microservices | 20 | | 15 | Caching strategies | 23 |
   | 6 | SQL vs NoSQL | 20 | | 16 | Message queues (Kafka, RabbitMQ) | 23 |
   | 7 | ACID vs eventual consistency | 20 | | 17 | CDN | 23 |
   | 8 | Multithreading & race conditions | 21 | | 18 | How a browser renders a page | 24 |
   | 9 | SOLID principles | 21 | | 19 | Frontend state management | 24 |
   | 10 | Code review best practices | 21 | | 20 | Idempotency | 23 |

2. **Điền vào dàn ý 6.1** cho dự án thật của bạn.
3. **Chuyển "we" thành "I"** khi đúng là việc của bạn: (a) "We designed the event format." (b) "We found the memory leak." (c) "We improved the latency."
4. **Trả lời "I don't know" một cách chuyên nghiệp:** viết 2 câu cho câu hỏi "What was the exact cost of your AWS infrastructure?" khi bạn không biết.
5. **Viết câu kết quả có số liệu** từ thông tin: thời gian deploy trước 2 giờ, sau 15 phút, nhờ GitHub Actions.
6. **Nói:** trả lời 5 câu hỏi đào sâu ở mục 5.2 bằng thông tin dự án thật của bạn, mỗi câu 45–90 giây.
7. **Mốc kiểm tra:** quay video 5 phút (checklist 6.3).

## 8. Tài liệu

- [ByteByteGo YouTube](https://www.youtube.com/@ByteByteGo) — xem lại video về các khái niệm bạn đánh ✗.
- [GOTO Conferences](https://www.youtube.com/@GOTO-) — xem 1 talk "case study" kiến trúc: chú ý cách speaker mở đầu, chuyển ý và kết thúc. Ghi lại 10 câu chuyển ý.
- [InfoQ](https://www.infoq.com) — mục *Architecture & Design* có nhiều bài/talk dạng "How we migrated X to Y": rất giống bài trình bày bạn cần làm.
- [roadmap.sh](https://roadmap.sh) — kiểm tra lại các chủ đề trong roadmap Backend/System Design còn thiếu.
- [Refactoring.Guru](https://refactoring.guru) — ôn design patterns trước giai đoạn phỏng vấn.
- Prompt AI luyện câu hỏi đào sâu:
  ```
  I'll describe a project I worked on. Act as a senior interviewer. Ask me
  follow-up questions one at a time ("Why did you choose...?", "What would you do
  differently?", "How would you scale it?"). After each answer, give short feedback
  on my English and on the technical content.
  ```

## 9. Đáp án

**Bài 3 (gợi ý):**
(a) "I designed the event format, and the team reviewed it."
(b) "I found the memory leak by analyzing a heap dump."
(c) "I improved the p95 latency from 1.2 seconds to 400 milliseconds by adding caching."
(Chỉ dùng "I" khi đúng là bạn làm. Nói thật quan trọng hơn nói hay.)

**Bài 4 (gợi ý):** "I don't know the exact number, because the platform team managed the budget. As far as I remember, it was in the range of a few thousand dollars a month, and our team's services were a small part of it."

**Bài 5 (gợi ý):** "I automated the deployment pipeline with GitHub Actions, reducing deployment time from two hours to fifteen minutes."

**Bài 1, 2, 6, 7:** tự chấm bằng phiếu 6.2. Mục tiêu hoàn thành giai đoạn: ≥ 17/20 khái niệm đạt ✓, video 5 phút đã lưu link.
