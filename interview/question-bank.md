# Interview Question Bank

Ngân hàng ~100 câu hỏi phỏng vấn thường gặp cho **Medior/Senior Software Engineer (Java/Spring, microservices, có frontend)**, kèm câu trả lời mẫu ngắn gọn bằng tiếng Anh và từ vựng tiếng Việt.

**Cách dùng:**
- Đây là câu trả lời **ngắn** (2–6 câu) để nắm ý. Trong phỏng vấn thật, mở rộng thành 45–90 giây bằng **ví dụ từ dự án của bạn** (khung D-E-E-T ở [week-32](../lessons/phase-4/week-32.md)).
- Mỗi ngày chọn 3–5 câu: đọc đáp án, **đóng lại**, tự nói, ghi âm, so sánh.
- Câu hỏi hành vi chi tiết hơn: xem [lessons/phase-4](../lessons/phase-4/README.md) tuần 27–30. Cụm từ: [phrasebook.md](phrasebook.md).

## Mục lục

1. [HR / Behavioral](#1-hr--behavioral) (Q1–Q15)
2. [Java core](#2-java-core) (Q16–Q32)
3. [Spring / Spring Boot](#3-spring--spring-boot) (Q33–Q45)
4. [Databases / SQL](#4-databases--sql) (Q46–Q58)
5. [Microservices & distributed systems](#5-microservices--distributed-systems) (Q59–Q73)
6. [Frontend / UI basics](#6-frontend--ui-basics) (Q74–Q83)
7. [System design](#7-system-design) (Q84–Q91)
8. [DevOps / Cloud basics](#8-devops--cloud-basics) (Q92–Q101)
9. [Questions to ask the interviewer](#9-questions-to-ask-the-interviewer) (Q102–Q110)

---

## 1. HR / Behavioral

> Câu trả lời đầy đủ: [week-27](../lessons/phase-4/week-27.md), [week-29](../lessons/phase-4/week-29.md), [week-30](../lessons/phase-4/week-30.md), [week-35](../lessons/phase-4/week-35.md).

**Q1. Tell me about yourself.**
> Use Present → Past → Future. "I'm a backend engineer with six years of experience, mainly in Java and Spring Boot. Currently I work on a payment platform at a fintech company… One thing I'm proud of is… Now I'm looking for a role in an international team where I can work on larger-scale systems."

**Q2. Why are you looking for a new job?**
> Positive and forward-looking. "I've learned a lot at my current company, but the product is now stable and mostly in maintenance. I'm looking for bigger technical challenges and an international environment."

**Q3. Why do you want to work here?**
> Three specific reasons: product, technology, culture. Mention something concrete from their website, engineering blog, or job description.

**Q4. Tell me about a project you're proud of.**
> Context → Problem → My role → Solution (with trade-offs) → Result (numbers) → Reflection. 2–3 minutes.

**Q5. Tell me about a time you disagreed with a teammate.**
> STAR. Show that you listened first, used data instead of opinions, found a compromise, and kept a good relationship.

**Q6. Tell me about a mistake you made.**
> A real but not catastrophic mistake. Own it ("I made a mistake"), explain how you fixed it quickly, and what process you changed so it doesn't happen again.

**Q7. Tell me about a time you worked under a tight deadline.**
> Show prioritization: clarify the real minimum scope, negotiate, split work, communicate progress, deliver.

**Q8. Tell me about a time you mentored someone.**
> Concrete actions (1-on-1s, pairing, review style) and a measurable result (fewer review comments, faster onboarding, they now mentor others).

**Q9. Tell me about a difficult technical decision.**
> Options considered, criteria (complexity, cost, team skills, requirements), the decision and why, and how it turned out.

**Q10. Tell me about a production incident you handled.**
> Detect → communicate → mitigate first (rollback, feature flag) → root cause → blameless post-mortem → action items.

**Q11. What are your strengths?**
> 2–3 strengths relevant to the job, each with a short example. E.g. "debugging production issues", "communicating with non-technical people", "learning quickly".

**Q12. What is your biggest weakness?**
> A real weakness that isn't core to the job + what you're doing about it + progress. E.g. spoken English, delegating, public speaking.

**Q13. Where do you see yourself in five years?**
> "Growing into a staff engineer or tech lead role — designing systems across teams and mentoring others — ideally here."

**Q14. Tell me about a time you had to work with unclear requirements.**
> "I listed my assumptions, asked the product manager specific questions, built a small prototype to get feedback early, and wrote down the agreed decisions in the ticket so everyone was aligned."
> *ambiguity* = sự mơ hồ; *assumption* = giả định; *aligned* = thống nhất.

**Q15. How do you handle feedback or criticism?**
> "I try not to take it personally — feedback on my code isn't feedback on me. I ask questions to understand the reason, and if I agree, I apply it and thank the person. If I disagree, I explain my reasoning with data and we decide together. For example, a reviewer once pointed out that my caching approach could serve stale prices; he was right, and I changed it."

---

## 2. Java core

**Q16. What are the four principles of OOP?**
> Encapsulation (hide internal state behind methods), abstraction (expose only what's necessary), inheritance (reuse/extend a parent class), polymorphism (one interface, many implementations — the actual object decides which method runs). In practice, I favor composition over inheritance.
> *encapsulation* = đóng gói; *inheritance* = kế thừa; *polymorphism* = đa hình.

**Q17. Interface vs. abstract class?**
> An abstract class can have state, constructors, and concrete methods; a class can extend only one. An interface defines a contract; a class can implement many, and since Java 8 interfaces can have default and static methods, but no instance fields. Use interfaces for capabilities/contracts, abstract classes to share code between closely related classes.

**Q18. Why must you override `hashCode()` when you override `equals()`?**
> Hash-based collections like `HashMap` first use `hashCode()` to find the bucket, then `equals()` to find the key. The contract says equal objects must have equal hash codes. If you only override `equals()`, two equal objects may land in different buckets, so `map.get()` won't find your key.

**Q19. How does `HashMap` work internally?**
> An array of buckets. The key's hash (with high bits spread into low bits) determines the bucket index. Collisions are stored in a linked list, which becomes a red-black tree when a bucket has more than 8 entries (and capacity ≥ 64). Default capacity 16, load factor 0.75; when size exceeds capacity × load factor, it doubles and rehashes. Not thread-safe; allows one null key.
> *bucket* = ngăn; *collision* = va chạm; *load factor* = hệ số tải.

**Q20. `HashMap` vs. `ConcurrentHashMap` vs. `Hashtable`?**
> `HashMap` is not thread-safe. `Hashtable` is synchronized on every method — thread-safe but slow, and considered legacy. `ConcurrentHashMap` is thread-safe with fine-grained locking (CAS and per-bin locks since Java 8), so reads are mostly lock-free and concurrent writes to different bins don't block each other. It doesn't allow null keys or values.

**Q21. `ArrayList` vs. `LinkedList`?**
> `ArrayList` is backed by a resizable array: O(1) random access, amortized O(1) append, O(n) insert in the middle. `LinkedList` is a doubly linked list: O(1) insert/remove at a known node, but O(n) access by index and more memory per element. In practice, `ArrayList` is almost always faster because of CPU cache locality.

**Q22. What does `final` mean in Java? Is a `final` list immutable?**
> A `final` variable can't be reassigned, a `final` method can't be overridden, and a `final` class can't be extended. But a `final List` only means the reference can't change — you can still add elements. For real immutability, use `List.of()` or `Collections.unmodifiableList()`, and immutable element types.

**Q23. Why is `String` immutable?**
> Security (strings are used for class names, file paths, URLs), thread safety without synchronization, caching of the hash code (good for `HashMap` keys), and the string pool — literals can be shared safely. The downside is that repeated concatenation in a loop creates many objects, so we use `StringBuilder`.

**Q24. Checked vs. unchecked exceptions?**
> Checked exceptions (subclasses of `Exception` but not `RuntimeException`, e.g. `IOException`) must be declared or caught — the compiler enforces it. Unchecked exceptions (`RuntimeException` and subclasses, e.g. `NullPointerException`, `IllegalArgumentException`) don't. Modern frameworks like Spring mostly use unchecked exceptions; I use checked ones only when the caller can realistically recover.

**Q25. Explain the Java memory model: heap vs. stack.**
> Each thread has its own stack, which stores method frames, local primitive variables, and references. Objects live on the heap, shared by all threads and managed by the garbage collector. Metaspace (since Java 8) stores class metadata. A `StackOverflowError` usually means too-deep recursion; `OutOfMemoryError: Java heap space` means the heap is full — often a memory leak or too-small `-Xmx`.

**Q26. How does garbage collection work?**
> The JVM automatically frees objects that are no longer reachable from GC roots (thread stacks, static fields). Most collectors are generational: most objects die young, so the young generation is collected often and cheaply, and survivors are promoted to the old generation. G1 is the default since Java 9; it splits the heap into regions and targets a pause-time goal. ZGC and Shenandoah offer very low pause times for large heaps.

**Q27. What is `volatile`? How is it different from `synchronized`?**
> `volatile` guarantees visibility — a write by one thread is immediately visible to others — and prevents certain reorderings, but it doesn't make compound actions like `count++` atomic. `synchronized` provides both mutual exclusion and visibility. For simple counters, I'd use `AtomicInteger` or `LongAdder`.
> *visibility* = khả năng nhìn thấy (giữa các luồng); *atomic* = nguyên tử, không bị chia cắt.

**Q28. How do you create and manage threads in modern Java?**
> I rarely create threads directly. I use an `ExecutorService` (thread pool) to control concurrency, `CompletableFuture` to compose async tasks, and in Java 21, virtual threads for high-concurrency I/O-bound work (`Executors.newVirtualThreadPerTaskExecutor()`). In Spring, `@Async` with a configured executor.

**Q29. What is a deadlock, and how do you prevent it?**
> Two or more threads each hold a lock and wait for a lock the other holds, so none can continue. Prevent it by always acquiring locks in the same order, using timeouts (`tryLock`), holding locks for as short a time as possible, or avoiding shared mutable state. In databases, the same idea applies — and the DB will detect deadlocks and abort one transaction, so we need retries.

**Q30. What's new in recent Java versions that you actually use?**
> Java 8: lambdas, streams, `Optional`, `java.time`. Java 11: `var` in lambdas, the new HTTP client. Java 14–17: switch expressions, records, text blocks, sealed classes, pattern matching for `instanceof`. Java 21: virtual threads, pattern matching for switch, record patterns, sequenced collections. I use records a lot for DTOs.

**Q31. What are streams? Any pitfalls?**
> The Stream API lets you process collections declaratively with `map`, `filter`, `collect`, etc. Streams are lazy — nothing runs until a terminal operation. Pitfalls: a stream can be consumed only once; side effects inside lambdas make code hard to reason about; `parallelStream()` uses the common ForkJoinPool and isn't always faster — I avoid it in web servers; and complex chains can be less readable than a simple loop.

**Q32. What is `Optional` for, and how should you not use it?**
> `Optional` represents a value that may be absent, mainly as a method return type, to make "no result" explicit and avoid `NullPointerException`. Don't use it for fields, method parameters, or collections (return an empty list instead), and avoid calling `get()` without checking — use `orElse`, `orElseThrow`, `map`.

---

## 3. Spring / Spring Boot

**Q33. What is dependency injection / inversion of control?**
> IoC means the framework creates and wires objects instead of my code. DI is how it's done: dependencies are passed in (usually through the constructor) instead of created with `new`. This makes code loosely coupled and easy to test with mocks.
> *loosely coupled* = liên kết lỏng.

**Q34. Constructor vs. field vs. setter injection?**
> I prefer constructor injection: fields can be `final`, dependencies are explicit, the object is always fully initialized, and it's easy to test without Spring. Setter injection is for optional dependencies. Field injection (`@Autowired` on a field) hides dependencies and makes testing harder.

**Q35. What are bean scopes?**
> Singleton (default — one instance per container), prototype (new instance each time it's requested), and in web apps: request, session, application, websocket. Singletons must be stateless or thread-safe, because many requests use them at the same time.

**Q36. Explain the Spring bean lifecycle briefly.**
> Instantiate → inject dependencies → `Aware` callbacks → `BeanPostProcessor` before-init → init (`@PostConstruct`, `afterPropertiesSet`) → `BeanPostProcessor` after-init (this is where AOP proxies are created) → bean in use → on shutdown, `@PreDestroy`.

**Q37. How does Spring Boot auto-configuration work?**
> Boot loads auto-configuration classes listed in `META-INF/spring/...AutoConfiguration.imports` (older versions used `spring.factories`). Each one is guarded by conditions like `@ConditionalOnClass`, `@ConditionalOnProperty`, and `@ConditionalOnMissingBean`. So if a library is on the classpath and you haven't defined your own bean, Boot configures a sensible default. You can see decisions with `--debug` (the conditions report).

**Q38. `@Component` vs. `@Service` vs. `@Repository` vs. `@Controller`?**
> All are stereotypes detected by component scanning. `@Service` and `@Component` are functionally the same — `@Service` documents intent. `@Repository` also enables translation of persistence exceptions into Spring's `DataAccessException`. `@Controller`/`@RestController` mark web handlers; `@RestController` = `@Controller` + `@ResponseBody`.

**Q39. How does `@Transactional` work, and what are its pitfalls?**
> It's implemented with AOP proxies: the proxy starts a transaction, calls the method, and commits or rolls back. Pitfalls: by default it only rolls back on unchecked exceptions; self-invocation (calling a transactional method from the same class) bypasses the proxy; it should be on public methods; and long transactions holding connections while calling external APIs can exhaust the pool.

**Q40. Explain transaction propagation `REQUIRED` vs. `REQUIRES_NEW`.**
> `REQUIRED` (default) joins an existing transaction or creates one. `REQUIRES_NEW` always suspends the current transaction and starts a new, independent one — useful for audit logs that must be saved even if the outer transaction rolls back. Be careful: it uses a second DB connection.

**Q41. What is the N+1 problem in JPA/Hibernate, and how do you fix it?**
> Loading a list of N entities with 1 query, then a lazy association triggers 1 extra query per entity — N+1 queries total. Fix with `JOIN FETCH` in JPQL, `@EntityGraph`, batch fetching (`@BatchSize` / `hibernate.default_batch_fetch_size`), or a DTO projection query. I detect it by enabling SQL logging or using query count assertions in tests.

**Q42. Lazy vs. eager loading?**
> Lazy loads an association only when accessed; eager loads it immediately. Default: `@ManyToOne`/`@OneToOne` are eager, `@OneToMany`/`@ManyToMany` are lazy. I make almost everything lazy and fetch explicitly per use case. Accessing a lazy field outside a transaction causes `LazyInitializationException`; I'd also disable `spring.jpa.open-in-view` so it doesn't hide these issues.

**Q43. How do you handle exceptions globally in a Spring REST API?**
> With `@RestControllerAdvice` and `@ExceptionHandler` methods that map exceptions to HTTP status codes and a consistent error body — ideally `ProblemDetail` (RFC 9457 / formerly 7807), supported since Spring Boot 3. For example, validation errors → 400, not found → 404, and unexpected errors → 500 with a generic message, while logging the details.

**Q44. How do you secure a Spring Boot REST API?**
> Spring Security with a `SecurityFilterChain`. For stateless APIs, typically OAuth2 / JWT: configure the app as a resource server that validates tokens issued by an identity provider (Keycloak, Auth0, Cognito). Use method security (`@PreAuthorize`) for fine-grained rules, HTTPS everywhere, CORS configured explicitly, and input validation with `@Valid`.

**Q45. How do you test a Spring Boot application?**
> Unit tests with JUnit 5 and Mockito for services, without Spring. Slice tests: `@WebMvcTest` for controllers with `MockMvc`, `@DataJpaTest` for repositories. Integration tests with `@SpringBootTest` and Testcontainers for real PostgreSQL/Kafka. Contract tests between services if needed. Most tests should be fast unit tests — the testing pyramid.

---

## 4. Databases / SQL

**Q46. What is an index, and how does it work?**
> A data structure — usually a B-tree (B+tree) — that lets the database find rows without scanning the whole table: O(log n) instead of O(n). The trade-off: indexes use storage and slow down inserts/updates, because every index must be updated.

**Q47. How does a composite index work? Does column order matter?**
> Yes. An index on `(user_id, created_at)` is sorted by `user_id` first, then `created_at`. It helps queries filtering on `user_id`, or on `user_id` and `created_at`, but generally not queries filtering only on `created_at` — the leftmost-prefix rule. Put equality columns first, then range/sort columns.

**Q48. How do you find and fix a slow query?**
> Find it via slow query logs, `pg_stat_statements`, or APM. Run `EXPLAIN ANALYZE` to see the plan — look for sequential scans on big tables, bad row estimates, expensive sorts. Fixes: add or adjust indexes, rewrite the query, avoid `SELECT *`, use keyset pagination instead of large `OFFSET`, update statistics, or cache/denormalize if needed.

**Q49. What are ACID properties?**
> Atomicity (all or nothing), Consistency (constraints are always valid), Isolation (concurrent transactions don't interfere, per the isolation level), Durability (once committed, data survives crashes — via the write-ahead log).

**Q50. Explain the isolation levels and read phenomena.**
> Read Uncommitted (dirty reads possible), Read Committed (no dirty reads, but non-repeatable reads), Repeatable Read (no non-repeatable reads; phantoms possible in the standard), Serializable (as if transactions ran one at a time). PostgreSQL and Oracle default to Read Committed; MySQL InnoDB to Repeatable Read. Higher isolation = more correctness, less concurrency.

**Q51. Optimistic vs. pessimistic locking?**
> Pessimistic: lock the row when reading (`SELECT ... FOR UPDATE`) so others wait — good for high contention. Optimistic: no lock; a version column is checked on update (`UPDATE ... WHERE id = ? AND version = ?`), and if 0 rows are updated, someone else changed it, so you retry or fail. JPA supports it with `@Version`. Optimistic is better when conflicts are rare.

**Q52. `INNER JOIN` vs. `LEFT JOIN`?**
> `INNER JOIN` returns only rows that match in both tables. `LEFT JOIN` returns all rows from the left table, with NULLs for the right side when there's no match. Example: all customers and their orders, including customers with no orders → `LEFT JOIN`.

**Q53. `WHERE` vs. `HAVING`?**
> `WHERE` filters rows before grouping; `HAVING` filters groups after `GROUP BY`, so it can use aggregates. E.g. `SELECT user_id, COUNT(*) FROM orders WHERE status = 'PAID' GROUP BY user_id HAVING COUNT(*) > 5`.

**Q54. Write a query to find the second-highest salary.**
> `SELECT MAX(salary) FROM employees WHERE salary < (SELECT MAX(salary) FROM employees);` Or with window functions: `SELECT DISTINCT salary FROM (SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk FROM employees) t WHERE rnk = 2;` — `DENSE_RANK` handles ties correctly.

**Q55. What is normalization? When would you denormalize?**
> Normalization organizes data to reduce duplication — e.g. 3NF: every non-key column depends on the key, the whole key, and nothing but the key. It keeps writes consistent. Denormalize for read performance — e.g. storing a precomputed `order_total` or a read model — accepting extra work to keep copies in sync.

**Q56. SQL vs. NoSQL — how do you choose?**
> SQL (PostgreSQL, MySQL): structured data, relationships, transactions, flexible queries — my default. NoSQL: key-value (Redis, DynamoDB) for simple fast lookups; document (MongoDB) for flexible schemas; wide-column (Cassandra) for huge write volumes with known access patterns; graph DBs for relationships. Choose by access patterns, consistency needs, and scale — not by hype.

**Q57. What is database replication and sharding?**
> Replication copies data to replicas — for read scaling and high availability; with async replication, replicas can lag. Sharding (partitioning) splits data across multiple databases by a shard key (e.g. `user_id`) — for write and storage scaling. Sharding adds complexity: cross-shard queries and transactions, rebalancing, and hot shards.
> *replication lag* = độ trễ đồng bộ; *shard key* = khoá phân mảnh.

**Q58. What is a connection pool, and why does it matter?**
> Opening a DB connection is expensive, so a pool (HikariCP in Spring Boot) keeps connections open and reuses them. Pool size matters: too small → requests wait; too large → the database is overloaded. With many service instances, total connections = instances × pool size, which can exceed the DB's limit. Monitor active/pending connections.

---

## 5. Microservices & distributed systems

**Q59. Monolith vs. microservices — when would you choose each?**
> A monolith is simpler to develop, test, deploy, and debug — great for small teams and early products. Microservices allow independent deployment and scaling, and team autonomy, but add network failures, distributed data, and operational overhead. I'd start with a well-structured modular monolith and extract services when there's a clear reason: team size, scaling needs, or different release cycles.

**Q60. How do microservices communicate?**
> Synchronously (REST, gRPC) — simple, request-response, but creates temporal coupling: if B is down, A fails. Asynchronously (Kafka, RabbitMQ events) — decoupled and resilient, but eventually consistent and harder to debug. I use sync for queries that need an immediate answer and async for events and side effects.

**Q61. What is the CAP theorem?**
> In a distributed system, during a network partition you must choose between consistency (every read sees the latest write) and availability (every request gets a response). Since partitions happen, the real choice is CP or AP during failures. PACELC extends it: else (no partition), you trade latency vs. consistency.

**Q62. How do you handle transactions across microservices?**
> Avoid distributed transactions (2PC) — they're slow and fragile. Use the Saga pattern: a sequence of local transactions, each publishing an event; if a step fails, run compensating actions (e.g. refund payment, release inventory). Sagas can be choreographed (services react to events) or orchestrated (a coordinator tells each service what to do).

**Q63. What is the transactional outbox pattern?**
> Problem: you need to update the DB and publish an event atomically — if you do both separately, one can fail (dual-write problem). Solution: in the same local transaction, write the business data and an event row into an `outbox` table. A separate process (a poller or CDC like Debezium) reads the outbox and publishes to Kafka. Delivery becomes at-least-once, so consumers must be idempotent.

**Q64. What does idempotency mean, and why is it important?**
> An operation is idempotent if doing it multiple times has the same effect as doing it once. Networks cause retries and message brokers deliver at-least-once, so duplicates happen. We make APIs idempotent with idempotency keys and consumers idempotent by tracking processed message IDs or using upserts. HTTP GET, PUT, DELETE are idempotent by definition; POST is not.

**Q65. Explain the circuit breaker pattern.**
> It stops calling a failing dependency to avoid cascading failures. States: closed (normal), open (fail fast after failures exceed a threshold), half-open (allow a few test calls; if they succeed, close again). In Java I use Resilience4j, combined with timeouts, retries with backoff, bulkheads, and fallbacks.

**Q66. What is an API gateway?**
> A single entry point in front of services that handles cross-cutting concerns: routing, authentication, rate limiting, TLS termination, request logging, and sometimes response aggregation. Examples: Spring Cloud Gateway, Kong, AWS API Gateway. Risk: it can become a bottleneck or single point of failure, so it must be scaled and kept thin.

**Q67. How does service discovery work?**
> Services register their instances (address, port) in a registry, and clients look them up instead of using hard-coded addresses. Client-side: Eureka with a load-balancing client. Server-side: a load balancer queries the registry. In Kubernetes, it's built in: a `Service` gets a stable DNS name and load-balances to healthy pods.

**Q68. How does Kafka work at a high level?**
> Kafka is a distributed, append-only log. Producers write records to topics; topics are split into partitions, which are replicated across brokers. Order is guaranteed only within a partition — so we choose a key (e.g. `orderId`) to keep related events in order. Consumers in a consumer group split partitions between them and track their position with offsets. Messages are retained for a configured time, so consumers can replay.

**Q69. Delivery semantics: at-most-once, at-least-once, exactly-once?**
> At-most-once: commit the offset before processing — may lose messages. At-least-once: process then commit — may get duplicates (most common, with idempotent consumers). Exactly-once: Kafka supports it within Kafka (idempotent producer + transactions, read-process-write), but end-to-end with external systems you still need idempotency.

**Q70. Kafka vs. RabbitMQ?**
> Kafka: a log with retention and replay, very high throughput, ordering per partition, consumer groups — great for event streaming and multiple independent consumers. RabbitMQ: a traditional message broker with flexible routing (exchanges), per-message acknowledgements, priorities, and delayed messages — great for task queues. Choose by use case and what the team already operates.

**Q71. How do you do observability in microservices?**
> The three pillars: logs (structured JSON, with a correlation/trace ID), metrics (Prometheus + Grafana — RED: rate, errors, duration), and distributed tracing (OpenTelemetry, Jaeger/Tempo/Zipkin) to follow a request across services. Plus alerts based on SLOs, not on every metric.

**Q72. How do you handle data consistency between services that each own a database?**
> Accept eventual consistency where possible. Use events to propagate changes, the outbox pattern for reliable publishing, sagas for multi-step workflows, and idempotent consumers. For reads that need data from several services, use API composition or build a read model (CQRS) from events.

**Q73. What is CQRS? Event sourcing?**
> CQRS separates the write model (commands) from the read model (queries), so each can be optimized — e.g. normalized writes in PostgreSQL, denormalized reads in Elasticsearch. Event sourcing stores state as a sequence of events instead of the current value; the current state is rebuilt by replaying them. Powerful for audit trails, but adds a lot of complexity — I'd use them only where clearly needed.

---

## 6. Frontend / UI basics

**Q74. What happens when you type a URL into the browser?**
> DNS lookup → TCP connection (+ TLS handshake for HTTPS) → HTTP request → server (maybe via CDN/load balancer) returns HTML → the browser parses HTML into the DOM and CSS into the CSSOM, downloads scripts and assets, builds the render tree, does layout and paint. JavaScript can then modify the DOM.

**Q75. How does React rendering work? What is the virtual DOM?**
> React components return a description of the UI. When state or props change, React re-renders the component, compares the new virtual tree with the previous one (reconciliation), and applies only the necessary changes to the real DOM. Keys on list items help React match elements correctly.

**Q76. Explain `useState` and `useEffect`.**
> `useState` holds local state; calling the setter triggers a re-render. `useEffect` runs side effects after render — data fetching, subscriptions — and re-runs when its dependency array changes; the cleanup function runs before the next effect and on unmount. Common bugs: missing dependencies and infinite loops from setting state in an effect without proper dependencies.

**Q77. How do you manage state in a larger frontend app?**
> Keep state as local as possible. For server data, use a data-fetching library like TanStack Query (React Query) — it handles caching, refetching, and loading states. For global client state (user, theme), React Context or a small store like Zustand or Redux Toolkit. Avoid putting everything in one global store.

**Q78. What is CORS?**
> Cross-Origin Resource Sharing: browsers block JavaScript from reading responses from a different origin (scheme + host + port) unless the server allows it with headers like `Access-Control-Allow-Origin`. For non-simple requests, the browser sends a preflight `OPTIONS` request first. It's enforced by the browser, not the server — so it's not a replacement for authentication.

**Q79. How do you improve web performance?**
> Measure first (Lighthouse, Core Web Vitals: LCP, INP, CLS). Then: reduce bundle size (code splitting, lazy loading, tree shaking), optimize images (modern formats, correct sizes, lazy loading), use a CDN and caching headers, avoid layout shifts, minimize render-blocking resources, and avoid unnecessary re-renders.

**Q80. What are the basics of web accessibility (a11y)?**
> Semantic HTML (`button`, `nav`, `label`), keyboard navigation and visible focus, alt text for images, sufficient color contrast, ARIA attributes only when native HTML isn't enough, and form errors that are announced to screen readers. Standard: WCAG.
> *accessibility* = khả năng tiếp cận (cho người khuyết tật).

**Q81. Explain common web security issues: XSS and CSRF.**
> XSS (cross-site scripting): an attacker injects script into a page that runs in other users' browsers. Prevent by escaping output (React does by default — avoid `dangerouslySetInnerHTML`), sanitizing HTML, and a Content Security Policy. CSRF: a malicious site makes the user's browser send an authenticated request to your site using cookies. Prevent with `SameSite` cookies, CSRF tokens, or token-based auth in headers.

**Q82. Where should you store auth tokens in the browser?**
> It's a trade-off. `localStorage` is easy but readable by any XSS. An `HttpOnly`, `Secure`, `SameSite` cookie can't be read by JavaScript, so it's safer against XSS, but you must handle CSRF. A common approach: short-lived access token in memory + refresh token in an HttpOnly cookie, or a backend-for-frontend that keeps tokens server-side.

**Q83. How do you work with designers? How do you think about UX as an engineer?**
> I get involved early, ask about user goals and edge cases (empty states, errors, loading, long text, mobile), and give feedback on technical cost. I use the design system components for consistency. After release, I look at data — completion rates, errors — to see if the UX actually works.

---

## 7. System design

> Walkthrough đầy đủ: [week-33](../lessons/phase-4/week-33.md) (URL shortener, rate limiter), [week-34](../lessons/phase-4/week-34.md) (chat, news feed, notification).

**Q84. How do you approach a system design question?**
> Clarify functional and non-functional requirements → rough estimates (QPS, storage) → API and data model → high-level design → deep dive into the hardest parts → discuss trade-offs, bottlenecks, failures, and monitoring. Keep checking in with the interviewer.

**Q85. How would you scale a web application from 1,000 to 1 million users?**
> Make the app servers stateless and scale horizontally behind a load balancer; add caching (CDN for static content, Redis for hot data); add read replicas; move slow work to async queues; then partition/shard the database and split services where needed. Add monitoring at each step to find the real bottleneck.

**Q86. What caching strategies do you know?**
> Cache-aside (app reads cache, on miss reads DB and fills cache — most common), read-through, write-through (write to cache and DB together), write-behind (write to cache, DB later — risky), and refresh-ahead. Plus eviction policies (LRU, LFU, TTL). The hard parts: invalidation, stampedes (use locking or early refresh), and consistency.

**Q87. How do you design for high availability?**
> Remove single points of failure: multiple instances across availability zones, load balancers with health checks, replicated databases with automatic failover, and graceful degradation (circuit breakers, fallbacks). Define SLOs, test failures (chaos testing), and make deployments safe (rolling/canary with fast rollback).

**Q88. Load balancing algorithms?**
> Round robin, weighted round robin, least connections, IP hash / consistent hashing (sticky routing). L4 load balancers route by IP/port (fast); L7 by HTTP content (path, headers). Health checks remove unhealthy instances.

**Q89. What is consistent hashing?**
> A hashing scheme where nodes and keys are placed on a ring; each key goes to the next node clockwise. When a node is added or removed, only about 1/N of keys move, instead of almost all keys with `hash % N`. Virtual nodes improve balance. Used in distributed caches and databases like Cassandra and DynamoDB.

**Q90. How would you design a distributed job scheduler (e.g. send reports at 8 a.m.)?**
> Store jobs in a database with `next_run_at`. Multiple scheduler instances poll for due jobs and claim them safely (`SELECT ... FOR UPDATE SKIP LOCKED` or a distributed lock), then push them to a queue for workers. Workers are idempotent; failed jobs retry with backoff. Libraries: Quartz (clustered mode), ShedLock for Spring `@Scheduled`.

**Q91. How would you design file upload for large files?**
> Don't stream large files through the app server. The client asks the backend for a pre-signed URL, uploads directly to object storage (S3) — multipart upload for large files with resume support — then the backend is notified (S3 event or client callback) to process the file asynchronously (virus scan, thumbnails). Serve downloads via a CDN with signed URLs.

---

## 8. DevOps / Cloud basics

**Q92. What is Docker, and how is a container different from a VM?**
> Docker packages an app with its dependencies into an image that runs the same everywhere. Containers share the host OS kernel and isolate processes with namespaces and cgroups, so they're lightweight and start in seconds. VMs virtualize hardware and run a full guest OS — stronger isolation, but heavier.

**Q93. How do you write a good Dockerfile for a Spring Boot app?**
> Use a slim JRE base image, multi-stage builds (build with Maven/Gradle, copy only the jar), layered jars for better caching, run as a non-root user, and set JVM memory relative to the container (`-XX:MaxRAMPercentage`). Keep images small and scan them for vulnerabilities.

**Q94. Explain the basic Kubernetes objects.**
> Pod (one or more containers, the smallest unit), Deployment (manages replicas and rolling updates), Service (stable network endpoint and load balancing for pods), Ingress (HTTP routing from outside), ConfigMap and Secret (configuration), HorizontalPodAutoscaler (scales pods by CPU/memory/custom metrics).

**Q95. Liveness vs. readiness probes?**
> A readiness probe says whether the pod can receive traffic — if it fails, Kubernetes removes it from the Service, but doesn't restart it. A liveness probe says whether the app is alive — if it fails, Kubernetes restarts the container. Don't make liveness depend on external systems like the database, or a DB outage will restart all pods. Spring Boot Actuator provides both endpoints.

**Q96. What does your CI/CD pipeline look like?**
> On each pull request: build, unit tests, static analysis, and security scans. On merge to main: integration tests, build and push a Docker image, deploy to staging automatically, run smoke tests, then deploy to production — with approval or automatically — using rolling or canary deployment and automatic rollback on failing health checks. Tools: GitHub Actions/GitLab CI/Jenkins, Argo CD or Helm.

**Q97. Deployment strategies: rolling, blue-green, canary?**
> Rolling: replace instances gradually — no extra infrastructure, but two versions run together. Blue-green: run the new version fully alongside the old, then switch traffic at once — fast rollback, but double resources. Canary: send a small percentage of traffic to the new version, watch metrics, then increase. Feature flags separate deploy from release.

**Q98. Which AWS services have you used, and for what?**
> Example: "EC2 and EKS for compute, RDS PostgreSQL for databases, S3 for files, SQS/SNS for queues and fan-out, ElastiCache Redis for caching, CloudWatch for logs and alarms, IAM roles for permissions, and Secrets Manager for credentials." Only mention what you actually used.

**Q99. How do you manage configuration and secrets?**
> Externalize config (12-factor): environment variables, Spring profiles, ConfigMaps. Secrets never go into Git; use a secret manager (AWS Secrets Manager, Vault, Kubernetes Secrets with encryption), rotate them, and give each service only the permissions it needs (least privilege).

**Q100. What is Infrastructure as Code?**
> Managing infrastructure with versioned code instead of manual clicks — Terraform, CloudFormation, Pulumi, or Helm charts for Kubernetes. Benefits: reproducible environments, code review for infra changes, and easy rollback. Terraform keeps state to know what exists and shows a plan before applying.

**Q101. How do you troubleshoot a service that is slow in production?**
> Check dashboards first: latency, error rate, traffic, saturation (CPU, memory, GC, connection pools, thread pools). Use traces to find which span is slow — DB, external call, or the code itself. Check recent deployments and config changes. For JVM issues: GC logs, thread dumps, heap dumps, or a profiler like async-profiler / JFR. Mitigate first (rollback, scale up), then fix the root cause.

---

## 9. Questions to ask the interviewer

> Chi tiết + cách chọn câu theo người phỏng vấn: [week-35](../lessons/phase-4/week-35.md).

**Q102.** "What does a typical week look like for an engineer on this team?"
**Q103.** "What are the biggest technical challenges the team is facing right now?"
**Q104.** "What would you expect me to achieve in my first three to six months?"
**Q105.** "How does the team handle code reviews, testing, and deployments? How often do you release?"
**Q106.** "How are technical decisions made — is there a design review or RFC process?"
**Q107.** "How is performance evaluated, and what does the growth path look like for senior engineers?"
**Q108.** "Is there an on-call rotation? How often are people paged?"
**Q109.** "What do you enjoy most about working here?"
**Q110.** "What are the next steps in the process?"

> Tránh hỏi ngay ở vòng kỹ thuật: lương, số ngày nghỉ, "Tôi có phải OT không?". Để những câu đó cho recruiter.
