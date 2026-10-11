# Tuần 20 — Họp và thảo luận kỹ thuật

> Giai đoạn 3 · Tuần 3/9 · Checklist gốc: [phase-3-it-english.md](../../phase-3-it-english.md#tuần-20--họp-và-thảo-luận-kỹ-thuật)

## 1. Mục tiêu tuần

- Đề xuất giải pháp mà không nghe như ra lệnh: *What if we..., I'd suggest..., One option is...*
- Phản đối lịch sự, dựa trên lý do kỹ thuật: *I have a concern about..., Have we considered...?*
- Nói về **trade-off** (đánh đổi): mọi lựa chọn đều có ưu và nhược điểm. Đây là kỹ năng phân biệt Medior với Senior.
- Giải thích **Monolith vs Microservices** và **SQL vs NoSQL** trong 2–3 phút mỗi bài.
- Tranh luận chọn công nghệ với gia sư (T5) mà không bị "đứng hình".

**Văn hóa họp quốc tế (khác Việt Nam ở điểm nào):**
- Im lặng thường bị hiểu là "đồng ý" hoặc "không có ý kiến". Nếu chưa hiểu, hãy hỏi ngay.
- Phản đối ý của senior là bình thường, miễn là có lý do và giọng lịch sự.
- Dùng "softeners" (từ làm mềm): *I think, maybe, might, could, a bit, I'm not sure, but...*

## 2. Từ vựng IT

| # | Từ | IPA (Mỹ) | Cách đọc dễ nhớ | Nghĩa | Câu ví dụ |
| --- | --- | --- | --- | --- | --- |
| 1 | agenda | /əˈdʒɛndə/ | "ơ-GIÉN-đờ" | chương trình họp | Let's go through the agenda. |
| 2 | action item | /ˈækʃən ˈaɪtəm/ | "ÉK-shần AI-rầm" | việc cần làm sau họp | Let me write down the action items. |
| 3 | trade-off | /ˈtreɪdɔːf/ | "TRÂY-đoóf" | sự đánh đổi | The trade-off is speed versus consistency. |
| 4 | proposal / propose | /prəˈpoʊzəl/ | "prơ-PÂU-zồ" | đề xuất | I have a proposal for the new search service. |
| 5 | concern | /kənˈsɝːn/ | "kần-SƠN" | lo ngại | My main concern is the migration time. |
| 6 | alternative | /ɔːlˈtɝːnətɪv/ | "ol-TƠ-nơ-tiv" | phương án khác | Is there an alternative to Elasticsearch? |
| 7 | pros and cons | /proʊz ən kɑːnz/ | "PRÂUZ ần KANZ" | ưu và nhược | Let's list the pros and cons. |
| 8 | consensus | /kənˈsɛnsəs/ | "kần-SÉN-sợs" | sự đồng thuận | I think we have consensus on Postgres. |
| 9 | bottleneck | /ˈbɑːtəlnɛk/ | "BA-rồ-nek" | nút thắt cổ chai | The database is the bottleneck. |
| 10 | scalability | /ˌskeɪləˈbɪləti/ | "skây-lơ-BI-lơ-ri" | khả năng mở rộng | Scalability isn't a problem at our size. |
| 11 | maintainability | /meɪnˌteɪnəˈbɪləti/ | "mên-tây-nơ-BI-lơ-ri" | khả năng bảo trì | This approach is better for maintainability. |
| 12 | latency | /ˈleɪtənsi/ | "LÂY-tần-si" | độ trễ | P99 latency went up to 800 milliseconds. |
| 13 | throughput | /ˈθruːpʊt/ | "THRU-put" | lưu lượng xử lý | We need a throughput of 5,000 messages per second. |
| 14 | overhead | /ˈoʊvərhɛd/ | "ÂU-vơ-hed" | chi phí phụ | Microservices add operational overhead. |
| 15 | learning curve | /ˈlɝːnɪŋ kɝːv/ | "LƠ-ning KƠV" | độ khó khi học | Kafka has a steep learning curve. |
| 16 | proof of concept (PoC) | /pruːf əv ˈkɑːnsɛpt/ | "PRUF ợv KAN-sept" | bản thử nghiệm ý tưởng | Let's build a quick PoC before we decide. |
| 17 | monolith | /ˈmɑːnəlɪθ/ | "MA-nơ-lith" | ứng dụng nguyên khối | We started with a monolith. |
| 18 | microservice | /ˈmaɪkroʊˌsɝːvɪs/ | "MAI-krâu-sơ-vis" | dịch vụ nhỏ độc lập | Each microservice has its own database. |
| 19 | coupling | /ˈkʌplɪŋ/ | "KÂP-ling" | mức phụ thuộc lẫn nhau | Tight coupling makes changes risky. |
| 20 | cohesion | /koʊˈhiːʒən/ | "kâu-HI-giần" | mức gắn kết bên trong | High cohesion means related code lives together. |
| 21 | service boundary | /ˈbaʊndəri/ | "BAO-đơ-ri" | ranh giới dịch vụ | Where should we draw the service boundary? |
| 22 | distributed system | /dɪˈstrɪbjətɪd/ | "đì-STRÍ-biu-tid" | hệ phân tán | Debugging a distributed system is hard. |
| 23 | network call | | | lời gọi qua mạng | Every network call can fail. |
| 24 | relational database | /rɪˈleɪʃənəl/ | "ri-LÂY-shần-nồ" | CSDL quan hệ | Postgres is a relational database. |
| 25 | schema migration | /ˈskiːmə maɪˈɡreɪʃən/ | "SKI-mờ mai-GRÂY-shần" | thay đổi cấu trúc DB | We use Flyway for schema migrations. |
| 26 | transaction | /trænˈzækʃən/ | "tren-ZÉK-shần" | giao dịch | Both updates run in one transaction. |
| 27 | ACID | /ˈæsɪd/ | "É-sid" (đọc như từ "acid") | tính chất giao dịch | We need ACID guarantees for payments. |
| 28 | eventual consistency | /ɪˈvɛntʃuəl kənˈsɪstənsi/ | "i-VÉN-chu-ồ kần-SÍS-tần-si" | nhất quán sau cùng | The read model is eventually consistent. |
| 29 | horizontal / vertical scaling | /ˌhɔːrəˈzɑːntəl/, /ˈvɝːtɪkəl/ | "ho-rơ-ZAN-tồ", "VƠ-ti-kồ" | mở rộng ngang/dọc | NoSQL databases are easier to scale horizontally. |
| 30 | vendor lock-in | /ˈvɛndər ˈlɑːkɪn/ | "VÉN-đơ LAK-in" | phụ thuộc nhà cung cấp | DynamoDB means vendor lock-in with AWS. |
| 31 | technical debt | /ˈtɛknɪkəl dɛt/ | "TÉK-ni-kồ ĐÉT" (b câm) | nợ kỹ thuật | We're paying down technical debt this quarter. |
| 32 | align / alignment | /əˈlaɪn/ | "ơ-LAIN" (g câm) | thống nhất | Let's align with the mobile team first. |
| 33 | sync up | /sɪŋk ʌp/ | "SINGK ÂP" | trao đổi nhanh | Can we sync up tomorrow? |
| 34 | circle back | /ˈsɝːkəl bæk/ | "SƠ-kồ BÉK" | quay lại chủ đề sau | Let's circle back to this next week. |
| 35 | ballpark (figure) | /ˈbɔːlpɑːrk/ | "BOL-park" | con số ước chừng | Can you give me a ballpark estimate? |
| 36 | ADR (Architecture Decision Record) | | "ây-đi-A" | ghi chép quyết định kiến trúc | Let's write an ADR for this decision. |

## 3. Mẫu câu công việc

**Mở đầu / điều phối**
1. Let's get started. The goal of this meeting is to decide ...
2. We have thirty minutes, so let's keep it focused.
3. Can everyone see my screen?
4. Let's park that for now and come back to it later.
5. We're running out of time. Let's take this offline.

**Đề xuất**
6. What if we cached the result instead of calling the API every time?
7. I'd suggest we start with a monolith and split it later.
8. One option is to use a message queue here.
9. How about adding an index on the `email` column?
10. I think it might be worth trying Redis for this.
11. My recommendation would be Postgres, because ...

**Phản đối lịch sự**
12. I have a concern about the migration time.
13. Have we considered the cost of running Kafka ourselves?
14. I see your point, but I'm worried about ...
15. That makes sense in theory, but in our case ...
16. I'm not sure that will scale. Our traffic doubles during sales.
17. I'd push back a little on that. ...
18. Could we look at this from the user's point of view?

**Đồng ý / đồng ý một phần**
19. That's a good point.
20. I agree with Linh on this.
21. I agree in principle, but we need to think about ...
22. Fair enough. Let's go with that.

**Nói về trade-off**
23. The trade-off is ... versus ...
24. On the one hand, ... On the other hand, ...
25. It's faster, but it costs more.
26. The downside is ...
27. It depends on how often the data changes.

**Hỏi lại / làm rõ**
28. Sorry, could you repeat the last part?
29. Just to make sure I understand: you mean ...?
30. What do you mean by "real-time"? Seconds or minutes?
31. Could you give an example?

**Kết thúc**
32. So, to summarize: we'll go with ..., and Nhat will write the ADR.
33. Who's going to own this?
34. What's the deadline for that?
35. I'll send a summary in Slack after the meeting.

## 4. Hội thoại mẫu

### Hội thoại 1: Chọn database cho tính năng mới

> **Tech lead (Mark):** We need to store user activity events for the new analytics page. Ideas?
> **Linh:** What if we used MongoDB? The events have different shapes, and the schema changes often.
> **Nhat:** That's a good point about flexibility. But I have a concern: we already run Postgres, and nobody on the team has operated MongoDB in production. Have we considered just using a JSONB column in Postgres?
> **Linh:** Hmm, would that scale? We're expecting maybe twenty million events a month.
> **Nhat:** Twenty million rows a month is fine for Postgres if we partition the table by month and add the right indexes. And we keep one database, one backup process, one set of tools.
> **Mark:** So the trade-off is flexibility and maybe easier scaling with Mongo, versus lower operational overhead with Postgres.
> **Nhat:** Exactly. I'd suggest we start with Postgres and set a clear limit. If we go over, say, a hundred million events, we revisit.
> **Linh:** I can live with that, as long as we measure query performance.
> **Mark:** OK, let's go with Postgres. Nhat, can you write a short ADR?
> **Nhat:** Sure, I'll share it by Thursday.

### Hội thoại 2: Có nên tách microservice?

> **Anna (PM):** The notification feature keeps breaking the main app. Should we make it a separate service?
> **Tom:** I'd say yes. If it's a separate microservice, a bug there won't take down checkout.
> **Nhat:** I see your point, but I'd push back a little. Most of the bugs are in the email templates, not in the architecture. A separate service gives us a network call, a new deployment pipeline and more monitoring.
> **Tom:** True, but the notification code also slows down our build.
> **Nhat:** That's fair. How about a middle step? We move notifications into a separate module inside the monolith, with a clear interface, and we send events through a queue. If it still causes problems, splitting it later will be easy.
> **Anna:** So, less work now, and we keep the option open?
> **Nhat:** Yes, exactly.
> **Tom:** OK, I'm fine with that. Let's circle back in two sprints.

## 5. Bài giải thích kỹ thuật mẫu

### 5.1 T4 — Monolith vs Microservices

> A monolith is an application where all the features, for example users, orders and payments, live in one codebase and are deployed as a single unit. Microservices split the system into small, independent services. Each one owns one business capability and usually its own database, and they talk to each other over the network, through REST, gRPC or messages.
>
> A monolith has real advantages. It's simple to develop, test and deploy. A function call is fast and reliable, and you can use a single database transaction across features. For a small team or a new product, it's usually the right choice.
>
> The problems appear when the system and the team grow. The codebase becomes hard to understand, builds get slow, and one bug can bring down everything. Also, you have to scale the whole application, even if only one part is busy.
>
> Microservices solve these problems. Teams can deploy their service independently, choose the right technology, and scale only the services that need it. But they come with a cost. You now have a distributed system: network calls can fail, data is spread across databases, so you often have eventual consistency instead of transactions, and you need good monitoring, tracing and automation.
>
> My view is: start with a well-structured, modular monolith. Move to microservices when you have a clear reason, such as independent scaling or several teams blocking each other, not just because it's popular.

**5 cụm từ dùng lại:**
1. *X is an application where ... live in one codebase*
2. *X has real advantages. ...*
3. *The problems appear when ...*
4. *But they come with a cost.*
5. *My view is: start with ... Move to ... when you have a clear reason.*

### 5.2 T6 — SQL vs NoSQL

> SQL databases, also called relational databases, like PostgreSQL and MySQL, store data in tables with a fixed schema. Tables are connected through relationships, and you use SQL to join them. Their biggest strength is ACID transactions: if you transfer money, either both updates happen or neither does. They are a great fit when your data is structured and consistency matters, for example orders, payments or user accounts.
>
> NoSQL is a broad name for databases that don't use the relational model. There are several types. Document databases like MongoDB store JSON-like documents. Key-value stores like Redis or DynamoDB are very fast for simple lookups. Wide-column stores like Cassandra handle huge write volumes, and graph databases like Neo4j are good for relationships, like social networks.
>
> Many NoSQL databases were designed to scale horizontally, across many machines, and they often have a flexible schema. The trade-off is that they usually give you weaker guarantees, such as eventual consistency, and fewer ways to query or join the data. You need to design your data model around your access patterns.
>
> That said, the line is not so sharp anymore. Postgres supports JSON columns, and MongoDB supports multi-document transactions.
>
> So my rule of thumb is: use a relational database by default. Choose NoSQL when you have a specific need, like massive scale, very simple key-based access or truly flexible data.

**5 cụm từ dùng lại:**
1. *X, also called Y, ...*
2. *Their biggest strength is ...*
3. *X is a broad name for ...*
4. *You need to design ... around ...*
5. *My rule of thumb is: ... by default. Choose ... when you have a specific need.*

## 6. Mẫu viết

**Tóm tắt cuộc họp (meeting notes) gửi Slack/email**

```
Subject: Notes - Analytics storage decision (Oct 14)

Attendees: Mark, Linh, Nhat
Decision: Store activity events in PostgreSQL (JSONB + monthly partitions).
Why: Lower operational overhead; current volume (~20M events/month) is fine for Postgres.
Revisit if: volume exceeds 100M events/month or p95 query time > 500 ms.

Action items:
- [Nhat] Write ADR-012 - by Thu Oct 16
- [Linh] Draft the event schema - by Fri Oct 17
- [Mark] Ask DevOps about extra disk space
```

**ADR ngắn (Architecture Decision Record)**

```
# ADR-012: Use PostgreSQL for activity events

## Status
Accepted

## Context
We need to store ~20M user activity events per month. Event shapes vary.

## Decision
Use a partitioned PostgreSQL table with a JSONB `payload` column.

## Consequences
+ One database to operate, back up and monitor.
+ The team already knows Postgres.
- Less flexible than a document database for very large volumes.
- We must manage partitions (automated with pg_partman).
```

## 7. Bài tập

1. **Biến câu "thẳng" thành câu lịch sự:** (a) "That's a bad idea." (b) "No, we can't use Kafka." (c) "You're wrong about the performance." (d) "Do it my way."
2. **Điền từ:** trade-off, bottleneck, overhead, concern, consensus.
   (a) The database is the ___; CPU is only at 20%. (b) The ___ is cost versus speed. (c) Kubernetes adds a lot of operational ___ for a team of three. (d) I think we have ___, so let's move on. (e) My only ___ is security.
3. **Đúng hay sai?** (a) Microservices always make a system faster. (b) A monolith can be modular. (c) NoSQL databases never support transactions. (d) Redis is a key-value store. (e) In a microservice architecture, each service often owns its own database.
4. **Viết 3 câu trade-off** cho: dùng managed database (AWS RDS) so với tự cài Postgres trên VM.
5. **Viết action items** (3 dòng) cho cuộc họp ở Hội thoại 2.
6. **Nói:** chọn một quyết định công nghệ thật trong dự án của bạn, trình bày 2 phút: bối cảnh, 2 lựa chọn, trade-off, quyết định cuối cùng.
7. **Nói:** giải thích Monolith vs Microservices, rồi SQL vs NoSQL, mỗi bài ≤ 3 phút, ghi âm.

## 8. Tài liệu

- [Martin Fowler — Microservices](https://martinfowler.com/articles/microservices.html) — bài kinh điển, đọc phần đầu và phần "Characteristics".
- [ByteByteGo YouTube](https://www.youtube.com/@ByteByteGo) — tìm "Monolith vs Microservices", "SQL vs NoSQL".
- [Fireship](https://www.youtube.com/@Fireship) — tìm "SQL vs NoSQL" / "7 Database Paradigms".
- [GOTO Conferences](https://www.youtube.com/@GOTO-) — có nhiều talk của Sam Newman về microservices (tìm "Sam Newman").
- [InfoQ](https://www.infoq.com) — mục *Architecture & Design*: đọc 1 bài, ghi 10 cụm từ hay.
- [roadmap.sh](https://roadmap.sh) — roadmap "Software Architect" và "Backend".

## 9. Đáp án

**Bài 1 (gợi ý):**
(a) "I'm not sure that's the best approach. Have we considered ...?"
(b) "I have a concern about using Kafka here. It might be too complex for our use case."
(c) "I see it a bit differently. In my tests, the performance was ..."
(d) "Could we try another approach? I think it might be simpler because ..."

**Bài 2:** (a) bottleneck (b) trade-off (c) overhead (d) consensus (e) concern.

**Bài 3:** (a) Sai — network calls thường làm chậm hơn; lợi ích là scale và deploy độc lập. (b) Đúng — "modular monolith". (c) Sai — ví dụ MongoDB hỗ trợ multi-document transactions. (d) Đúng. (e) Đúng — "database per service".

**Bài 4 (gợi ý):**
- A managed database is easier to operate, but it costs more.
- Self-hosting gives us more control, but we have to handle backups, upgrades and failover ourselves.
- On the one hand, RDS saves engineering time; on the other hand, it means some vendor lock-in.

**Bài 5 (gợi ý):**
```
- [Tom] Move notification code into a separate module with a clear interface
- [Nhat] Send notification events through the existing queue
- [Anna] Review the number of notification incidents in two sprints
```

**Bài 6, 7:** tự chấm: có nêu ít nhất 1 trade-off, dùng ít nhất 1 câu "softener", kết luận rõ ràng.
