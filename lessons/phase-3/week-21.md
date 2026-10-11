# Tuần 21 — Code review và giải thích code

> Giai đoạn 3 · Tuần 4/9 · Checklist gốc: [phase-3-it-english.md](../../phase-3-it-english.md#tuần-21--code-review-và-giải-thích-code)

## 1. Mục tiêu tuần

- Viết và đọc hiểu comment code review: *nit, LGTM, PTAL, Could we extract this into...?*
- Góp ý **về code, không về người**: "This method is doing too much" thay vì "You wrote bad code".
- Đọc to và giải thích một hàm Java từng dòng (T3), theo khung: *mục đích → input → các bước → output → edge case*.
- Giải thích **multithreading và race condition** trong Java, và **SOLID**.

## 2. Từ vựng IT

| # | Từ | IPA (Mỹ) | Cách đọc dễ nhớ | Nghĩa | Câu ví dụ |
| --- | --- | --- | --- | --- | --- |
| 1 | nit (nitpick) | /nɪt/ | "NÍT" | góp ý nhỏ, không bắt buộc | Nit: this variable name could be clearer. |
| 2 | LGTM | | "EL-GI-TI-EM" | Looks good to me | LGTM, approved. |
| 3 | PTAL | | "PI-TI-ÂY-EL" | Please take a(nother) look | Fixed the comments, PTAL. |
| 4 | WIP | /wɪp/ | "UÍP" | đang làm dở | Don't review yet, it's still WIP. |
| 5 | approve | /əˈpruːv/ | "ơ-PRUV" | phê duyệt | Mai approved the PR. |
| 6 | request changes | | | yêu cầu sửa | I requested changes because tests are missing. |
| 7 | refactor | /riˈfæktər/ | "ri-FÉK-tơ" | tái cấu trúc code | Let's refactor this before adding new logic. |
| 8 | extract (method) | /ɪkˈstrækt/ | "ik-STRÉKT" | tách ra thành hàm riêng | Could we extract this into a helper method? |
| 9 | readability | /ˌriːdəˈbɪləti/ | "ri-đơ-BI-lơ-ri" | dễ đọc | Splitting the method improves readability. |
| 10 | edge case | /ɛdʒ keɪs/ | "ÉJ kêys" | trường hợp biên | What happens in the edge case where the list is empty? |
| 11 | magic number | | | số "thần kỳ" không rõ nghĩa | Please replace the magic number 86400 with a constant. |
| 12 | hardcoded | /ˈhɑːrdkoʊdɪd/ | "HARD-kâu-đid" | viết cứng trong code | The URL is hardcoded; move it to config. |
| 13 | duplicate / duplication | /ˈduːplɪkət/ | "ĐU-pli-kợt" | trùng lặp | This logic is duplicated in three places. |
| 14 | side effect | /saɪd ɪˈfɛkt/ | "SAID i-FÉKT" | tác dụng phụ | This getter has a side effect: it writes to the DB. |
| 15 | immutable | /ɪˈmjuːtəbəl/ | "i-MIU-tơ-bồ" | bất biến | Make this class immutable with a record. |
| 16 | null-safe | | | an toàn với null | Use `Optional` to make it null-safe. |
| 17 | thread | /θrɛd/ | "THRED" (lưỡi giữa răng) | luồng | Each request runs on its own thread. |
| 18 | thread-safe | /θrɛd seɪf/ | "THRED SÊYF" | an toàn đa luồng | `HashMap` is not thread-safe. |
| 19 | concurrency | /kənˈkɝːənsi/ | "kần-KƠ-rần-si" | xử lý đồng thời | Concurrency bugs are hard to reproduce. |
| 20 | parallelism | /ˈpærəlɛlɪzəm/ | "PÉ-rơ-le-li-zầm" | song song thực sự | Parallel streams use parallelism on many cores. |
| 21 | race condition | /reɪs kənˈdɪʃən/ | "RÊYS kần-ĐÍ-shần" | tranh chấp dữ liệu | Two threads updating the counter cause a race condition. |
| 22 | deadlock | /ˈdɛdlɑːk/ | "ĐÉT-lak" | khóa chết | The two transactions caused a deadlock. |
| 23 | lock | /lɑːk/ | "LAK" | khóa | We take a lock before updating the balance. |
| 24 | synchronized | /ˈsɪŋkrənaɪzd/ | "SÍNG-krơ-naizd" | đồng bộ hóa | Mark the method as `synchronized`. |
| 25 | atomic | /əˈtɑːmɪk/ | "ơ-TA-mik" | nguyên tử, không chia cắt | Use `AtomicInteger` for an atomic increment. |
| 26 | volatile | /ˈvɑːlətəl/ | "VA-lơ-rồ" | biến luôn đọc từ bộ nhớ chính | The `running` flag should be `volatile`. |
| 27 | thread pool | /θrɛd puːl/ | "THRED PUL" | nhóm luồng tái sử dụng | We use a fixed thread pool of 10 threads. |
| 28 | executor | /ɪɡˈzɛkjətər/ | "ig-ZÉ-kiu-tơ" | bộ thực thi tác vụ | Submit the task to an `ExecutorService`. |
| 29 | dependency injection | /dɪˈpɛndənsi ɪnˈdʒɛkʃən/ | "đì-PÉN-đần-si in-GIÉK-shần" | tiêm phụ thuộc | Spring uses dependency injection. |
| 30 | interface | /ˈɪntərfeɪs/ | "IN-tơ-fêys" | giao diện | Depend on the interface, not the implementation. |
| 31 | abstraction | /æbˈstrækʃən/ | "éb-STRÉK-shần" | trừu tượng | This abstraction hides the payment provider. |
| 32 | single responsibility | /rɪˌspɑːnsəˈbɪləti/ | "ri-span-sơ-BI-lơ-ri" | đơn trách nhiệm | This class breaks the single responsibility principle. |
| 33 | unit test / mock | /mɑːk/ | "MAK" | kiểm thử đơn vị / đối tượng giả | Mock the repository in this unit test. |
| 34 | test coverage | /ˈkʌvərɪdʒ/ | "KÂ-vơ-rij" | độ phủ test | Coverage dropped to 70%. |
| 35 | blocking / non-blocking | | | chặn / không chặn | This call is blocking, so it holds the thread. |
| 36 | out of scope | | | ngoài phạm vi | Good idea, but out of scope for this PR. |

## 3. Mẫu câu công việc

**Comment review: góp ý nhẹ (nit, optional)**
1. Nit: missing a space here.
2. Nit: could we rename `data` to something more specific, like `orderItems`?
3. Optional: you could use a stream here, but the loop is fine too.
4. Minor: this import isn't used.

**Comment review: đề xuất thay đổi**
5. Could we extract this into a separate method? It would make `process()` easier to read.
6. What do you think about moving this logic to the service layer?
7. I'd suggest using a constant instead of the magic number `3600`.
8. Can we avoid hardcoding the URL? It should come from config.
9. This looks duplicated in `UserService`. Could we reuse that method?

**Comment review: lo ngại nghiêm trọng (blocking)**
10. I think this could cause a race condition if two requests come in at the same time.
11. What happens if `customer` is null here?
12. This query runs inside the loop, so we get N plus one queries.
13. This isn't thread-safe. `SimpleDateFormat` shouldn't be shared between threads.
14. We should add a test for the empty list case before merging.

**Comment review: hỏi để hiểu**
15. Just curious, why did you choose a `LinkedList` here?
16. Could you explain the reason for this retry logic?
17. Is this change related to the ticket, or is it a separate fix?

**Comment review: khen**
18. Nice! This is much cleaner than before.
19. Great test coverage.
20. Good catch on the timezone issue.

**Trả lời review**
21. Good point, fixed.
22. Done. PTAL.
23. I'd prefer to keep it as is, because ... What do you think?
24. Agreed, but it's out of scope. I've created a follow-up ticket.
25. Thanks for the review!

**Giải thích code từng dòng**
26. This method takes ... and returns ...
27. First, we check whether ... If not, we throw an exception.
28. Then we loop through ...
29. On this line, we ...
30. Here's the tricky part: ...
31. Finally, we return ...
32. One edge case is when ...

## 4. Hội thoại mẫu

### Hội thoại 1: Review PR qua call

> **Linh:** Thanks for reviewing my PR. I saw you requested changes?
> **Nhat:** Yes, just one blocking comment. The rest are nits. In `applyDiscount`, you read the balance, calculate the new value and then save it. If two requests come in at the same time, they can both read the old balance.
> **Linh:** Oh, so one update could get lost.
> **Nhat:** Exactly, it's a race condition. Since the data is in Postgres, the simplest fix is optimistic locking. Add a `@Version` field to the entity, and JPA will throw an exception if someone else updated the row first.
> **Linh:** Makes sense. And the nits?
> **Nhat:** Mostly naming. `tmp` could be `discountedTotal`, and there's a magic number, `0.15`. Maybe make it a constant, like `LOYALTY_DISCOUNT_RATE`.
> **Linh:** Good point. I'll fix those today and ping you.
> **Nhat:** Great. Otherwise it looks good. Nice tests, by the way.

### Hội thoại 2: Giải thích code cho gia sư / người không biết Java

> **Tutor:** Can you explain what this function does?
> **Nhat:** Sure. In simple terms, it finds the customers who haven't ordered anything in the last ninety days, so marketing can send them a discount.
> **Tutor:** OK. And how does it work?
> **Nhat:** First, it calculates a date: today minus ninety days. Then it loads all active customers from the database. For each customer, it checks the date of their last order. If the date is before the cutoff, or if they never ordered, we add them to the result list.
> **Tutor:** Is there anything you would improve?
> **Nhat:** Yes. Right now it loads every customer into memory. With a million customers, that's slow. I'd move the filter into the SQL query, so the database does the work.

## 5. Bài giải thích kỹ thuật mẫu

### 5.0 T3 — Đọc to và giải thích một hàm Java từng dòng (mẫu)

```java
public Optional<Order> cancelOrder(long orderId, String reason) {
    Order order = orderRepository.findById(orderId)
            .orElseThrow(() -> new OrderNotFoundException(orderId));

    if (order.getStatus() == OrderStatus.SHIPPED) {
        return Optional.empty();
    }

    order.setStatus(OrderStatus.CANCELLED);
    order.setCancelReason(reason);
    eventPublisher.publish(new OrderCancelledEvent(orderId));
    return Optional.of(orderRepository.save(order));
}
```

> This method cancels an order. It takes the order ID and a reason, and it returns an `Optional` of the updated order.
>
> On the first line, we look up the order by its ID. If it doesn't exist, we throw an `OrderNotFoundException`.
>
> Next, we check the status. If the order has already been shipped, we can't cancel it, so we return an empty `Optional`. The caller can then show a message to the user.
>
> Otherwise, we set the status to `CANCELLED` and save the reason. Then we publish an `OrderCancelledEvent`, so other services, like payments, can issue a refund. Finally, we save the order and return it.
>
> One thing I'd improve: we publish the event before saving. If the save fails, other services will react to a cancellation that never happened. It would be safer to publish after the transaction commits, for example with the outbox pattern or a transactional event listener.

Khung dùng cho mọi hàm: **What it does → Input/Output → Step by step (First / Next / Then / Finally) → Edge case → What I'd improve.**

### 5.1 T4 — Multithreading in Java and race conditions

> A thread is a single path of execution inside a program. A Java application can run many threads at the same time. For example, a Spring Boot web server handles each incoming request on a thread from a thread pool. Multithreading helps us use several CPU cores and keep the application responsive while some threads are waiting for I/O, like a database call.
>
> The problem is shared data. Threads in the same process share the heap, so two threads can read and write the same object. Take a simple counter: `count++`. It looks like one step, but it's actually three: read the value, add one, write it back. If two threads read the value five at the same time, both write six. We expected seven. One update is lost. This is a race condition: the result depends on the timing of the threads, so the bug is random and hard to reproduce.
>
> Java gives us several tools to prevent it. We can use the `synchronized` keyword or a `ReentrantLock`, so only one thread can run that block at a time. For simple cases, atomic classes like `AtomicInteger` do the update in one atomic operation. Concurrent collections, like `ConcurrentHashMap`, are safe to share. And the best option is often to avoid shared mutable state completely, for example with immutable objects.
>
> We also need to be careful: too much locking can cause deadlocks, where two threads wait for each other forever. For new code, I prefer high-level tools like `ExecutorService` or `CompletableFuture` instead of creating threads by hand. And since Java 21, virtual threads make it cheap to run a very large number of blocking tasks.

**5 cụm từ dùng lại:**
1. *X is a single ... inside ...*
2. *It looks like one step, but it's actually three.*
3. *The result depends on the timing of ...*
4. *Java gives us several tools to prevent it.*
5. *The best option is often to avoid ... completely.*

### 5.2 T6 — SOLID principles

> SOLID is a set of five object-oriented design principles that help us write code that is easy to change.
>
> **S** is the Single Responsibility Principle: a class should have only one reason to change. For example, an `OrderService` shouldn't also format PDF invoices. That should be a separate class.
>
> **O** is Open/Closed: code should be open for extension but closed for modification. If we add a new payment method, we should add a new class that implements a `PaymentProvider` interface, not add another `if` to a big switch statement.
>
> **L** is the Liskov Substitution Principle: a subclass must be usable anywhere its parent is used, without breaking the behavior. The classic bad example is a `Square` extending `Rectangle`: setting the width also changes the height, which surprises code that expects a rectangle.
>
> **I** is Interface Segregation: many small, focused interfaces are better than one huge interface. A class shouldn't be forced to implement methods it doesn't need.
>
> **D** is Dependency Inversion: high-level code should depend on abstractions, not on concrete classes. In Spring, our service depends on a `UserRepository` interface, and the framework injects the implementation. This also makes unit testing easy, because we can pass a mock.
>
> These are guidelines, not strict rules. Applied too much, they can create too many tiny classes, so I use them when the code actually needs to change.

**5 cụm từ dùng lại:**
1. *X is a set of ... that help us ...*
2. *A class should have only one reason to change.*
3. *The classic bad example is ...*
4. *This also makes ... easy, because ...*
5. *These are guidelines, not strict rules.*

## 6. Mẫu viết

**Quy ước tiền tố comment review** (nhiều team dùng, dựa trên *Conventional Comments*)

```
nit:        small style issue, non-blocking
suggestion: an idea, author decides
question:   I want to understand, not necessarily a change
issue:      must be fixed before merge
praise:     something done well
```

**Comment mẫu đầy đủ**

```
issue: This isn't thread-safe. `orderCache` is a HashMap shared by all request threads,
so concurrent `put` calls can corrupt it. Could we use a ConcurrentHashMap,
or better, the existing Caffeine cache?
```

```
suggestion (non-blocking): This method is about 80 lines. What do you think about
extracting the validation part into `validateRequest()`? It would make the main flow
easier to follow.
```

**Tổng kết review**

```
Thanks, this is a nice improvement! Two things before I approve:
1. Possible race condition in `applyDiscount` (see comment).
2. Missing test for the empty-cart case.
Everything else is nits, feel free to ignore them.
```

## 7. Bài tập

1. **Viết lại comment cho lịch sự và cụ thể:** (a) "Bad name." (b) "Why so long???" (c) "Wrong, this is not thread-safe." (d) "No tests."
2. **Ghép:** (a) LGTM (b) PTAL (c) nit (d) WIP — (1) chưa xong, đừng review (2) góp ý nhỏ (3) code ổn (4) mời xem lại.
3. **Tìm lỗi đa luồng:** đoạn code sau có vấn đề gì? Viết 2–3 câu tiếng Anh giải thích và cách sửa.
   ```java
   public class VisitCounter {
       private int visits = 0;
       public void increment() { visits++; }
   }
   ```
4. **SOLID:** mỗi tình huống vi phạm nguyên tắc nào? (a) `UserService` vừa lưu user vừa gửi email vừa tạo báo cáo Excel. (b) Mỗi lần thêm loại thông báo mới phải sửa một `switch` lớn. (c) Interface `Worker` có `work()`, `eat()`, `sleep()`, nhưng class `Robot` buộc phải implement `eat()`.
5. **Điền từ:** deadlock, edge case, refactor, hardcoded, side effect. (a) The password is ___ in the code. (b) Calling `getUser()` shouldn't have a ___. (c) Let's ___ this class before adding features. (d) An empty string is an ___ we forgot. (e) Thread A waits for B, and B waits for A: that's a ___.
6. **Nói (T3):** chọn một hàm Java thật trong dự án của bạn (20–40 dòng), giải thích theo khung ở mục 5.0, 2–3 phút, ghi âm.
7. **Nói:** giải thích race condition và SOLID, mỗi bài ≤ 3 phút.

## 8. Tài liệu

- [Google Engineering Practices — Code Review](https://google.github.io/eng-practices/review/) — hướng dẫn review của Google, tiếng Anh dễ đọc, rất nhiều câu mẫu.
- [The Java Tutorials — Concurrency](https://docs.oracle.com/javase/tutorial/essential/concurrency/) — bài chính thức của Oracle về thread, synchronization, atomic.
- [Refactoring.Guru](https://refactoring.guru) — code smells, refactoring và design patterns, có hình minh họa, rất hợp để học từ vựng review.
- [Fireship](https://www.youtube.com/@Fireship) — tìm "SOLID" và "concurrency vs parallelism".
- [ByteByteGo YouTube](https://www.youtube.com/@ByteByteGo) — tìm "code review".
- [GOTO Conferences](https://www.youtube.com/@GOTO-) — tìm talk về "clean code" hoặc "refactoring".

## 9. Đáp án

**Bài 1 (gợi ý):**
(a) "Nit: could we use a more descriptive name, like `activeUsers`?"
(b) "This method is quite long. Could we split it into smaller methods?"
(c) "issue: I think this might not be thread-safe, because `cache` is shared between requests. What do you think about using `ConcurrentHashMap`?"
(d) "Could we add a unit test for this logic, especially the error case?"

**Bài 2:** a-3, b-4, c-2, d-1.

**Bài 3 (gợi ý):** "`visits++` is not atomic. It reads, increments and writes the value in three steps, so if two threads call `increment()` at the same time, one update can be lost. That's a race condition. We can fix it with `AtomicInteger` and `incrementAndGet()`, or by making the method `synchronized`."

**Bài 4:** (a) Single Responsibility (b) Open/Closed (c) Interface Segregation.

**Bài 5:** (a) hardcoded (b) side effect (c) refactor (d) edge case (e) deadlock.

**Bài 6, 7:** tự chấm theo khung: có câu mở đầu nói mục đích, dùng First/Next/Then/Finally, nêu ít nhất 1 edge case.
