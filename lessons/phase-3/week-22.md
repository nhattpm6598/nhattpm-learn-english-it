# Tuần 22 — Bug và sự cố (incident)

> Giai đoạn 3 · Tuần 5/9 · Checklist gốc: [phase-3-it-english.md](../../phase-3-it-english.md#tuần-22--bug-và-sự-cố)

## 1. Mục tiêu tuần

- Mô tả bug theo cấu trúc chuẩn: **Summary → Steps to reproduce → Expected vs Actual → Environment → Root cause → Fix**.
- Kể lại một lần xử lý sự cố production trong 2–3 phút (rất hay bị hỏi khi phỏng vấn: *"Tell me about a production incident you handled."*).
- Báo cáo sự cố cho manager: bình tĩnh, ngắn gọn, nói **impact** trước, chi tiết kỹ thuật sau.
- Giải thích **Logging, monitoring, alerting** và **Java garbage collection**.

**Ngữ pháp trọng tâm: kể chuyện quá khứ**
- Quá khứ đơn cho chuỗi sự kiện: *At 2 a.m. we **got** an alert. I **checked** the logs.*
- Quá khứ tiếp diễn cho bối cảnh: *While we **were deploying**, the error rate **went up**.*
- Quá khứ hoàn thành cho việc xảy ra trước đó: *We found that someone **had changed** the config.*
- Bị động khi không cần nói ai làm: *The service **was restarted**. The fix **was deployed** at 3:10.*

## 2. Từ vựng IT

| # | Từ | IPA (Mỹ) | Cách đọc dễ nhớ | Nghĩa | Câu ví dụ |
| --- | --- | --- | --- | --- | --- |
| 1 | reproduce / repro | /ˌriːprəˈduːs/ | "ri-prơ-ĐUS", "RI-prâu" | tái hiện lỗi | I can't reproduce it on my machine. |
| 2 | steps to reproduce | | | các bước tái hiện | Please add the steps to reproduce. |
| 3 | expected behavior | /ɪkˈspɛktɪd bɪˈheɪvjər/ | "ik-SPÉK-tid bi-HÂY-viơ" | hành vi mong đợi | Expected behavior: the user sees an error message. |
| 4 | actual behavior | /ˈæktʃuəl/ | "ÉK-chu-ồ" | hành vi thực tế | Actual behavior: the page goes blank. |
| 5 | root cause | /ruːt kɔːz/ | "RUT KOZ" | nguyên nhân gốc | The root cause was a missing index. |
| 6 | workaround | /ˈwɝːkəraʊnd/ | "UƠK-ơ-raond" | cách tạm thời | As a workaround, users can refresh the page. |
| 7 | hotfix | /ˈhɑːtfɪks/ | "HAT-fiks" | bản sửa khẩn | We shipped a hotfix within an hour. |
| 8 | rollback / roll back | /ˈroʊlbæk/ | "RÂUL-bék" | quay về bản cũ | We rolled back to the previous version. |
| 9 | regression | /rɪˈɡrɛʃən/ | "ri-GRÉ-shần" | lỗi cũ quay lại / tính năng cũ hỏng | This is a regression from yesterday's release. |
| 10 | stack trace | /stæk treɪs/ | "STÉK TRÊYS" | vết ngăn xếp lỗi | Can you paste the full stack trace? |
| 11 | exception | /ɪkˈsɛpʃən/ | "ik-SÉP-shần" | ngoại lệ | It throws an `IllegalStateException`. |
| 12 | NullPointerException (NPE) | | "nâl-POIN-tơ ik-SÉP-shần", "EN-PI-I" | lỗi null | We got an NPE in the checkout flow. |
| 13 | memory leak | /ˈmɛməri liːk/ | "MÉ-mơ-ri LIK" | rò rỉ bộ nhớ | A static map caused a memory leak. |
| 14 | OutOfMemoryError (OOM) | | "ÂU-ÂU-EM" | hết bộ nhớ | The pod was killed with an OOM. |
| 15 | timeout | /ˈtaɪmaʊt/ | "TAIM-aot" | quá thời gian chờ | The payment API timed out after 30 seconds. |
| 16 | outage | /ˈaʊtɪdʒ/ | "AO-tij" | sự cố ngừng dịch vụ | We had a 40-minute outage on Monday. |
| 17 | downtime | /ˈdaʊntaɪm/ | "ĐAON-taim" | thời gian chết | The migration needs zero downtime. |
| 18 | incident | /ˈɪnsɪdənt/ | "ÍN-si-đần(t)" | sự cố | I was the incident commander. |
| 19 | severity (SEV1, SEV2) | /sɪˈvɛrəti/ | "si-VÉ-rơ-ri" | mức độ nghiêm trọng | This is a SEV2: some users are affected. |
| 20 | impact | /ˈɪmpækt/ | "ÍM-pékt" | ảnh hưởng | The impact was about 5% of orders. |
| 21 | mitigate / mitigation | /ˈmɪtɪɡeɪt/ | "MÍ-ti-gêyt" | giảm nhẹ | We mitigated it by scaling up the database. |
| 22 | escalate | /ˈɛskəleɪt/ | "ÉS-kơ-lêyt" | báo lên cấp cao hơn | If it's not fixed in 15 minutes, escalate to the lead. |
| 23 | on-call | /ˈɑːn kɔːl/ | "AN-kol" | trực sự cố | I'm on call this week. |
| 24 | postmortem | /ˌpoʊstˈmɔːrtəm/ | "pâust-MO-tầm" | báo cáo sau sự cố | We'll write a blameless postmortem. |
| 25 | blameless | /ˈbleɪmləs/ | "BLÂYM-lợs" | không đổ lỗi cá nhân | Postmortems are blameless: we fix the process. |
| 26 | SLA / SLO / SLI | | "ÉS-EL-ÂY..." | cam kết / mục tiêu / chỉ số dịch vụ | Our SLO is 99.9% availability. |
| 27 | alert | /əˈlɝːt/ | "ơ-LƠT" | cảnh báo | The alert fired at 2:13 a.m. |
| 28 | dashboard | /ˈdæʃbɔːrd/ | "ĐÉSH-bord" | bảng theo dõi | Check the Grafana dashboard. |
| 29 | metric | /ˈmɛtrɪk/ | "MÉ-trik" | chỉ số đo | CPU usage is a basic metric. |
| 30 | log level | /lɔːɡ ˈlɛvəl/ | "LOG LÉ-vồ" | mức log (ERROR, WARN, INFO, DEBUG) | Set the log level to DEBUG temporarily. |
| 31 | distributed tracing | /ˈtreɪsɪŋ/ | "TRÂY-sing" | theo vết request qua nhiều service | Tracing showed the delay was in the auth service. |
| 32 | spike | /spaɪk/ | "SPAIK" | tăng vọt | We saw a spike in 500 errors. |
| 33 | heap dump / thread dump | /hiːp dʌmp/ | "HIP ĐÂMP" | ảnh chụp bộ nhớ / luồng | I took a heap dump and analyzed it. |
| 34 | garbage collection (GC) | /ˈɡɑːrbɪdʒ kəˈlɛkʃən/ | "GA-bij kơ-LÉK-shần" | thu gom rác | Long GC pauses caused the timeouts. |
| 35 | flaky / intermittent | /ˈfleɪki/, /ˌɪntərˈmɪtənt/ | "FLÂY-ki", "in-tơ-MÍ-tần(t)" | lúc lỗi lúc không | It's an intermittent bug; it happens once a day. |
| 36 | patch | /pætʃ/ | "PÉCH" | bản vá | We applied a security patch. |
| 37 | restore (service) | /rɪˈstɔːr/ | "ri-STOR" | khôi phục | Service was restored at 3:05. |

## 3. Mẫu câu công việc

**Mô tả bug**
1. When I click "Save", nothing happens.
2. The page crashes when the cart is empty.
3. It only happens on Safari / on mobile / for new users.
4. I can reproduce it every time. / It's intermittent; about one in ten requests fails.
5. Expected: the order is saved. Actual: we get a 500 error.
6. It started after yesterday's release, so it's probably a regression.
7. Here's the stack trace and a screenshot.

**Điều tra**
8. I'm looking into it.
9. I checked the logs and found a lot of timeouts from the payment API.
10. It looks like the connection pool is exhausted.
11. I can't reproduce it locally. Can you share the request ID?
12. My guess is that ... but I need to confirm.
13. I've narrowed it down to the new caching code.

**Báo cáo trong lúc sự cố (incident call)**
14. We have an incident: checkout is failing for about 20% of users.
15. Current status: we've identified the cause and we're rolling back.
16. The rollback is done. Error rates are back to normal.
17. We're still monitoring.
18. Next update in fifteen minutes.
19. I need help from someone on the database team.

**Báo cáo cho manager (impact trước)**
20. Quick summary: between 2:10 and 2:50 a.m., about 1,200 orders failed.
21. The root cause was a configuration change that reduced the DB connection pool.
22. We mitigated it by rolling back the change.
23. No data was lost; customers can retry their orders.
24. To prevent this from happening again, we'll add an alert and a config review step.

**Kể lại sự cố (phỏng vấn)**
25. Let me tell you about an incident from last year.
26. At first, we thought it was a network problem, but ...
27. It turned out that ...
28. The lesson I learned was ...

**Giải thích root cause**
29. The root cause was ...
30. This happened because ...
31. It only showed up under high load.
32. Our tests didn't catch it because ...

## 4. Hội thoại mẫu

### Hội thoại 1: Incident call lúc nửa đêm

> **Nhat (on-call):** Hi, thanks for joining. Quick context: at 1:45 we got an alert. The error rate on the order service jumped from under one percent to about thirty percent.
> **Mai (lead):** What's the user impact?
> **Nhat:** Customers can browse, but about a third of checkouts fail with a 500 error.
> **Mai:** Any recent changes?
> **Nhat:** Yes. We deployed version 4.12 at 1:30. The logs show a lot of `SQLTransientConnectionException`, so the service can't get database connections.
> **Mai:** OK. Let's mitigate first. Can you roll back to 4.11?
> **Nhat:** Starting the rollback now. ... Done. Error rate is going down. It's back under one percent.
> **Mai:** Great. Let's keep monitoring for thirty minutes. Do we know the root cause?
> **Nhat:** Not a hundred percent yet. My guess is the new config file. I think it reduced the connection pool size from fifty to five. I'll confirm in the morning and write the postmortem.
> **Mai:** Sounds good. Please post a summary in the incident channel. Nice work.

### Hội thoại 2: Báo cáo cho manager (không chuyên kỹ thuật)

> **Manager (Kate):** I heard there was a problem last night. What happened?
> **Nhat:** Yes. From 1:45 to 2:20, about thirty percent of checkouts failed. In total, around 800 orders.
> **Kate:** Did we lose any money or data?
> **Nhat:** No data was lost. Customers saw an error and could try again. Our analytics show that about half of them retried successfully.
> **Kate:** What was the cause?
> **Nhat:** A configuration change in our release. It limited how many database connections the service could use, so under normal traffic it ran out of connections.
> **Kate:** How do we make sure it doesn't happen again?
> **Nhat:** Three things. We'll add a check in the pipeline for this setting, an alert on connection pool usage, and we'll do releases with a canary first, so only five percent of traffic hits the new version.
> **Kate:** Good. Can you send me the postmortem when it's ready?
> **Nhat:** Sure, by Thursday.

## 5. Bài giải thích kỹ thuật mẫu

### 5.1 T4 — Logging, monitoring and alerting

> Logging, monitoring and alerting work together to tell us what's happening in production.
>
> Logging means recording events from the application, for example "Order 123 created" or an exception with a stack trace. Logs have levels, like ERROR, WARN, INFO and DEBUG. Good logs are structured, usually JSON, and include context like a request ID or trace ID, so we can follow one request across services. We send them to a central place such as the ELK stack or Grafana Loki, because we can't SSH into fifty pods to read files. And we must never log passwords or personal data.
>
> Monitoring means collecting metrics, numbers over time, and showing them on dashboards. Common metrics are request rate, error rate, latency, and resource usage like CPU, memory and JVM heap. A popular setup is Prometheus with Grafana. In a microservice system we also add distributed tracing, for example with OpenTelemetry, to see where time is spent in a request.
>
> Alerting means automatically notifying a person when something is wrong, usually through PagerDuty or Slack. A good alert is actionable: it's based on symptoms that users feel, like a high error rate or slow responses, not on every small CPU spike. Too many noisy alerts cause alert fatigue, and then people start ignoring them.
>
> In short: logs tell you **why** something happened, metrics tell you **what** is happening, and alerts tell you **when** you need to act.

**5 cụm từ dùng lại:**
1. *X, Y and Z work together to ...*
2. *X means recording / collecting ...*
3. *A good alert is actionable: ...*
4. *We can't ..., so we ...*
5. *In short: X tells you why, Y tells you what, and Z tells you when.*

### 5.2 T6 — How does garbage collection work in Java?

> In Java, we create objects with `new`, but we never free memory ourselves. The garbage collector, or GC, does it for us. It finds objects that are no longer reachable and reclaims their memory.
>
> How does it know an object is garbage? It starts from GC roots, such as local variables on thread stacks and static fields, and follows every reference. Any object it can reach is alive. Everything else can be collected, even objects that point to each other in a cycle.
>
> Most JVM collectors are generational, because most objects die young. New objects are created in the young generation, in an area called Eden. When Eden fills up, a minor GC runs: live objects are copied to a survivor space, and after surviving several collections they are promoted to the old generation. Minor GCs are frequent and fast. Collecting the old generation is more expensive.
>
> Some phases of GC are "stop-the-world": all application threads pause. That's why the choice of collector matters. Since Java 9, the default is G1, which splits the heap into regions and tries to meet a pause-time goal. For very low latency, there are ZGC and Shenandoah, which do most of the work concurrently and keep pauses very short, usually around a millisecond or less.
>
> One important point: GC doesn't prevent memory leaks. If you keep references you don't need, for example in a static map that keeps growing, those objects stay reachable, and you can still get an `OutOfMemoryError`.

**5 cụm từ dùng lại:**
1. *X does it for us.*
2. *How does it know ...? It starts from ...*
3. *X is ... because most ...*
4. *That's why ... matters.*
5. *One important point: X doesn't prevent ...*

## 6. Mẫu viết

**Bug report (Jira/GitHub issue)**

```
Title: Checkout returns 500 when the cart contains a discounted item

Environment: Production, web, Chrome 129 / Safari 18. Version 4.12.0
Severity: High - blocks purchases for some users

Steps to reproduce:
1. Log in as a regular customer.
2. Add any item with an active discount to the cart.
3. Click "Checkout", then "Pay now".

Expected result: The order is created and the payment page opens.
Actual result:   A "Something went wrong" page. API returns HTTP 500.

Logs / evidence: Request ID 7f3a-...; stack trace attached (NullPointerException
in DiscountCalculator.apply, line 87). Screenshot attached.

Frequency: 100% reproducible with discounted items.
Notes: Started after release 4.12.0 (regression).
```

**Cập nhật trạng thái sự cố (Slack #incident)**

```
[SEV2] Checkout errors - UPDATE 2 (02:05)
Impact: ~30% of checkouts failing since 01:45.
Status: Cause identified (DB connection pool config in v4.12). Rollback to v4.11 in progress.
Next update: 02:20 or earlier if anything changes.
```

**Postmortem rút gọn**

```
# Postmortem: Checkout failures on Oct 20

Summary:     From 01:45 to 02:20 (35 min), ~30% of checkouts failed. ~800 orders affected.
Root cause:  v4.12 included a config change that reduced the DB pool size from 50 to 5.
Detection:   Error-rate alert fired at 01:47 (2 min after the deployment).
Mitigation:  Rolled back to v4.11 at 02:12. Recovered fully at 02:20.
What went well:   Alert fired quickly; rollback took under 10 minutes.
What went wrong:  The config change was not reviewed; no alert on pool usage.
Action items:
  - Add validation for pool size in CI (owner: Nhat, due Oct 27)
  - Alert when pool usage > 80% for 5 min (owner: Mai, due Oct 25)
  - Introduce canary releases (owner: Platform team, due Nov 15)
```

## 7. Bài tập

1. **Sắp xếp** các phần của bug report theo đúng thứ tự: Actual result, Title, Steps to reproduce, Environment, Expected result.
2. **Chia động từ (kể chuyện):** "At 2 a.m. we (get) ___ an alert. While I (check) ___ the logs, the database CPU (go) ___ up to 100%. We later found that a new query (be) ___ deployed the day before without an index."
3. **Viết lại cho manager** (bỏ thuật ngữ, nói impact trước): "HikariCP pool exhausted due to maxPoolSize=5 in v4.12, causing SQLTransientConnectionException and 500s on /checkout."
4. **Ghép:** (a) workaround (b) rollback (c) root cause (d) mitigate (e) regression — (1) quay về phiên bản trước (2) lý do sâu xa (3) tính năng từng chạy giờ hỏng (4) cách tạm để người dùng vẫn làm được việc (5) giảm ảnh hưởng.
5. **Đúng hay sai?** (a) Java GC can collect two objects that reference each other if nothing else references them. (b) GC makes memory leaks impossible in Java. (c) Minor GCs collect the young generation. (d) G1 has been the default collector since Java 9.
6. **Viết bug report** cho một bug thật bạn đã sửa gần đây, theo mẫu mục 6.
7. **Nói (T3):** kể một sự cố production bạn từng xử lý, 2–3 phút, theo khung: *Context → Impact → What I did → Root cause → Fix → Lesson.*
8. **Nói:** giải thích logging/monitoring/alerting và Java GC, mỗi bài ≤ 3 phút.

## 8. Tài liệu

- [Google SRE Books](https://sre.google/books/) — đọc miễn phí online; chương về *Monitoring Distributed Systems* và *Postmortem Culture* rất hay cho từ vựng sự cố.
- [ByteByteGo YouTube](https://www.youtube.com/@ByteByteGo) — tìm "logging tracing metrics".
- [Fireship](https://www.youtube.com/@Fireship) — tìm "garbage collection".
- [GOTO Conferences](https://www.youtube.com/@GOTO-) và [InfoQ](https://www.infoq.com) — tìm "observability", "Java GC", "ZGC".
- [Oracle Java documentation](https://docs.oracle.com/javase/tutorial/) — trang chủ tutorial; tìm thêm tài liệu "HotSpot GC tuning guide" cho phiên bản Java bạn dùng.

## 9. Đáp án

**Bài 1:** Title → Environment → Steps to reproduce → Expected result → Actual result.

**Bài 2:** got · was checking · went · had been deployed.

**Bài 3 (gợi ý):** "Checkout was failing for some customers because the service couldn't connect to the database. A setting in the new release limited the number of connections too much. We rolled it back and everything is working again."

**Bài 4:** a-4, b-1, c-2, d-5, e-3.

**Bài 5:** (a) Đúng — GC dùng reachability từ GC roots, không đếm reference. (b) Sai — vẫn leak nếu giữ reference không cần thiết. (c) Đúng. (d) Đúng (JEP 248, Java 9).

**Bài 6–8:** tự chấm: có số liệu cụ thể (thời gian, % người dùng), có root cause và action item, dùng đúng thì quá khứ.
