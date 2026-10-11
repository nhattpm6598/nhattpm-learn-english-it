# Tuần 33 — System design (1): URL shortener, Rate limiter

> Checklist gốc: [phase-4-interview.md](../../phase-4-interview.md#tuần-33--system-design-1)

## 1. Mục tiêu tuần này

- Thuộc **khung 5 bước** trình bày system design và các cụm câu cho từng bước.
- Trình bày được **URL shortener** và **Rate limiter** trong 35–45 phút, bằng tiếng Anh.
- Luyện ngôn ngữ **trade-off**: *"The downside is...", "It depends on..."*
- **Phỏng vấn thử #5** (system design).

> System design interview không có đáp án đúng duy nhất. Interviewer chấm: bạn **hỏi requirement** tốt không, **ước lượng** hợp lý không, **thiết kế** có rõ ràng không, và **giải thích trade-off** thế nào. Với Senior, phần trade-off là quan trọng nhất.

## 2. Khung 5 bước (45 phút)

| Bước | Thời gian | Việc làm | Mẫu câu |
| --- | --- | --- | --- |
| **1. Requirements** | 5–8' | Functional (tính năng), non-functional (scale, latency, availability, consistency), ngoài phạm vi | "Before I start, I'd like to clarify the requirements." |
| **2. Estimation** | 3–5' | QPS, storage, bandwidth — tròn số | "Let me do some quick back-of-the-envelope calculations." |
| **3. High-level design** | 10' | API, data model, các khối chính, luồng request | "Let me start with a high-level design and then go deeper." |
| **4. Deep dive** | 10–15' | 1–2 phần khó nhất (interviewer thường chọn) | "The most interesting part here is... Let me go deeper." |
| **5. Trade-offs & wrap-up** | 5' | Bottleneck, failure, scaling, monitoring, cải tiến | "To wrap up, the main trade-offs are..." |

### Số liệu cần nhớ cho ước lượng

| Đại lượng | Giá trị |
| --- | --- |
| 1 ngày | ~86,400 giây ≈ **10⁵ giây** (làm tròn để dễ tính) |
| 1 triệu request/ngày | ≈ **12 QPS** |
| 100 triệu request/ngày | ≈ **1,200 QPS** |
| Peak | thường **2–3× trung bình** |
| Đọc RAM | ~100 ns · SSD random read ~100 µs · round trip cùng datacenter ~0.5 ms |
| 1 server web | ~vài nghìn QPS cho request đơn giản (tuỳ ứng dụng) |
| Redis | ~100k ops/s/node (lệnh đơn giản) |

**Đọc số tiếng Anh:** 1,200 = "twelve hundred" / "one thousand two hundred"; 10⁸ = "ten to the eighth" / "a hundred million"; 1 TB = "one terabyte"; 5 ms = "five milliseconds"; QPS = "queries per second" (đọc "Q-P-S").

## 3. Walkthrough 1: Design a URL shortener (như bit.ly)

### Bước 1 — Requirements

> "Before I start drawing, I'd like to clarify the requirements.
>
> **Functional:** a user gives us a long URL, and we return a short URL, like `sho.rt/aZ3kQ9b`. When someone opens the short URL, we redirect them to the original URL. Should users be able to choose a custom alias? … And do links expire? … Okay, let's say custom aliases are optional, and links can have an optional expiration date. Do we need analytics, like click counts? … Let's treat basic click counting as a nice-to-have.
>
> **Non-functional:** the redirect must be very fast and highly available — if redirects fail, every link on the internet that uses us is broken. Short links should not be guessable in sequence, ideally. It's a very **read-heavy** system — I'd assume about a 100 to 1 read-to-write ratio. Is that a reasonable assumption?"

### Bước 2 — Estimation

> "Let me do some quick estimates. Let's say we create **100 million new URLs per month**. That's about 40 writes per second on average — 100 million divided by roughly 2.5 million seconds in a month. With a 100 to 1 ratio, that's about **4,000 redirects per second**, maybe 10,000 at peak.
>
> Storage: each record is maybe 500 bytes — the long URL, the short code, user ID, timestamps. 100 million times 500 bytes is 50 GB per month, so about **600 GB per year**, and a few terabytes over five years. That's manageable.
>
> How long should the code be? If I use **Base62** — lowercase, uppercase, and digits — then 7 characters give 62 to the power of 7, which is about **3.5 trillion** combinations. That's more than enough for 6 billion URLs over five years."

### Bước 3 — High-level design

> "**API:**
> - `POST /api/v1/urls` with body `{ longUrl, customAlias?, expiresAt? }` → returns `{ shortUrl }`.
> - `GET /{code}` → returns an HTTP redirect.
>
> Should it be **301 or 302**? A 301 is a permanent redirect, so browsers cache it — less load on us, but we lose click tracking. A 302 is temporary, so every click comes to us. Since we want analytics, I'd use **302**, or 301 if the business doesn't care about analytics.
>
> **Data model:** one main table — `short_code` as the primary key, `long_url`, `user_id`, `created_at`, `expires_at`. The access pattern is a simple key-value lookup, so either a relational database with an index, or a key-value store like DynamoDB or Cassandra works. Given the scale, a few terabytes, I'd start with PostgreSQL and shard by short code later if needed, or go directly with a key-value store.
>
> **Components:** clients → load balancer → stateless **API service** → **cache** (Redis) → **database**. For redirects, we check Redis first; on a cache miss, we read from the database and populate the cache. Popular links follow a power-law distribution, so a cache holding the top 20 percent of links will serve most traffic."

### Bước 4 — Deep dive: generating the short code

> "The most interesting part is how to generate unique short codes. There are three main options.
>
> **Option one: hash the long URL**, for example MD5 or SHA-256, and take the first 7 characters in Base62. It's simple, but there can be **collisions**, so we'd need to check the database and retry with a salt. Also, the same long URL always gives the same code, which may or may not be what we want.
>
> **Option two: a global counter** — an auto-increment ID — converted to Base62. No collisions at all. The downsides are that the codes are **predictable** — someone can enumerate all our links — and a single counter is a bottleneck and a single point of failure.
>
> **Option three — which I'd choose — is a distributed ID approach.** For example, a **key range allocator**: each API server asks a coordination service — like ZooKeeper, or just a database table — for a range of a million IDs, then generates IDs locally from that range. That's fast and has no collisions. To avoid predictable codes, we can shuffle the bits of the ID with a reversible function before encoding to Base62. Another option is a pre-generated key service that stores unused random codes. The trade-off is a bit more complexity, but it scales horizontally and has no collision checks.
>
> For **custom aliases**, we just insert with a uniqueness constraint and return an error if it's taken."

### Bước 5 — Trade-offs & wrap-up

> "Let me cover a few more points.
> - **Analytics:** we shouldn't slow down the redirect. The API service publishes a click event to **Kafka** asynchronously, and a separate consumer aggregates the counts.
> - **Expiration:** check `expires_at` when reading, and run a background job to clean up expired links.
> - **Availability:** the API is stateless, so we scale horizontally behind the load balancer; the database is replicated, and Redis is clustered. Even if the database primary is down, redirects still work from replicas and cache — only creation is affected.
> - **Abuse:** rate limit the creation API per user and per IP, and check URLs against a malware blocklist.
>
> So to summarize: it's a read-heavy key-value system; the main decisions are the ID generation strategy, aggressive caching, and 302 versus 301 depending on whether we need analytics."

## 4. Walkthrough 2: Design a rate limiter

### Bước 1 — Requirements

> "Let me clarify a few things first. Is this a **client-side** or a **server-side** rate limiter? … Server-side, for our APIs. Do we limit by user ID, by IP, or by API key? … Let's say by user ID or API key, with different limits per plan. Is it one service or a **distributed** system with many instances? … Many instances behind a load balancer.
>
> **Non-functional:** it must add very little latency — say under a few milliseconds — because it's on every request. It must be accurate enough, but a small error is okay. And if the rate limiter itself fails, we should **fail open** — let traffic through — so we don't take down the whole API. And clients should know they're being limited: we return **HTTP 429 Too Many Requests** with headers like `Retry-After` and `X-RateLimit-Remaining`."

### Bước 2 — Estimation

> "Say we have 10 million daily active users and 50,000 requests per second at peak. Each counter in Redis takes maybe 100 bytes with overhead, so even with 10 million keys, that's only about **1 GB** of memory. 50,000 operations per second is fine for a small Redis cluster."

### Bước 3 — High-level design

> "Where should it live? We could put it in each service, or in the **API gateway**. I'd put it in the gateway — or as a middleware — so all services get it for free, and the counters are stored in a **shared Redis**, because with many gateway instances, local memory counters wouldn't be accurate.
>
> The flow is: request → gateway → rate limiter checks Redis for this key → if allowed, forward to the backend; if not, return 429. The rules — like 'free plan: 100 requests per minute' — are stored in config and cached in memory in the gateway."

### Bước 4 — Deep dive: algorithms

> "There are four common algorithms. Let me compare them.
>
> 1. **Fixed window counter** — count requests per user per minute, like key `user123:2026-10-11T10:05`, with `INCR` and `EXPIRE`. Very simple and cheap. The problem is **bursts at the window boundary**: a user can send 100 requests at 10:05:59 and 100 more at 10:06:00, so 200 in two seconds.
>
> 2. **Sliding window log** — store a timestamp for every request, for example in a Redis sorted set, and count the ones in the last 60 seconds. It's very accurate, but it uses a lot of memory for high limits.
>
> 3. **Sliding window counter** — a hybrid: use the current and previous fixed windows, and weight the previous one by how much it overlaps. For example, 30 percent into the current minute, the estimate is `current + previous × 0.7`. Low memory and quite accurate. Cloudflare has written about using this approach.
>
> 4. **Token bucket** — each user has a bucket with a maximum of N tokens, refilled at a fixed rate, say 10 tokens per second. Each request takes a token; no token, the request is rejected. It **allows short bursts** up to the bucket size but controls the average rate. It's used by many API providers, for example AWS API Gateway. There's also **leaky bucket**, which processes requests at a constant rate — good for smoothing traffic, like a queue.
>
> I'd choose **token bucket** for a public API, because allowing small bursts is user-friendly, and it only needs two values per key: the token count and the last refill timestamp."

> "**Race conditions:** if two gateway instances read the counter at the same time, both may allow the request. To avoid that, I'd make the check-and-update **atomic** by running it as a **Lua script** in Redis, which executes atomically. For the fixed window, a single `INCR` is already atomic."

### Bước 5 — Trade-offs & wrap-up

> "Some trade-offs and failure cases:
> - **Redis latency** on every request: we can keep Redis close to the gateway, in the same region. For very high scale, each gateway could keep a local counter and **sync to Redis periodically** — faster, but less accurate. It's a trade-off between accuracy and latency.
> - **Redis down:** fail open, plus a coarse local in-memory limit as a fallback, and alert on it.
> - **Multi-region:** global exact limits are expensive; usually we enforce limits per region and accept some inaccuracy.
> - **Monitoring:** track how many requests are rejected per rule, so we can see if limits are too strict.
>
> So in summary: token bucket in the API gateway, counters in Redis with atomic Lua scripts, fail open, and return 429 with clear headers."

## 5. Cụm từ hữu ích (40)

**Requirements**
1. Before I jump into the design, I'd like to clarify the requirements.
2. What are the main features we need to support?
3. Who are the users, and how many do we expect?
4. Is it more read-heavy or write-heavy?
5. What's more important here — consistency or availability?
6. What's the expected latency?
7. I'll assume ... Is that reasonable?
8. I'll leave ... out of scope for now.

**Estimation**
9. Let me do some back-of-the-envelope calculations.
10. Let's round that up to ...
11. That gives us roughly ... requests per second.
12. At peak, it could be two to three times higher.
13. Over five years, that's about ... terabytes.
14. That fits in memory / doesn't fit on a single machine.

**High-level design**
15. Let me start with a high-level design.
16. The client sends a request to ...
17. It goes through the load balancer to ...
18. This service is stateless, so we can scale it horizontally.
19. We store ... in ..., because the access pattern is ...
20. Let me define the API first.
21. The data model looks like this: ...

**Deep dive**
22. The most interesting / challenging part is ...
23. Let me go deeper into ...
24. There are a few options here. Option one is ...
25. The upside is ..., but the downside is ...
26. I'd go with ... because ...
27. To avoid a race condition, we can ...
28. This could become a bottleneck / a single point of failure.

**Trade-offs**
29. It depends on ... If ..., then I'd choose ...; otherwise ...
30. The trade-off here is between ... and ...
31. We're trading ... for ...
32. That's acceptable for this use case because ...
33. It's eventually consistent, which is fine for ...
34. It adds complexity, so I'd only do it if ...
35. A simpler alternative would be ...

**Wrap-up / interaction**
36. Does this make sense so far?
37. Which part would you like me to go deeper into?
38. If I had more time, I'd also look at ...
39. To summarize, the key design decisions are ...
40. For monitoring, I'd track ...

## 6. Lỗi người Việt hay mắc

1. **Vẽ ngay không hỏi requirement.** 5 phút đầu luôn là câu hỏi.
2. **Liệt kê công nghệ** ("We use Kafka, Redis, Kubernetes, Elasticsearch...") **không có lý do**.
3. **Không có trade-off** → nghe như học thuộc từ một video. Mỗi quyết định = 1 câu "because..." + 1 câu "the downside is...".
4. **Không giao tiếp với interviewer** — nói một mạch 20 phút. Cứ 5 phút hỏi "Does this make sense?" / "Should I go deeper here?"
5. **Ước lượng sai đơn vị** hoặc mất quá nhiều thời gian tính chính xác. Làm tròn mạnh tay.
6. **Đọc số:** "one thousand two hundred QPS" ✔; "ten power eight" ✗ → "ten to the (power of) eight"; "zero point five" ✔ for 0.5.
7. **Phát âm:** *scalability* /ˌskeɪləˈbɪləti/, *availability* /əˌveɪləˈbɪləti/, *consistency* /kənˈsɪstənsi/, *latency* /ˈleɪtənsi/, *throughput* /ˈθruːpʊt/, *shard* /ʃɑːd/, *replica* /ˈreplɪkə/, *cache* /kæʃ/, *algorithm* /ˈælɡərɪðəm/, *Base62* "base sixty-two".

## 7. Lịch luyện trong tuần

| Ngày | Việc |
| --- | --- |
| T2 | Học khung 5 bước + 40 cụm câu. Xem 1 video ByteByteGo, shadow 5 phút. |
| T3 | **URL shortener**: đọc mục 3, đóng lại, tự trình bày 30' có vẽ (Excalidraw / giấy). Ghi âm. |
| T4 | **Rate limiter**: tương tự. |
| T5 | **Phỏng vấn thử #5** (prompt mục 8). |
| T6 | Xem lại. Luyện riêng nhóm cụm trade-off (29–35): mỗi cụm đặt 2 câu về dự án của bạn. |
| T7 | Ôn + nhật ký. |

## 8. Prompt cho AI voice — Mock interview #5 (system design)

```
You are a staff engineer running a 45-minute system design interview for a
Senior Backend Engineer role. I'm a Java/Spring engineer, English B1.

The question is: "Design a URL shortener like bit.ly" (or: "Design a
distributed rate limiter for our public API" - choose one randomly).

Behave like a real interviewer:
- Start with only the one-line question. Let me ask clarifying questions and
  give realistic answers (scale, features).
- Let me lead. If I skip requirements or estimation, don't remind me - note it
  for feedback.
- After my high-level design, pick ONE area for a deep dive and challenge me
  (e.g. "What happens if Redis goes down?", "How do you avoid collisions?",
  "How does this work across multiple regions?").
- Ask at least 2 "why not X?" questions to test my trade-off thinking.

Feedback at the end:
1. Did I follow: requirements -> estimation -> high-level -> deep dive -> trade-offs?
2. Technical gaps or mistakes.
3. How well I explained trade-offs (1-5).
4. English: phrases I should use instead of the ones I used.
5. Level: junior / mid / senior based on this interview.
```

## 9. Checklist tự đánh giá

- [ ] Hỏi cả functional và non-functional requirements
- [ ] Nói ra giả định ("I'll assume...") và xin xác nhận
- [ ] Có ước lượng QPS và storage, tính nhanh, làm tròn
- [ ] Định nghĩa API và data model
- [ ] Mô tả luồng request rõ ràng
- [ ] Deep dive có **ít nhất 2 phương án** + chọn 1 có lý do
- [ ] Nói về failure (cái gì hỏng thì sao)
- [ ] Hỏi interviewer ít nhất 2 lần trong buổi ("Does this make sense?")
- [ ] Dùng ít nhất 5 cụm trade-off khác nhau
- [ ] Có tóm tắt cuối
- [ ] Đọc số đúng (QPS, GB/TB, ms)

## 10. Tài liệu tham khảo

- System Design Primer: https://github.com/donnemartin/system-design-primer
- ByteByteGo: https://bytebytego.com · YouTube: https://www.youtube.com/@ByteByteGo
- Tech Interview Handbook (system design section): https://www.techinterviewhandbook.org
