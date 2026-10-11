# Tuần 32 — Java và kiến thức nền

> Checklist gốc: [phase-4-interview.md](../../phase-4-interview.md#tuần-32--java-và-kiến-thức-nền) · Ngân hàng câu hỏi đầy đủ: [interview/question-bank.md](../../interview/question-bank.md)

## 1. Mục tiêu tuần này

- Trả lời lưu loát (1–2 phút/câu) các chủ đề: **OOP, interface vs abstract class, Collections, HashMap, Spring Boot & DI, transactions & isolation levels**.
- **Phỏng vấn thử #4** (Java).
- **Bắt đầu nhận lời mời phỏng vấn thật** từ cuối tuần.

> Bạn đã **biết** những kiến thức này bằng tiếng Việt. Tuần này là luyện **diễn đạt** chúng bằng tiếng Anh: ngắn gọn, có cấu trúc, có ví dụ.

## 2. Khung trả lời câu hỏi kỹ thuật: D-E-E-T

| Bước | Nội dung | Ví dụ câu mở |
| --- | --- | --- |
| **D – Definition** | Định nghĩa 1 câu | "In short, X is..." |
| **E – Explain** | Cách hoạt động, 2–3 ý chính | "It works like this: ..." |
| **E – Example** | Ví dụ thực tế từ dự án của bạn | "For example, in my current project, we..." |
| **T – Trade-off** | Khi nào dùng / không dùng, lưu ý | "The thing to be careful about is..." |

Câu trả lời tốt: **45–90 giây**. Sau đó dừng lại, để interviewer hỏi tiếp. Có thể kết bằng: "I can go deeper into ... if you'd like."

## 3. Model answers

### 3.1. "Explain the four principles of OOP."

> "Sure. The four main principles are encapsulation, abstraction, inheritance, and polymorphism.
>
> **Encapsulation** means keeping the data and the methods that work on that data together in a class, and hiding the internal state. For example, an `Account` class has a private `balance` field, and you can only change it through `deposit()` or `withdraw()`, which can check the rules — like not allowing a negative balance.
>
> **Abstraction** means exposing only what the user of a class needs and hiding the details. For example, a `PaymentGateway` interface has a `charge()` method, and the caller doesn't need to know if it's Stripe or a local bank behind it.
>
> **Inheritance** lets a class reuse and extend the behavior of a parent class — like `SavingsAccount extends Account`. In practice, I prefer composition over inheritance in most cases, because deep inheritance hierarchies are hard to change.
>
> And **polymorphism** means one interface, many implementations — the same method call behaves differently depending on the actual object. For example, I can have a `List<NotificationSender>` with email, SMS, and push implementations, and call `send()` on each without `if-else` checks. That's basically how Spring injects different strategy beans in our projects."

### 3.2. "What's the difference between an interface and an abstract class?"

> "Both are used for abstraction, but they have different purposes.
>
> An **abstract class** is a partial implementation. It can have state — instance fields — constructors, and both abstract and concrete methods. A class can extend only **one** abstract class. I use it when several classes share common code and state, like a `BaseEntity` with `id`, `createdAt`, and `updatedAt`.
>
> An **interface** defines a contract — what a class can do. A class can implement **many** interfaces. Since Java 8, interfaces can have `default` and `static` methods, and since Java 9, private methods, but they still can't have instance fields — only constants.
>
> So my rule of thumb is: use an interface to define a capability or a contract, like `Comparable` or a `PaymentService`, and use an abstract class when you want to share implementation between closely related classes. In Spring projects, I almost always program to interfaces, because it makes testing and swapping implementations easier."

### 3.3. "How does HashMap work internally?"

> "A `HashMap` stores key-value pairs in an array of **buckets**.
>
> When you call `put(key, value)`, it calls `key.hashCode()`, spreads the bits a little — it XORs the high bits into the low bits — and then uses the result to calculate the bucket index, basically `hash & (capacity - 1)`, because the capacity is always a power of two.
>
> If two keys land in the same bucket — that's a **collision** — the entries are stored in a linked list in that bucket. Since Java 8, if one bucket gets more than eight entries and the table has at least 64 buckets, the list is converted into a **red-black tree**, so the worst-case lookup in that bucket becomes O of log n instead of O of n.
>
> For `get()`, it finds the bucket the same way, then uses `equals()` to find the right key. That's why, if you override `equals()`, you must also override `hashCode()` consistently — otherwise you might not find your key.
>
> The default capacity is 16 and the load factor is 0.75, so when the map has more than 12 entries, it **resizes** — it doubles the array and redistributes the entries. Resizing is expensive, so if I know the size in advance, I set the initial capacity.
>
> Two more points: `HashMap` allows one null key, and it's **not thread-safe**. For concurrent access, I'd use `ConcurrentHashMap`, which uses CAS operations and locks only on individual buckets, instead of locking the whole map like `Hashtable` or `Collections.synchronizedMap`."

### 3.4. "Which collections do you use, and when?"

> "The ones I use most are `ArrayList`, `HashMap`, `HashSet`, and sometimes `LinkedHashMap`, `TreeMap`, and `ArrayDeque`.
>
> `ArrayList` is my default list — it's backed by an array, so access by index is O of one and it's cache-friendly. `LinkedList` is rarely better in practice, even for inserts, because of the overhead of nodes.
>
> `HashMap` and `HashSet` give O of one average lookup, but no ordering. If I need insertion order, I use `LinkedHashMap` — it's also useful for a simple LRU cache with `accessOrder = true` and `removeEldestEntry`. If I need sorted keys or range queries, I use `TreeMap`, which is a red-black tree, so operations are O of log n.
>
> For a queue or stack, I use `ArrayDeque`. And for concurrency, `ConcurrentHashMap` and `CopyOnWriteArrayList` for read-heavy lists, or `BlockingQueue` for producer-consumer."

### 3.5. "What is dependency injection, and how does Spring do it?"

> "Dependency injection means a class doesn't create its own dependencies — they're **given** to it from outside. It's an implementation of **inversion of control**: the framework controls object creation, not my code.
>
> In Spring, the **IoC container** — the `ApplicationContext` — scans for classes annotated with `@Component`, `@Service`, `@Repository`, or defined with `@Bean` methods in `@Configuration` classes. It creates these objects, called **beans**, resolves their dependencies, and injects them.
>
> There are three ways to inject: constructor, setter, and field injection. I always prefer **constructor injection**: dependencies can be `final`, the class can't be created in an invalid state, it's easy to unit test without Spring — I just pass mocks to the constructor — and circular dependencies fail fast at startup. With Lombok, `@RequiredArgsConstructor` makes it very short.
>
> If there are multiple beans of the same type, I use `@Qualifier` or `@Primary`. And by default beans are **singletons**, so they must be stateless or thread-safe."

### 3.6. "What does Spring Boot add on top of Spring?"

> "Spring Boot makes it much faster to build production-ready Spring applications. The main features are:
> **auto-configuration** — it configures beans automatically based on the classpath and properties, for example, if it sees a PostgreSQL driver and `spring.datasource` properties, it creates a `DataSource` with HikariCP;
> **starters**, like `spring-boot-starter-web`, which bring a consistent set of dependencies;
> an **embedded server**, so the app runs as a single jar with Tomcat inside;
> **externalized configuration** with `application.yml`, profiles, and environment variables;
> and **Actuator** for health checks and metrics, which we use with Kubernetes probes and Prometheus.
> Auto-configuration always backs off if you define your own bean, so you can override anything."

### 3.7. "How does @Transactional work? What are isolation levels?"

> "`@Transactional` is implemented with **AOP proxies**. Spring wraps the bean in a proxy; when you call a transactional method, the proxy opens a transaction, calls the method, and then commits — or rolls back if there's an exception.
>
> There are a few common traps. First, by default it only rolls back on **unchecked** exceptions — `RuntimeException` and `Error` — not on checked exceptions, unless you set `rollbackFor`. Second, **self-invocation** doesn't work: if a method calls another `@Transactional` method in the same class, the call doesn't go through the proxy, so the annotation is ignored. Third, it only applies to public methods in the classic proxy mode.
>
> **Propagation** controls what happens if a transaction already exists — the default `REQUIRED` joins it, and `REQUIRES_NEW` suspends it and starts a new one, which I've used for audit logs that must be saved even if the main transaction fails.
>
> **Isolation levels** define how much concurrent transactions can see each other's changes. There are four in the SQL standard:
> - **Read Uncommitted** — you can see uncommitted data, so *dirty reads* are possible.
> - **Read Committed** — you only see committed data, but if you read the same row twice, it may change — a *non-repeatable read*. This is the default in PostgreSQL and Oracle.
> - **Repeatable Read** — the same row returns the same value inside the transaction, but in the standard, new rows can still appear — *phantom reads*. It's the default in MySQL InnoDB, and in practice both InnoDB and PostgreSQL prevent most phantoms using snapshots.
> - **Serializable** — the strictest; transactions behave as if they ran one by one, but you get more locking or serialization failures that need retries.
>
> Higher isolation means more correctness but less concurrency. In practice, I keep Read Committed and handle specific cases with **optimistic locking** — a `@Version` column in JPA — or `SELECT ... FOR UPDATE` when I need to lock a row, for example when decreasing an account balance."

## 4. Cụm từ hữu ích (35)

| # | English | Nghĩa |
| --- | --- | --- |
| 1 | In short, ... / In simple terms, ... | Nói ngắn gọn |
| 2 | The main difference is that... | Khác biệt chính |
| 3 | It works like this: ... | Nó hoạt động thế này |
| 4 | Under the hood, ... | Bên trong, về mặt kỹ thuật |
| 5 | For example, in my current project, ... | Ví dụ trong dự án |
| 6 | My rule of thumb is... | Nguyên tắc kinh nghiệm |
| 7 | In practice, I prefer... because... | Thực tế tôi thích... |
| 8 | The thing to be careful about is... | Điều cần cẩn thận |
| 9 | A common pitfall / trap is... | Lỗi hay gặp |
| 10 | It's backed by... (an array / a tree) | Dựa trên |
| 11 | It's thread-safe / not thread-safe. | An toàn luồng |
| 12 | On average it's O of one, but in the worst case... | Trung bình / tệ nhất |
| 13 | It's a trade-off between... and... | Đánh đổi giữa |
| 14 | ...since Java 8 / as of Java 17 | Từ Java 8 |
| 15 | You must override X whenever you override Y. | Phải override cùng nhau |
| 16 | encapsulation / abstraction / inheritance / polymorphism | 4 tính chất OOP |
| 17 | favor composition over inheritance | Ưu tiên composition |
| 18 | program to an interface | Lập trình theo interface |
| 19 | inversion of control / IoC container | Đảo ngược điều khiển |
| 20 | a bean / bean scope / singleton / prototype | Bean và scope |
| 21 | constructor injection | Inject qua constructor |
| 22 | auto-configuration backs off | Tự lùi khi có bean riêng |
| 23 | It's implemented with a proxy. | Dùng proxy |
| 24 | roll back / commit | Rollback / commit |
| 25 | checked vs. unchecked exception | Ngoại lệ |
| 26 | self-invocation bypasses the proxy | Gọi nội bộ bỏ qua proxy |
| 27 | dirty read / non-repeatable read / phantom read | Hiện tượng đọc |
| 28 | optimistic vs. pessimistic locking | Khoá lạc quan / bi quan |
| 29 | race condition / deadlock | Tranh chấp / khoá chết |
| 30 | garbage collector / heap / stack | Bộ nhớ |
| 31 | immutable / mutable | Bất biến / khả biến |
| 32 | I'm not 100% sure about the exact number, but I believe it's... | Không chắc con số |
| 33 | I can go deeper into... if you'd like. | Có thể nói sâu hơn |
| 34 | That's a good question. Let me think for a second. | Câu mua thời gian |
| 35 | To summarize, ... | Tóm lại |

## 5. Lỗi người Việt hay mắc

1. **Trả lời như đọc sách giáo khoa**, không có ví dụ thực tế → interviewer nghĩ bạn học thuộc. Luôn có "In my project...".
2. **Trả lời quá ngắn:** "Interface has no implementation, abstract class has." → sai một phần (default methods) và không đủ ý.
3. **Trả lời quá dài** 5 phút cho 1 câu. 1–2 phút rồi dừng.
4. **Đoán bừa khi không chắc** → nói "I'm not 100% sure, but I believe..." tốt hơn nhiều.
5. **Phát âm:** *polymorphism* /ˌpɒliˈmɔːfɪzəm/, *inheritance* /ɪnˈherɪtəns/, *encapsulation* /ɪnˌkæpsjuˈleɪʃn/, *abstract* /ˈæbstrækt/ (tính từ), *hierarchy* /ˈhaɪərɑːki/, *isolation* /ˌaɪsəˈleɪʃn/, *transaction* /trænˈzækʃn/, *thread* /θred/ (âm θ, không phải "tờ-rét"), *synchronized* /ˈsɪŋkrənaɪzd/, *annotation* /ˌænəˈteɪʃn/, *generic* /dʒəˈnerɪk/, *bean* /biːn/.
6. **Nhầm từ:** "extend interface" (class **implements** interface, interface **extends** interface); "the bean is inject" → "the bean **is injected**".

## 6. Lịch luyện trong tuần

| Ngày | Việc |
| --- | --- |
| T2 | OOP + interface vs abstract class (3.1, 3.2). Nói theo D-E-E-T, mỗi câu 3 lần. |
| T3 | Collections + HashMap (3.3, 3.4). Vẽ bucket trên giấy khi nói. |
| T4 | Spring Boot + DI (3.5, 3.6). |
| T5 | **Phỏng vấn thử #4** (prompt mục 7). |
| T6 | Transactions + isolation (3.7). Thêm 5 câu từ [question-bank](../../interview/question-bank.md) mục Java/Spring. |
| T7 | Ôn + nhật ký. **Cập nhật CV, bắt đầu nộp hồ sơ / nhận lời mời phỏng vấn thật.** |

## 7. Prompt cho AI voice — Mock interview #4 (Java)

```
You are a senior Java engineer interviewing me for a Senior Backend Engineer
role (Java 17, Spring Boot, PostgreSQL, Kafka, microservices). My English is B1.

Run a 30-minute technical Q&A. Ask 8 questions, one at a time, mixing:
- OOP and Java core (interfaces, generics, equals/hashCode, immutability)
- Collections and HashMap internals, ConcurrentHashMap
- Java concurrency basics (threads, ExecutorService, CompletableFuture, volatile)
- Spring Boot, dependency injection, bean scopes, @Transactional pitfalls
- Transactions and isolation levels, optimistic vs pessimistic locking
- JPA: N+1 problem, lazy loading

For each answer, ask one follow-up that goes deeper (like a real interviewer
checking if I really understand). If my answer is technically wrong, say so
politely and move on - explain the correct answer only at the end.

Final feedback:
- Technical accuracy per question (correct / partly / wrong) with corrections.
- Was each answer well-structured (definition -> explanation -> example -> trade-off)?
- English: top 5 mistakes and words I mispronounced (if you can tell).
```

## 8. Checklist tự đánh giá

- [ ] Mỗi câu trả lời có cấu trúc D-E-E-T
- [ ] Mỗi câu có **ít nhất 1 ví dụ từ dự án thật**
- [ ] Thời lượng 45–90 giây/câu
- [ ] Đúng kỹ thuật (đối chiếu question-bank)
- [ ] Dùng "I'm not sure, but..." khi không chắc thay vì đoán bừa
- [ ] Phát âm đúng: polymorphism, inheritance, thread, transaction, hierarchy
- [ ] Không đọc code từng ký tự; giải thích bằng ý
- [ ] Kết thúc rõ ràng, không lửng ("...so yeah")

## 9. Tài liệu tham khảo

- Tech Interview Handbook: https://www.techinterviewhandbook.org
- System Design Primer (phần database, consistency): https://github.com/donnemartin/system-design-primer
- Levels.fyi — xem mức lương trước khi phỏng vấn thật: https://www.levels.fyi
