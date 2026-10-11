# Tuần 18 — Phát âm từ IT, đọc ký hiệu và code

> Giai đoạn 3 · Tuần 1/9 · Checklist gốc: [phase-3-it-english.md](../../phase-3-it-english.md#tuần-18--phát-âm-từ-it)

## 1. Mục tiêu tuần

Cuối tuần này bạn phải làm được:

- Đọc đúng khoảng 40 từ IT mà người Việt (và cả dev nhiều nước) hay đọc sai: *cache, queue, suite, deploy, GUI, SQL, char, null, Linux, Kubernetes, nginx, Azure, height, width...*
- Đọc to được số phiên bản (`v2.3.1`), phần trăm (`99.9%`), độ phức tạp (`O(n log n)`), URL (`/api/v1/users`) và một dòng code có ký hiệu (`!=`, `=>`, `&&`, `::`).
- Nói 2 phút không dừng về hai chủ đề: **What is an API?** và **REST vs GraphQL**.
- Giới thiệu được stack công nghệ của mình với gia sư (T5).

**Mẹo cả tuần:** tra mỗi từ trên [YouGlish](https://youglish.com) (gõ từ, chọn *US*) để nghe dev bản ngữ nói từ đó trong video thật. Đừng chỉ đọc IPA.

Ký hiệu trong bảng: chữ IN HOA = âm được nhấn. Cách đọc "dễ nhớ" chỉ là gần đúng, luôn nghe lại audio.

## 2. Từ vựng IT: 40 từ hay đọc sai

| # | Từ | IPA (Mỹ) | Cách đọc dễ nhớ | Nghĩa | Câu ví dụ |
| --- | --- | --- | --- | --- | --- |
| 1 | cache | /kæʃ/ | "KÉT-sh", giống **cash** (tiền mặt). KHÔNG đọc "ca-chê" | bộ nhớ đệm | We cache the product list in Redis for five minutes. |
| 2 | queue | /kjuː/ | "KIU", giống chữ **Q**. Bốn chữ "ueue" câm | hàng đợi | The job goes into a queue and a worker picks it up. |
| 3 | suite | /swiːt/ | "SUÍT", giống **sweet**. KHÔNG đọc "suit" | bộ (test suite) | The whole test suite takes about eight minutes. |
| 4 | deploy | /dɪˈplɔɪ/ | "đì-PLOI", nhấn âm 2 | triển khai | I'll deploy the fix to staging after lunch. |
| 5 | deployment | /dɪˈplɔɪmənt/ | "đì-PLOI-mần(t)" | bản/lần triển khai | The deployment failed because of a missing env variable. |
| 6 | GUI | /ˈɡuːi/ | "GU-i", giống **gooey**; cũng có người đánh vần G-U-I | giao diện đồ họa | It's a CLI tool, there's no GUI. |
| 7 | SQL | /ˈsiːkwəl/ hoặc /ˌɛs kjuː ˈɛl/ | "SI-quồ" (sequel) hoặc "ét-kiu-EO". Cả hai đều đúng | ngôn ngữ truy vấn | Can you share the SQL query you ran? |
| 8 | MySQL | /ˌmaɪ ˌɛs kjuː ˈɛl/ | "mai-ét-kiu-EO" (cách chính thức) | hệ CSDL | We moved from MySQL to PostgreSQL last year. |
| 9 | PostgreSQL | /ˈpoʊstɡrɛs ˌkjuː ˈɛl/ | "PÂUST-gres-kiu-EO", hay gọi tắt **Postgres** "PÂUST-gres" | hệ CSDL | Our main database is Postgres. |
| 10 | char | /tʃɑːr/ hoặc /kɛr/ | "CHA" (như **char**coal) hoặc "KE" (như **care**). Tránh "sa" | kiểu ký tự | This method returns a char, not a String. |
| 11 | null | /nʌl/ | "NÂL", âm ngắn như **nut**. KHÔNG đọc "nu-lờ" | giá trị rỗng | The API returns null when the user is not found. |
| 12 | Linux | /ˈlɪnəks/ | "LI-nợks". KHÔNG đọc "lai-nớt" | hệ điều hành | All our servers run Linux. |
| 13 | Ubuntu | /ʊˈbʊntuː/ | "u-BUN-tu" | bản phân phối Linux | The base image is Ubuntu 22.04. |
| 14 | Kubernetes | /ˌkuːbərˈnɛtiːz/ | "ku-bơ-NÉ-tiz"; viết tắt **K8s** đọc "kates" /keɪts/ | điều phối container | We run about forty services on Kubernetes. |
| 15 | nginx | /ˌɛndʒɪnˈɛks/ | "EN-gin-ÉKS" (engine-x). KHÔNG đọc "n-ginx" | web server/reverse proxy | Nginx terminates TLS and forwards traffic to the app. |
| 16 | Azure | /ˈæʒər/ | "Á-giơ" | cloud của Microsoft | The client wants everything on Azure. |
| 17 | height | /haɪt/ | "HAI-t", kết thúc bằng **t**, KHÔNG có "th" | chiều cao | Set the height of the card to auto. |
| 18 | width | /wɪdθ/ | "UÍT-th", kết thúc bằng "th" | chiều rộng | The modal width is 600 pixels on desktop. |
| 19 | Java | /ˈdʒɑːvə/ | "GIA-vờ" | ngôn ngữ Java | I've worked with Java for five years. |
| 20 | data | /ˈdeɪtə/ (hoặc /ˈdætə/) | "ĐÂY-rờ" (Mỹ hay nói "t" thành "r" nhẹ) | dữ liệu | The data is stored in S3. |
| 21 | API | /ˌeɪ piː ˈaɪ/ | "ây-pi-AI", nhấn chữ cuối | giao diện lập trình | The mobile app calls our API. |
| 22 | algorithm | /ˈælɡərɪðəm/ | "ÁL-gơ-ri-đờm" | thuật toán | The sorting algorithm runs in O(n log n). |
| 23 | architecture | /ˈɑːrkɪtɛktʃər/ | "AR-ki-tek-chơ", **ch** đầu đọc là **k** | kiến trúc | Let me walk you through the architecture. |
| 24 | parameter | /pəˈræmətər/ | "pơ-RÉ-mờ-tơ", nhấn âm 2 | tham số | This endpoint takes two query parameters. |
| 25 | variable | /ˈvɛriəbəl/ | "VE-ri-ơ-bồ" | biến | Don't use a global variable here. |
| 26 | integer | /ˈɪntɪdʒər/ | "IN-ti-giơ", **g** đọc là "gi" | số nguyên | The ID is a 64-bit integer. |
| 27 | Boolean | /ˈbuːliən/ | "BU-li-ần" | kiểu đúng/sai | It returns a Boolean: true or false. |
| 28 | async | /ˈeɪsɪŋk/ | "ÂY-sinhk" | bất đồng bộ | The email is sent async, so the user doesn't wait. |
| 29 | schema | /ˈskiːmə/ | "SKI-mờ", **ch** đọc là **k** | lược đồ | We need to change the database schema. |
| 30 | module | /ˈmɑːdʒuːl/ | "MA-giul" | mô-đun | Put this logic in the billing module. |
| 31 | JSON | /ˈdʒeɪsən/ | "GIÂY-sần", giống tên **Jason** | định dạng dữ liệu | The response body is JSON. |
| 32 | YAML | /ˈjæməl/ | "DÉ-mồ" (âm "y" như "d" nhẹ) | định dạng cấu hình | The pipeline is defined in a YAML file. |
| 33 | Redis | /ˈrɛdɪs/ | "RÉ-đis" | kho key-value trong RAM | Sessions are stored in Redis. |
| 34 | Maven | /ˈmeɪvən/ | "MÂY-vần" | công cụ build Java | Run `mvn clean install` before you push. |
| 35 | Docker | /ˈdɑːkər/ | "ĐA-kơ" | công cụ container | Each service has its own Docker image. |
| 36 | route / router | /ruːt/, /raʊt/ ; /ˈraʊtər/ | Mỹ thường nói "RAO-t", "RAO-rơ"; "RUT" cũng đúng | đường đi/bộ định tuyến | Add a new route for the settings page. |
| 37 | daemon | /ˈdiːmən/ | "ĐI-mần" | tiến trình nền | Is the Docker daemon running? |
| 38 | ASCII | /ˈæski/ | "ÁS-ki" | bảng mã ký tự | The file must contain only ASCII characters. |
| 39 | regex | /ˈrɛdʒɛks/ | "RÉ-giéks" | biểu thức chính quy | I used a regex to validate the email. |
| 40 | enum | /ˈiːnəm/ | "I-nầm" (cũng nghe "I-num") | kiểu liệt kê | Order status is an enum with five values. |

**Lỗi chung của người Việt cần sửa tuần này:**

- **Bỏ âm cuối**: *deploy-s*, *queue-s*, *test-s*, *cache-d*. Âm cuối /s/, /t/, /d/, /k/ phải nghe rõ. Ví dụ: *We **cached** it* (/kæʃt/, "két-sh-t").
- **Nhấn sai âm**: *deVELop* (không phải DEvelop), *paRAMeter*, *aRCHitecture* là AR-ki-tek-chơ.
- **Đọc từ viết tắt**: đa số đánh vần từng chữ: *A-P-I, U-R-L, C-I-C-D, J-V-M, H-T-T-P*. Một số đọc như một từ: *JSON, YAML, GUI, SaaS ("sas"), CRUD ("crăd"), WYSIWYG ("WI-zi-uig")*.

## 3. Đọc số, ký hiệu, version, URL và code

### 3.1 Ký hiệu trong code

| Ký hiệu | Cách đọc thường dùng | Ví dụ đọc to |
| --- | --- | --- |
| `=` | equals / is assigned | `x = 5` → "x equals five" |
| `==` | double equals / is equal to | `a == b` → "a double equals b" hoặc "a is equal to b" |
| `===` | triple equals (strict equals) | `a === b` → "a triple equals b" |
| `!=` | not equal (to) / bang equals | `user != null` → "user is not null" / "user not equal null" |
| `!` | not / bang | `!isValid` → "not is valid" / "bang is valid" |
| `&&` | and / double ampersand | `a && b` → "a and b" |
| `\|\|` | or / double pipe | `a \|\| b` → "a or b" |
| `=>` | arrow / fat arrow | `x => x * 2` → "x arrow x times two" |
| `->` | arrow | Java lambda `s -> s.trim()` → "s arrow s dot trim" |
| `::` | double colon | `User::getName` → "user double colon get name" (method reference) |
| `.` | dot | `user.getId()` → "user dot get I-D" |
| `()` | parentheses / parens | "open paren ... close paren" |
| `{}` | curly braces | "open curly brace" |
| `[]` | square brackets | `arr[0]` → "arr at index zero" / "arr of zero" |
| `<>` | angle brackets | `List<String>` → "list of string" |
| `;` `:` | semicolon, colon | |
| `_` | underscore | `MAX_SIZE` → "max underscore size" |
| `-` `--` | dash / hyphen, double dash | `--force` → "dash dash force" |
| `/` `\` | slash (forward slash), backslash | |
| `*` | asterisk / star / times | `SELECT *` → "select star" |
| `#` | hash / pound | `#123` → "issue one-two-three" / "hash one twenty-three" |
| `@` | at | `@Override` → "at Override" (annotation) |
| `~` `^` `\|` | tilde, caret, pipe | `cat log \| grep ERROR` → "cat log pipe grep error" |
| `%` | percent / modulo / mod | `i % 2` → "i mod two" |
| `` ` `` `'` `"` | backtick, single quote, double quote | |
| `++` `+=` | plus plus, plus equals | `i++` → "i plus plus" |
| `<=` `>=` | less than or equal to, greater than or equal to | |

### 3.2 Số, version, phần trăm, đơn vị

| Viết | Đọc |
| --- | --- |
| v2.3.1 | "version two point three point one" |
| Java 21 | "Java twenty-one" |
| Python 3.10 | "Python three point ten" (KHÔNG phải "three point one") |
| 1.0 | "one point oh" hoặc "one point zero" |
| 99.9% | "ninety-nine point nine percent" (dân ops gọi là "three nines") |
| 0.5 | "zero point five" / "point five" |
| 2026 | "twenty twenty-six" |
| 10 ms | "ten milliseconds" |
| 16 GB | "sixteen gigabytes" / "sixteen gigs" |
| 1,000 / 1,000,000 | "a thousand" / "a million"; 1.5M → "one point five million" |
| 10k RPS | "ten K requests per second" / "ten thousand R-P-S" |
| HTTP 404 | "four-oh-four"; 500 → "five hundred"; 2xx → "two hundreds" / "two-X-X" |
| 192.168.1.1 | "one ninety-two dot one sixty-eight dot one dot one" |
| localhost:8080 | "localhost colon eighty-eighty" |
| 3/4 | "three quarters" / "three out of four" |

### 3.3 Độ phức tạp (Big O)

| Viết | Đọc | Tên gọi |
| --- | --- | --- |
| O(1) | "O of one" /oʊ əv wʌn/ | constant time |
| O(log n) | "O of log n" | logarithmic |
| O(n) | "O of n" | linear |
| O(n log n) | "O of n log n" | linearithmic / "n log n" |
| O(n²) | "O of n squared" | quadratic |
| O(2ⁿ) | "O of two to the n" | exponential |

Câu mẫu: *"Binary search runs in O of log n, so it's much faster than a linear scan on large arrays."*

### 3.4 URL, đường dẫn, email

- `https://api.example.com/v1/users?id=42&sort=desc`
  → "h-t-t-p-s colon slash slash api dot example dot com slash v-one slash users, question mark, id equals forty-two, and sort equals desc."
  Khi nói chuyện thực tế, người ta bỏ phần đầu: "api dot example dot com slash v-one slash users".
- `/api/v1/users/{id}` → "slash api slash v-one slash users slash I-D" (hoặc "...users slash, then the user ID").
- `GET /orders` → "a GET request to slash orders".
- `nhat.dev@gmail.com` → "nhat dot dev at gmail dot com".
- `src/main/java` → "source main java" (src đọc là "source").

### 3.5 Đọc một dòng code

```java
if (user != null && user.isActive()) { ... }
```
"If user is not null and user dot is active, then..."

```java
List<String> names = users.stream().map(User::getName).toList();
```
"Names is a list of strings. We take users dot stream, map with user double colon get name, then to list."
(Tự nhiên hơn khi giải thích: *"We stream the users, map each one to its name, and collect them into a list."*)

```javascript
const add = (a, b) => a + b;
```
"Const add equals a, b, arrow, a plus b." → *"add is an arrow function that returns a plus b."*

**Mẹo:** khi review code với người khác, **nói ý nghĩa** chứ không đọc từng ký hiệu. Đọc từng ký hiệu chỉ cần khi đọc lệnh cho ai đó gõ.

## 4. Mẫu câu công việc

**Giới thiệu stack công nghệ**
1. I mainly work with Java and Spring Boot on the backend.
2. Our stack is Spring Boot, PostgreSQL, Redis and Kafka, running on Kubernetes.
3. On the frontend we use React with TypeScript.
4. I've been using Java for about five years, mostly Java 11 and 17.
5. We deploy to AWS using GitHub Actions and Docker.
6. I'm most comfortable with backend work, but I also do some UI.

**Hỏi lại cách đọc / chính tả**
7. Sorry, how do you pronounce that?
8. Could you spell that for me?
9. Is that "cache" with a C-A-C-H-E?
10. Do you say "S-Q-L" or "sequel" in your team?
11. Could you paste the link in the chat?
12. Sorry, was that version two point three or two point thirty?

**Đọc thông tin kỹ thuật cho người khác**
13. The endpoint is slash api slash v-one slash orders.
14. It's running on port eighty-eighty.
15. We're on version three point two point one.
16. Uptime last month was ninety-nine point nine five percent.
17. The query takes about two hundred milliseconds.
18. Let me share my screen so you can see the code.

**Giải thích khái niệm**
19. In simple terms, ...
20. The main idea is that ...
21. Think of it like a waiter in a restaurant.
22. The key difference is ...
23. For example, in our project we ...
24. That's why we use ... instead of ...
25. Does that make sense so far?
26. Let me give you a concrete example.
27. To sum up, ...

## 5. Hội thoại mẫu

### Hội thoại 1: Giới thiệu stack với đồng nghiệp mới

> **Anna (new PM):** Hi Nhat, I'm new to the team. Could you give me a quick overview of the tech stack?
> **Nhat:** Sure. The backend is a set of Spring Boot services written in Java seventeen. They talk to a PostgreSQL database, and we use Redis as a cache.
> **Anna:** Redis, is that "REE-dis" or "RED-is"?
> **Nhat:** We say "RED-is". It's an in-memory key-value store, so reads are really fast.
> **Anna:** Got it. And how do the services talk to each other?
> **Nhat:** Mostly through REST APIs. For things that don't need an immediate answer, like sending emails, we put a message on a queue, a Kafka topic, and another service processes it later.
> **Anna:** And where does everything run?
> **Nhat:** On Kubernetes in AWS. Every service is a Docker image, and we deploy with GitHub Actions. A normal deployment takes about ten minutes.
> **Anna:** That's really helpful, thanks.
> **Nhat:** No problem. I can draw a diagram for you later if you want.

### Hội thoại 2: Đọc lỗi cho đồng nghiệp qua call

> **Tom:** The build is failing on my machine. Can you read me the error?
> **Nhat:** Sure. It says: "NullPointerException at OrderService dot java, line one-forty-two."
> **Tom:** Line one-forty-two... What's on that line?
> **Nhat:** It's `order.getCustomer().getEmail()`. So order dot get customer dot get email.
> **Tom:** So the customer is null.
> **Nhat:** Probably. I think we should add a null check: if customer is not null and email is not blank, then send the email.
> **Tom:** Makes sense. Which branch are you on?
> **Nhat:** `fix slash order-email`. "fix" slash "order dash email".
> **Tom:** OK, I'll pull it and take a look.

## 6. Bài giải thích kỹ thuật mẫu

Cách luyện: (1) đọc to 3 lần, (2) shadowing cùng bản ghi âm của chính bạn hoặc TTS, (3) gấp lại, chỉ nhìn 5 cụm từ, nói lại bằng lời của mình trong 2 phút, ghi âm.

### 6.1 T4 — What is an API?

> An API, or Application Programming Interface, is a contract that lets one piece of software talk to another. It defines what you can ask for, how to ask, and what you will get back. You don't need to know how the other system works inside. You only need to follow the contract.
>
> A common analogy is a waiter in a restaurant. You, the customer, don't go into the kitchen. You look at the menu, which is like the API documentation, and you give your order to the waiter. The waiter takes it to the kitchen and brings back your food. The kitchen can change how it cooks, but as long as the menu stays the same, you are happy.
>
> In web development, when people say "API" they usually mean a web API over HTTP. For example, our mobile app sends a GET request to slash api slash v-one slash orders, and the backend returns a list of orders in JSON. The client and the server can be written in different languages, because they only share the contract.
>
> APIs are not only web APIs, though. The Java standard library is also an API: when you call `list.add()`, you use the API of the `List` interface.
>
> Good APIs are consistent, well documented and versioned, so you can change the implementation without breaking the clients that depend on them.

**5 cụm từ dùng lại:**
1. *is a contract that lets ... talk to ...*
2. *A common analogy is ...*
3. *as long as ... stays the same*
4. *When people say X, they usually mean ...*
5. *without breaking the clients that depend on them*

### 6.2 T6 — REST vs GraphQL

> REST and GraphQL are two popular ways to design an API.
>
> REST is an architectural style built around resources. Each resource has its own URL, like slash users or slash users slash forty-two, and you use HTTP methods to work with it: GET to read, POST to create, PUT or PATCH to update, and DELETE to remove. REST is simple, it works well with HTTP caching, and almost every developer understands it.
>
> The problem is that the server decides the shape of the response. Sometimes you get too much data, which we call over-fetching. Sometimes you get too little, so you need several requests to build one screen. That's under-fetching.
>
> GraphQL solves this by letting the client decide. There is usually a single endpoint, often slash graphql, and the client sends a query that describes exactly which fields it needs. For example, "give me the user's name and their last three orders with only the total price." The server returns exactly that, in one round trip. The API is described by a strongly typed schema, which gives you good tooling and auto-completion.
>
> But GraphQL has trade-offs. HTTP caching is harder because most requests are POSTs to the same URL. The server is more complex, and you have to protect it from very expensive queries and the N plus one problem.
>
> In short: REST is a great default for simple, resource-based APIs. GraphQL shines when you have many different clients, like web and mobile, that need different data from the same backend.

**5 cụm từ dùng lại:**
1. *X and Y are two popular ways to ...*
2. *X is built around ...*
3. *The problem is that ...*
4. *X solves this by letting ...*
5. *X is a great default for ..., while Y shines when ...*

## 7. Mẫu viết

**Tin nhắn Slack giới thiệu bản thân khi vào team mới**

```
Hi everyone! I'm Nhat, a backend engineer who just joined the Payments team.
I mostly work with Java/Spring Boot and PostgreSQL, and I do some React too.
Looking forward to working with you all. Feel free to ping me anytime!
```

**Ghi chú phát âm trong `log/vocabulary.md`** (mẫu để tự dùng)

```
| Word      | IPA        | I used to say | Correct     | Example sentence                    |
| queue     | /kjuː/     | "kiu-ơ"       | "kiu"       | The job is waiting in the queue.     |
```

**Commit message đầu tiên bằng tiếng Anh** (học kỹ hơn ở tuần 25)

```
fix: add null check before sending order email
```

## 8. Bài tập

1. **Phát âm:** ghi âm 40 từ ở mục 2, mỗi từ 1 lần + 1 câu ví dụ. Nghe lại, đánh dấu 5 từ bạn còn đọc sai. So với YouGlish.
2. **Chọn cách đọc đúng:** (a) suite: "suit" hay "sweet"? (b) cache: "cash" hay "catch-ay"? (c) height kết thúc bằng /t/ hay /θ/? (d) Kubernetes nhấn âm thứ mấy? (e) schema: "ch" đọc như "k" hay "ch"?
3. **Viết ra cách đọc** (bằng chữ tiếng Anh): (a) `v3.0.12` (b) `O(n²)` (c) `99.99%` (d) `GET /api/v2/products?page=3` (e) `if (count >= 10 || isAdmin)`.
4. **Đọc code:** viết câu tự nhiên giải thích dòng sau: `orders.stream().filter(o -> o.getTotal() > 100).count();`
5. **Điền từ:** (a) Our main database is ___ (Postgres / Postgre). (b) The job is waiting in the ___. (c) We ___ the fix to production yesterday. (d) Each service runs in its own ___ container.
6. **Nói:** dùng khung ở mục 6.1, giải thích "What is an API?" trong 90 giây mà không nhìn bài. Ghi âm, đếm số lần "uhm".
7. **Tự giới thiệu stack (cho buổi gia sư T5):** viết 6–8 câu về stack dự án hiện tại, dùng mẫu câu 1–6.

## 9. Tài liệu

- [Fireship](https://www.youtube.com/@Fireship) — xem các video "in 100 Seconds" (ví dụ: Kubernetes, GraphQL, Redis): nói rất nhanh, rất tốt để shadowing từng câu.
- [ByteByteGo YouTube](https://www.youtube.com/@ByteByteGo) — tìm video về REST/GraphQL/API design, giọng chậm, rõ.
- [ByteByteGo](https://bytebytego.com) — blog/hình minh họa API.
- [YouGlish](https://youglish.com) — nghe cách người bản ngữ đọc một từ trong video thật.
- [Cambridge Dictionary](https://dictionary.cambridge.org) — IPA chuẩn, nút US/UK.
- [MDN Web Docs](https://developer.mozilla.org) — tìm "HTTP request methods" và "HTTP response status codes".
- [roadmap.sh](https://roadmap.sh) — xem roadmap Backend để biết từ khóa nào cần đọc đúng.

## 10. Đáp án

**Bài 2:** (a) "sweet" /swiːt/ (b) "cash" /kæʃ/ (c) /t/ — height /haɪt/ (d) âm thứ 3: ku-ber-NE-tes (e) như "k": /ˈskiːmə/.

**Bài 3:**
(a) "version three point oh point twelve" (hoặc "three point zero point twelve").
(b) "O of n squared".
(c) "ninety-nine point nine nine percent" ("four nines").
(d) "a GET request to slash api slash v-two slash products, question mark, page equals three".
(e) "if count is greater than or equal to ten, or is admin".

**Bài 4 (gợi ý):** *"It counts how many orders have a total greater than one hundred."* Đọc ký hiệu: "orders dot stream dot filter, o arrow o dot get total greater than one hundred, dot count."

**Bài 5:** (a) Postgres (không có "Postgre") (b) queue (c) deployed — nhớ âm cuối /d/ (d) Docker.

**Bài 1, 6, 7:** không có đáp án cố định. Tiêu chí tự chấm: âm cuối rõ, nhấn đúng âm, không dừng quá 3 giây, dùng ít nhất 3 cụm từ ở mục 6.
