# Tuần 36 — Phỏng vấn trọn vòng (1)

> Checklist gốc: [phase-4-interview.md](../../phase-4-interview.md#tuần-36--phỏng-vấn-trọn-vòng-1)

## 1. Mục tiêu tuần này

- Ôn lại toàn bộ [interview/answers.md](../../interview/answers.md) — đảm bảo mọi mục đã có nội dung.
- **Phỏng vấn thử #8**: 45 phút, đủ các phần (intro, behavioral, technical, mini system design/coding, câu hỏi ngược).
- Xác định **phần yếu nhất** và luyện có chủ đích 2 ngày.
- Luyện kỹ năng **chuyển tiếp** giữa các phần và **giữ năng lượng** suốt 45 phút.

> Từ tuần 36, bạn không học nội dung mới nữa. Mục tiêu là **ghép mọi thứ lại** và luyện **độ bền**: nói tiếng Anh 45 phút liên tục mệt hơn nhiều so với 5 phút.

## 2. Cấu trúc một vòng phỏng vấn 45 phút điển hình

| Phút | Phần | Bạn cần |
| --- | --- | --- |
| 0–3 | Small talk + giới thiệu interviewer | Thoải mái, chào hỏi tự nhiên |
| 3–6 | Tell me about yourself | Bản 1–2 phút (tuần 27) |
| 6–18 | Behavioral / dự án | 2–3 câu chuyện STAR + 1 dự án (tuần 28–30) |
| 18–35 | Technical: Java/Spring Q&A **hoặc** coding **hoặc** system design | Tuần 31–34 |
| 35–42 | Your questions | 3 câu hỏi (tuần 35) |
| 42–45 | Closing | Cảm ơn, hỏi bước tiếp theo |

## 3. Mẫu hội thoại đầy đủ (transcript rút gọn)

> Đọc to đoạn hội thoại này, **đóng vai Candidate**. Sau đó che phần Candidate và tự trả lời.

**[Small talk]**

> **Interviewer:** Hi, can you hear me okay?
> **Candidate:** Yes, I can hear you clearly. Can you hear me?
> **Interviewer:** Yes, perfect. How's your day going?
> **Candidate:** Pretty good, thanks. It's evening here in Vietnam, so I've finished work for the day. How about you?
> **Interviewer:** Good, it's morning here in Berlin, so I've just had my coffee. So, I'm Anna, I'm an engineering manager on the payments team. The plan for today: I'll ask about your background, a couple of experience questions, then we'll spend about 15 minutes on a technical discussion, and leave time for your questions at the end. Sound good?
> **Candidate:** Sounds great. Thanks for the introduction.

**[Intro]**

> **Interviewer:** Great. So, tell me a bit about yourself.
> **Candidate:** *(bản 1–2 phút của bạn — tuần 27)*

**[Behavioral]**

> **Interviewer:** Thanks. You mentioned the transaction history service. What was the hardest part of that project?
> **Candidate:** I'd say the hardest part wasn't technical — it was getting the time to do it. It wasn't on the roadmap, so I had to convince our product manager. I took two days to measure the impact: I showed that slow history pages generated about 300 support tickets a month and that the load on the primary database was putting payments at risk. With that data, she agreed to give us one sprint for the first phase, and the results from that phase got us the time for the rest.
>
> **Interviewer:** Nice. Tell me about a time you disagreed with your manager.
> **Candidate:** Sure. Let me think of a good example... *(STAR — có thể dùng lại câu chuyện xung đột tuần 29, điều chỉnh nhân vật cho phù hợp)*

**[Technical transition]**

> **Interviewer:** Okay, let's switch to something more technical. Imagine we have a payment service, and we've noticed that sometimes customers get charged twice. How would you investigate and fix that?
> **Candidate:** Okay, interesting. Let me first make sure I understand: the customer clicks pay once, or possibly twice, and the charge happens twice at the payment provider? … Got it.
>
> I'd start by investigating: I'd look at logs and traces for a few affected payments to see where the duplicate comes from. There are a few usual suspects: the client retrying after a timeout — for example, a mobile app on a bad network; the user double-clicking; our service retrying the call to the provider after a timeout when the first call actually succeeded; or a message consumer processing the same event twice.
>
> For the fix, the key concept is **idempotency**. The client generates an **idempotency key** — a UUID — per payment attempt and sends it in a header. On the server, we store the key with a unique constraint, together with the request status and the response. If the same key comes again, we return the stored result instead of charging again. If the first request is still in progress, we return a 409 or ask the client to retry later.
>
> We should also pass an idempotency key to the payment provider — most providers like Stripe support that — so that our own retries are safe too. And on the frontend, disable the pay button after the first click, but that's just a UX improvement, not the real protection.
>
> Finally, I'd add a reconciliation job that compares our records with the provider's reports daily, and alerts on duplicates, so we catch any remaining cases.
>
> **Interviewer:** How long would you keep the idempotency keys?
> **Candidate:** It depends on how long clients might retry. Usually 24 hours is enough — Stripe, for example, keeps them for 24 hours. We could store them in the database with a TTL clean-up job, or in Redis with an expiry, but for payments I'd prefer the database, because it's durable and we can write the key in the same transaction as the payment record.

**[Your questions]**

> **Interviewer:** Great, we have about eight minutes left. What questions do you have for me?
> **Candidate:** Thanks. First, could you tell me about the biggest challenge your team is facing in the next six months?
> **Interviewer:** *(trả lời)*
> **Candidate:** That makes sense. And how do you measure success for a senior engineer in the first six months?
> **Interviewer:** *(trả lời)*
> **Candidate:** Thanks, that's really helpful. Last question: what are the next steps in the process?

**[Closing]**

> **Interviewer:** We'll get back to you within a week, and the next step would be a system design round.
> **Candidate:** Perfect. Thank you so much for your time, Anna. I really enjoyed the conversation, especially learning about the payment reconciliation work. Have a great day!

## 4. Kỹ năng chuyển tiếp & giữ nhịp

### 4.1. Cụm từ chuyển tiếp (Transitions)

| Tình huống | Cụm từ |
| --- | --- |
| Bắt đầu trả lời | "Sure." / "Good question." / "Happy to." |
| Cần thời gian | "Let me think about that for a second." / "That's a great question — let me think of the best example." |
| Chuyển ý | "Moving on to..." / "Another thing I'd mention is..." / "On top of that, ..." |
| Quay lại ý chính | "Coming back to your question, ..." / "So, to answer your question directly, ..." |
| Kết thúc câu trả lời | "So that's how I approached it." / "...and that's the main lesson I took from it." |
| Kiểm tra | "Did that answer your question?" / "Would you like more detail on any part?" |
| Interviewer ngắt lời | "Sure, go ahead." / "Good point — ..." |
| Không nghe rõ | "Sorry, could you repeat the last part?" / "I think the connection cut out for a second — could you say that again?" |
| Không hiểu câu hỏi | "Just to make sure I understand — are you asking about X or Y?" |

### 4.2. Giữ năng lượng 45 phút

- **Uống nước** khi interviewer nói dài — hoàn toàn bình thường.
- **Đứng hoặc ngồi thẳng**, giọng sẽ rõ hơn.
- **Ghi chú từ khoá** câu hỏi lên giấy khi interviewer hỏi câu dài (vd: "challenge — team — result").
- Nếu nói sai: **tự sửa nhanh** và đi tiếp: "Sorry, I mean ..." — không dừng lại xin lỗi.
- Phút 30 trở đi, người học tiếng Anh hay **giảm chất lượng ngữ pháp** do mệt. Luyện mock dài là cách duy nhất để quen.

## 5. Cách xem lại video (review) — phương pháp 3 lượt

| Lượt | Tập trung vào | Ghi chép |
| --- | --- | --- |
| **1. Nội dung** | Có trả lời đúng câu hỏi không? Có cấu trúc (STAR, D-E-E-T, 5 bước)? | Câu nào trả lời lạc đề / thiếu ý |
| **2. Ngôn ngữ** | Ngữ pháp, từ vựng, âm cuối, từ phát âm sai | 10 lỗi cụ thể + câu đúng |
| **3. Giao tiếp** | Ánh mắt, tốc độ, khoảng lặng, "ừm/ờ", năng lượng | Thời điểm (phút:giây) cần sửa |

**Bảng chấm điểm (copy vào log/progress.md):**

```
Mock #8 — ngày ...
Intro:            _/5   Ghi chú:
Behavioral:       _/5
Technical:        _/5
Questions asked:  _/5
Fluency:          _/5   (số lần "ừm": ___ / số lần im lặng > 5s: ___)
Pronunciation:    _/5   (từ sai: ...)
Grammar:          _/5   (lỗi hay gặp: ...)
Phần yếu nhất:
Kế hoạch luyện T5–T6:
```

## 6. Luyện phần yếu nhất — bài tập có chủ đích

| Nếu yếu ở | Bài tập 30 phút |
| --- | --- |
| **Intro** | Nói 10 lần với 10 "công ty" khác nhau, thay câu kết nối cuối. |
| **STAR** | Chọn 1 câu chuyện, kể 3 lần: lần 1 trong 3 phút, lần 2 trong 2 phút, lần 3 trong 1 phút. Buộc bạn chọn ý chính. |
| **Kỹ thuật** | Chọn 5 câu từ question-bank, ghi âm mỗi câu, nghe lại so với đáp án mẫu. |
| **Coding** | 1 bài LeetCode Easy, nói to, không được im lặng > 20s. |
| **System design** | Chỉ luyện phần "deep dive + trade-off" của 1 bài trong 10'. |
| **Nghe hiểu** | Nghe 1 video mock interview, dừng sau mỗi câu hỏi, tự trả lời trước khi nghe candidate. |
| **Ngữ pháp (thì quá khứ)** | Kể lại 3 câu chuyện STAR, đếm số động từ quá khứ đúng/sai. |
| **Âm cuối** | Shadow 5 phút với video tốc độ 0.75, tập trung -s, -ed, -t, -k. |
| **Ừm/ờ quá nhiều** | Thay "ừm" bằng khoảng lặng 1 giây hoặc "So...", "Well...". Ghi âm 2 phút, đếm. |

## 7. Cụm từ hữu ích (30) — tổng hợp cho vòng đầy đủ

| # | English | Nghĩa |
| --- | --- | --- |
| 1 | Can you hear me okay? | Bạn nghe rõ không? |
| 2 | Sorry, you're breaking up a little. | Tiếng bị ngắt quãng |
| 3 | Thanks for taking the time to talk with me. | Cảm ơn đã dành thời gian |
| 4 | Sounds great. / That works for me. | Nghe ổn |
| 5 | Let me give you a quick overview. | Tổng quan nhanh |
| 6 | Let me think of the best example. | Để tôi chọn ví dụ tốt nhất |
| 7 | The short answer is ..., but let me explain. | Trả lời ngắn là |
| 8 | To give you a concrete example, ... | Ví dụ cụ thể |
| 9 | Let me first make sure I understand the scenario. | Hiểu tình huống |
| 10 | There are a few possible causes. | Có vài nguyên nhân |
| 11 | The usual suspects are ... | Nghi phạm thường gặp |
| 12 | The key concept here is ... | Khái niệm then chốt |
| 13 | That's a UX improvement, not the real protection. | Chỉ là cải thiện UX |
| 14 | It depends on ... | Tuỳ vào |
| 15 | I'd prefer ... because ... | Tôi thích ... vì |
| 16 | On top of that, ... | Thêm vào đó |
| 17 | Coming back to your question, ... | Quay lại câu hỏi |
| 18 | Sorry, I mean ... | Xin lỗi, ý tôi là |
| 19 | Would you like me to go deeper? | Nói sâu hơn không? |
| 20 | Good point. I hadn't thought about that. | Ý hay, tôi chưa nghĩ tới |
| 21 | That makes sense. | Hợp lý |
| 22 | That's really helpful, thank you. | Rất hữu ích |
| 23 | What would the next steps be? | Bước tiếp theo |
| 24 | I really enjoyed our conversation. | Rất thích buổi trao đổi |
| 25 | I'm looking forward to hearing from you. | Mong tin từ bạn |
| 26 | Have a great rest of your day! | Chúc ngày tốt lành |
| 27 | It's evening here, so ... | Ở đây đang tối |
| 28 | Just to clarify — are you asking about X or Y? | Làm rõ câu hỏi |
| 29 | Could you rephrase the question? | Diễn đạt lại câu hỏi |
| 30 | I'll take a quick note, if that's okay. | Tôi ghi chú nhanh |

## 8. Lỗi người Việt hay mắc ở vòng đầy đủ

1. **Mở đầu cứng nhắc**, bỏ qua small talk → trả lời "How are you?" bằng "Fine, thank you, and you?" (sách giáo khoa). Thay bằng "Pretty good, thanks. How about you?" và thêm 1 chi tiết.
2. **Mệt ở phút 30** → câu ngắn cụt, mất cấu trúc. Giải pháp: luyện mock đủ 45 phút.
3. **Không biết dừng** — trả lời quá dài, mất thời gian cho phần kỹ thuật. Mỗi câu behavioral ≤ 2,5 phút.
4. **Quên hỏi lại khi câu hỏi mơ hồ** ở phần kỹ thuật.
5. **Kết thúc vội**: "Okay, bye." → luôn cảm ơn + nhắc 1 điều bạn thích trong buổi nói chuyện.
6. **Không xem lại video** vì ngại nhìn mình. Đây là bước quan trọng nhất của mỗi mock.

## 9. Lịch luyện trong tuần

| Ngày | Việc |
| --- | --- |
| T2 | Ôn toàn bộ answers.md. Điền chỗ còn trống. Đọc to transcript mục 3. |
| T3 | **Phỏng vấn thử #8** — 45', đủ các phần (gia sư hoặc prompt mục 10). Quay video. |
| T4 | Review 3 lượt (mục 5), chấm điểm, ghi vào log. |
| T5 | Luyện phần yếu nhất (mục 6). |
| T6 | Luyện phần yếu nhất (tiếp) + 1 bài khác. |
| T7 | Ôn + nhật ký. |

## 10. Prompt cho AI voice — Mock interview #8 (full loop)

```
You are an engineering manager at a European tech company running a full
45-minute interview for a Senior Backend Engineer (Java, Spring Boot,
microservices, some frontend). My English is B1+. Speak naturally, at normal
speed, like a real interviewer.

Structure:
- 2 min small talk and introduce yourself and the agenda.
- "Tell me about yourself" + 1 follow-up.
- 2 behavioral questions (choose from: conflict, failure, leadership,
  ambiguity, prioritization) with follow-ups.
- 15 min technical scenario discussion: give me a realistic production
  problem (e.g. duplicate payments, a slow endpoint, a memory leak, a Kafka
  consumer lagging) and ask how I'd investigate and fix it. Dig deeper twice.
- 5-7 min for my questions. Answer realistically.
- Close the interview naturally.

Do not give feedback during the interview. At the end, give:
1. A score 1-5 for each section and an overall hire / no-hire.
2. The single weakest area I should practice this week.
3. 10 specific language corrections (what I said -> better version).
4. 3 phrases I used well.
```

## 11. Checklist tự đánh giá

- [ ] Small talk tự nhiên, không theo kiểu sách giáo khoa
- [ ] Intro ≤ 2 phút
- [ ] Mỗi câu behavioral có STAR, ≤ 2,5 phút
- [ ] Phần kỹ thuật: hỏi làm rõ trước khi trả lời
- [ ] Có trade-off trong câu trả lời kỹ thuật
- [ ] Hỏi ít nhất 2 câu cho interviewer + phản hồi câu trả lời của họ
- [ ] Kết thúc lịch sự, có cảm ơn
- [ ] Chất lượng tiếng Anh phút 35–45 không tệ hơn phút 0–10 quá nhiều
- [ ] Đã review 3 lượt và ghi điểm vào log

## 12. Tài liệu tham khảo

- Pramp — mock interview với người thật: https://www.pramp.com
- Tech Interview Handbook: https://www.techinterviewhandbook.org
- ByteByteGo YouTube (shadowing giải thích kỹ thuật): https://www.youtube.com/@ByteByteGo
