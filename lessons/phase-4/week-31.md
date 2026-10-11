# Tuần 31 — Coding interview: nói khi đang nghĩ (think aloud)

> Checklist gốc: [phase-4-interview.md](../../phase-4-interview.md#tuần-31--coding-interview-nói-khi-đang-nghĩ)

## 1. Mục tiêu tuần này

- Thuộc các mẫu câu cho **6 bước** của một bài coding interview.
- Giải ít nhất 2 bài LeetCode Easy, **nói to toàn bộ bằng tiếng Anh**, ghi âm.
- **Phỏng vấn thử #3** (coding).

> Trong coding interview, interviewer chấm **cách bạn nghĩ và giao tiếp** gần ngang với việc code đúng. Im lặng 5 phút rồi đưa code đúng = điểm thấp hơn nói rõ hướng đi và có 1 lỗi nhỏ được tự phát hiện.

## 2. Khung 6 bước (UMPIRE rút gọn)

| Bước | Việc làm | Thời gian (bài 30') |
| --- | --- | --- |
| **1. Clarify** | Nhắc lại đề, hỏi input/output, edge cases, ràng buộc | 2–4' |
| **2. Examples** | Tự lấy 1–2 ví dụ, kể cả edge case | 1–2' |
| **3. Approach** | Nói brute force + độ phức tạp → tối ưu → **xin đồng ý** trước khi code | 3–5' |
| **4. Code** | Code và **giải thích trong khi viết** | 10–15' |
| **5. Test** | Chạy tay ví dụ, edge cases, tìm bug | 3–5' |
| **6. Complexity & follow-up** | Time/space, cách cải thiện, câu hỏi mở rộng | 2–3' |

### Đọc độ phức tạp bằng tiếng Anh

| Ký hiệu | Đọc là |
| --- | --- |
| O(1) | "O of one" / "constant time" |
| O(log n) | "O of log n" / "logarithmic" |
| O(n) | "O of n" / "linear time" |
| O(n log n) | "O of n log n" |
| O(n²) | "O of n squared" / "quadratic" |
| O(2ⁿ) | "O of two to the n" / "exponential" |
| O(n + m) | "O of n plus m" |

- "big O" đọc là /bɪɡ əʊ/.
- **time complexity** (độ phức tạp thời gian), **space complexity** (bộ nhớ), **auxiliary space** (bộ nhớ phụ).

## 3. Full think-aloud script: Two Sum (LeetCode #1)

> Đề: Cho mảng số nguyên `nums` và số `target`, trả về **chỉ số** của 2 phần tử có tổng bằng `target`. Mỗi input có đúng 1 đáp án, không dùng 1 phần tử 2 lần.

**Interviewer:** "Given an array of integers and a target, return the indices of the two numbers that add up to the target."

### Bước 1 — Clarify

> **You:** "Okay, let me make sure I understand the problem. I get an array of integers and a target integer, and I need to return the **indices** — not the values — of two different elements whose sum equals the target. Is that right?"
>
> **Interviewer:** "Yes."
>
> **You:** "A few questions. First, can there be more than one valid pair, or is there always exactly one solution?"
>
> **Interviewer:** "You can assume exactly one solution."
>
> **You:** "Got it. Can the array contain negative numbers or duplicates?"
>
> **Interviewer:** "Yes, both."
>
> **You:** "And can I use the same element twice? For example, if the target is 6 and there's a single 3?"
>
> **Interviewer:** "No, two different indices."
>
> **You:** "Okay. And does the order of the output matter? And roughly how large can the array be?"
>
> **Interviewer:** "Any order. Up to 10 to the power of 4 elements."

### Bước 2 — Examples

> **You:** "Let me write a quick example. `nums = [2, 7, 11, 15]`, `target = 9`. The answer is `[0, 1]`, because 2 plus 7 is 9.
>
> An edge case with duplicates: `nums = [3, 3]`, `target = 6` — the answer should be `[0, 1]`. And with negatives: `[-1, 4, 5]`, target `3` → `[0, 1]`."

### Bước 3 — Approach

> **You:** "The simplest idea is brute force: check every pair with two nested loops. For each `i`, loop `j` from `i + 1` to the end, and check if `nums[i] + nums[j] == target`. That's **O of n squared** time and **O of one** extra space. With 10 to the 4 elements, that's about 50 million checks — it would probably pass, but we can do better.
>
> To optimize, I notice that for each number `x`, I'm really looking for its **complement**, `target - x`. If I can check whether I've already seen the complement in constant time, I only need one pass. So I'll use a **hash map** from value to index.
>
> I go through the array once. For each element, I first check if `target - nums[i]` is already in the map. If yes, I return the stored index and the current index. If not, I put the current value and index into the map. Checking **before** inserting also handles the 'same element twice' case correctly — for example, with `[3, 3]`, the first 3 isn't matched with itself.
>
> That's **O of n** time and **O of n** space. The trade-off is using extra memory for the map to get linear time. Does that sound good, or should I consider something else — like sorting with two pointers?"
>
> **Interviewer:** "What about sorting?"
>
> **You:** "Sorting with two pointers would be O of n log n time, and it works well for finding the values, but we'd lose the original indices, so we'd need to sort pairs of value and index. It's more complex and slower than the hash map, so I'd go with the hash map."
>
> **Interviewer:** "Sounds good, go ahead."

### Bước 4 — Code (nói trong khi viết)

```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> seen = new HashMap<>(); // value -> index
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (seen.containsKey(complement)) {
                return new int[] { seen.get(complement), i };
            }
            seen.put(nums[i], i);
        }
        throw new IllegalArgumentException("No solution");
    }
}
```

> **You (khi viết):** "I'll create a `HashMap` called `seen` that maps a value to its index… Now I loop through the array with index `i`… I compute the complement as `target - nums[i]`… If `seen` contains the complement, I return a new array with the stored index and `i`… Otherwise, I put the current number and its index into the map… The problem says there's always a solution, so after the loop I'll just throw an exception — in a real codebase, I might return an empty array or an `Optional` instead, depending on the team's convention."

### Bước 5 — Test

> **You:** "Now let me walk through the example to check. `nums = [2, 7, 11, 15]`, target 9.
> - `i = 0`: the value is 2, the complement is 7. The map is empty, so I put 2 → 0.
> - `i = 1`: the value is 7, the complement is 2. 2 is in the map with index 0, so I return `[0, 1]`. Correct.
>
> Now the duplicate case `[3, 3]`, target 6.
> - `i = 0`: the complement is 3, the map is empty, so I put 3 → 0.
> - `i = 1`: the complement is 3, found at index 0, return `[0, 1]`. Correct — and we didn't use the same element twice.
>
> Negative numbers work the same way, because the subtraction handles them. One thing to double-check: integer overflow on `target - nums[i]`. With normal LeetCode constraints, values are up to 10 to the 9, so the subtraction fits in an `int`. If the range were bigger, I'd use `long`."

### Bước 6 — Complexity & follow-up

> **You:** "So the final complexity is **O of n** time, since we visit each element once and hash map operations are O of one on average, and **O of n** space for the map in the worst case."
>
> **Interviewer:** "What if the array were already sorted?"
>
> **You:** "Then I'd use two pointers — one at the start, one at the end. If the sum is too small, move the left pointer right; if it's too big, move the right pointer left. That's O of n time and O of one space, so better on memory."
>
> **Interviewer:** "What if we needed all pairs, not just one?"
>
> **You:** "Then I can't return early. I'd store a list of indices for each value, and for each element, add a pair for every earlier index of its complement. The output itself could be O of n squared in the worst case — for example, if all elements are equal — so the complexity depends on the output size."

## 4. Model answer thứ 2 (ngắn): Valid Parentheses (LeetCode #20)

> "Let me restate: I get a string containing only brackets — round, square, and curly — and I need to check if every opening bracket is closed by the same type, in the correct order. Is an empty string valid? … Okay, I'll treat it as valid.
>
> My approach is to use a **stack**. When I see an opening bracket, I push it. When I see a closing bracket, the top of the stack must be the matching opening bracket — if the stack is empty or it doesn't match, I return false. At the end, the string is valid only if the stack is empty, because otherwise some brackets were never closed.
>
> That's O of n time and O of n space in the worst case, for example a string of only opening brackets.
>
> A quick optimization: if the length is odd, I can return false immediately."

```java
public boolean isValid(String s) {
    if (s.length() % 2 == 1) return false;
    Deque<Character> stack = new ArrayDeque<>();
    for (char c : s.toCharArray()) {
        if (c == '(') stack.push(')');
        else if (c == '[') stack.push(']');
        else if (c == '{') stack.push('}');
        else if (stack.isEmpty() || stack.pop() != c) return false;
    }
    return stack.isEmpty();
}
```

> "Here I used a small trick: instead of pushing the opening bracket, I push the **expected closing bracket**, so the comparison is simpler. I'm using `ArrayDeque` instead of the old `Stack` class, because `Stack` is synchronized and generally not recommended in modern Java."

## 5. Cụm từ hữu ích (40)

**Clarify**
1. Let me make sure I understand the problem correctly. — Để tôi chắc là hiểu đúng đề.
2. So, just to restate the problem, ... — Nhắc lại đề
3. Can I assume that...? — Tôi có thể giả sử rằng...?
4. What should I return if...? — Trả về gì nếu...?
5. Can the input be empty / null? — Input có thể rỗng / null?
6. Are there duplicates / negative numbers? — Có trùng / số âm?
7. How large can the input be? — Input lớn tới đâu?
8. Is the array sorted? — Mảng đã sắp xếp chưa?
9. Should I optimize for time or for memory? — Tối ưu thời gian hay bộ nhớ?

**Approach**
10. Let me start with a brute-force approach. — Bắt đầu bằng vét cạn
11. The naive solution would be... — Cách ngây thơ là...
12. That would be O of n squared, which is too slow for large inputs. — Quá chậm
13. Can we do better? I think so. — Có cách tốt hơn
14. The key observation / insight here is... — Nhận xét then chốt
15. I could use a hash map / a stack / two pointers / a sliding window. — Cấu trúc dữ liệu
16. The trade-off is extra memory for faster lookup. — Đánh đổi
17. Does this approach sound good to you? / Should I go ahead and code it? — Xin xác nhận
18. I'm thinking out loud here... — Tôi đang nghĩ thành lời

**Coding**
19. I'll start by initializing... — Khởi tạo
20. I'm going to loop through... — Duyệt
21. Here I'm checking whether... — Kiểm tra xem
22. This handles the case where... — Xử lý trường hợp
23. I'll write a helper function for... — Hàm phụ
24. Let me name this variable something clearer. — Đặt tên rõ hơn
25. I'll skip the input validation for now, but in production I'd... — Bỏ qua tạm
26. Give me a second to think about this part. — Cho tôi 1 giây

**Testing & debugging**
27. Let me walk through an example. — Chạy tay ví dụ
28. Let me trace the code with this input. — Lần theo code
29. At this point, the map contains... — Tại thời điểm này
30. Oh, I see a bug here. This should be... — Có bug
31. Let me check the edge cases: empty input, one element, ... — Kiểm tra biên
32. What about an off-by-one error here? — Lỗi lệch 1
33. I think this works now. — Tôi nghĩ đúng rồi

**Complexity & follow-up**
34. The time complexity is O of n, because... — Độ phức tạp thời gian
35. The space complexity is O of n for the map. — Bộ nhớ
36. On average / in the worst case, ... — Trung bình / tệ nhất
37. If I had more time, I would... — Nếu có thêm thời gian
38. One possible improvement is... — Một cải tiến có thể
39. If the input didn't fit in memory, I'd... — Nếu không vừa bộ nhớ
40. I'm stuck on this part. Could you give me a small hint? — Xin gợi ý (được phép!)

## 6. Lỗi người Việt hay mắc

1. **Im lặng code luôn.** Interviewer không biết bạn nghĩ gì → không thể giúp, không thể chấm. Nói ít nhất 1 câu mỗi 30 giây.
2. **Không hỏi clarify** vì sợ bị coi là không hiểu đề. Ngược lại: không hỏi = trừ điểm.
3. **Code trước khi interviewer đồng ý approach** → code sai hướng 15 phút.
4. **Không test.** Nói "I think it's correct" mà không chạy tay.
5. **Đọc code từng ký tự:** "for open bracket int i equal zero semicolon..." → Nói **ý**: "I loop through the array".
6. **Phát âm:** *array* /əˈreɪ/, *integer* /ˈɪntɪdʒə/, *index* / *indices* /ˈɪndɪsiːz/, *iterate* /ˈɪtəreɪt/, *algorithm* /ˈælɡərɪðəm/, *recursion* /rɪˈkɜːʃn/, *queue* /kjuː/, *height* /haɪt/, *width* /wɪdθ/, *null* /nʌl/, *char* /tʃɑː/ hoặc /kɑː/.
7. **Xin lỗi liên tục** "Sorry, sorry..." → thay bằng "Let me fix that."
8. **Không dám xin gợi ý.** Xin gợi ý đúng lúc là kỹ năng tốt, không phải thất bại.

## 7. Lịch luyện trong tuần

| Ngày | Việc |
| --- | --- |
| T2 | Học 40 mẫu câu mục 5, đặt vào Anki. Đọc to script Two Sum mục 3 hai lần (shadow chính mình). |
| T3 | Giải **Two Sum** (đóng script lại) — nói to 6 bước, bấm giờ 20'. |
| T4 | Giải **Valid Parentheses** hoặc **Best Time to Buy and Sell Stock** (#121). Ghi âm. |
| T5 | **Phỏng vấn thử #3** — prompt mục 8, hoặc Pramp. |
| T6 | Nghe lại, ghi những chỗ bạn im lặng > 20s hoặc chuyển sang tiếng Việt trong đầu; thêm cụm còn thiếu vào Anki. |
| T7 | Ôn + nhật ký. |

**Bài Easy gợi ý luyện think-aloud:** Two Sum (#1), Valid Parentheses (#20), Merge Two Sorted Lists (#21), Best Time to Buy and Sell Stock (#121), Valid Anagram (#242), Contains Duplicate (#217), Reverse Linked List (#206), Binary Search (#704). Danh sách NeetCode 150 là lộ trình tốt.

## 8. Prompt cho AI voice — Mock interview #3 (coding)

```
You are a software engineer at an international tech company, running a
30-minute coding interview with me. I'm a Java developer with B1 English.
I will write code in a separate editor and read/explain it to you.

1. Give me ONE LeetCode easy-level problem (not Two Sum). Describe it verbally
   like a real interviewer, without giving all the details - let me ask
   clarifying questions.
2. Answer my clarifying questions realistically.
3. When I explain my approach, push back once (e.g. "Can you do better?" or
   "What about memory?").
4. If I'm silent for too long, remind me: "Can you tell me what you're thinking?"
5. If I'm stuck, give a small hint, not the solution.
6. After I finish, ask about time and space complexity and one follow-up question.

At the end, give feedback on:
- Communication: did I clarify, explain my approach before coding, test my code?
- Did I explain complexity correctly in English?
- Phrases I used well, and phrases I should learn.
- Score 1-5 for problem solving and 1-5 for communication.
```

## 9. Checklist tự đánh giá

- [ ] Nhắc lại đề bằng lời của mình
- [ ] Hỏi ít nhất 3 câu clarify (input size, edge cases, output format)
- [ ] Tự đưa ví dụ, kể cả edge case
- [ ] Nói brute force + độ phức tạp trước
- [ ] Hỏi "Does that sound good?" trước khi code
- [ ] Không im lặng quá 30 giây liên tục
- [ ] Giải thích **ý** khi code, không đọc từng ký tự
- [ ] Chạy tay ít nhất 1 ví dụ + 1 edge case
- [ ] Nói đúng time **và** space complexity
- [ ] Đọc đúng "O of n squared", "O of log n"
- [ ] Phát âm đúng: array, integer, indices, iterate

## 10. Tài liệu tham khảo

- LeetCode: https://leetcode.com
- NeetCode (lộ trình + video giải thích bằng tiếng Anh — rất tốt để shadow): https://neetcode.io
- Tech Interview Handbook — coding interview cheatsheet, mẫu câu: https://www.techinterviewhandbook.org
- Pramp — phỏng vấn coding thử với người thật: https://www.pramp.com
