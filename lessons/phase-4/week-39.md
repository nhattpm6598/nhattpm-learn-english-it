# Tuần 39 — Tổng kết và kế hoạch duy trì

> Checklist gốc: [phase-4-interview.md](../../phase-4-interview.md#tuần-39--tổng-kết)

## 1. Mục tiêu tuần này

- Làm lại **EF SET**, so sánh với tuần 0.
- Viết **bản tổng kết** 9 tháng (bằng tiếng Anh — đây cũng là bài luyện viết).
- Lập **kế hoạch duy trì** để không mất những gì đã học.
- Tiếp tục **phỏng vấn thật**.
- Chuẩn bị tiếng Anh cho **những tuần đầu ở công ty quốc tế** (stand-up, 1-1, Slack).
- Đạt **mốc kiểm tra cuối**.

## 2. EF SET — làm lại và so sánh

- Làm bài EF SET 50 phút (đọc + nghe) trong điều kiện giống tuần 0: cùng giờ trong ngày, yên tĩnh, không tra từ.
- Ghi vào `log/progress.md`:

```
EF SET tuần 0:  __/100 (CEFR __)   Reading __  Listening __
EF SET tuần 39: __/100 (CEFR __)   Reading __  Listening __
Thay đổi:       +__
```

> Lưu ý: EF SET chỉ đo **đọc và nghe**. Tiến bộ lớn nhất của 9 tháng nằm ở **nói**, nên hãy dùng thêm bảng so sánh video (tuần 38) làm thước đo.

## 3. Viết tổng kết (bằng tiếng Anh)

### 3.1. Khung

1. **Where I started** — trình độ, khó khăn lúc đầu.
2. **What I did** — số giờ, số buổi mock, số phỏng vấn thật.
3. **What improved** — có số liệu.
4. **What's still weak** — thành thật.
5. **What worked / didn't work** — phương pháp.
6. **Next steps**.

### 3.2. Bài mẫu (~300 từ)

> **My 9-month English journey — summary**
>
> **Where I started.** Nine months ago, my English was around A2. I could read technical documentation, but I couldn't hold a conversation. In my first recording, my 1-minute introduction had long pauses, and I dropped almost every final sound.
>
> **What I did.** I studied about one hour a day, six days a week — roughly 230 hours in total. I did around 120 Anki sessions, more than 40 sessions with a tutor, 10 full mock interviews, and 3 real interviews in English.
>
> **What improved.** My EF SET score went from 38 to 61 (A2 to B2). More importantly, I can now speak for 45 minutes in an interview. My filler words dropped from about 12 per minute to 3, and I can explain a system design with trade-offs, which I couldn't do even in Vietnamese at this level before. I also got to the final round at one company.
>
> **What's still weak.** Listening to fast native speakers, especially in group conversations, is still hard for me. My grammar gets worse when I'm tired or nervous — mostly past tense and articles. And I still need to think before using idioms.
>
> **What worked.** Speaking out loud every day, recording myself, and doing mock interviews with strangers. Writing my answers in `answers.md` but practicing from keywords, not memorizing, was also very effective.
>
> **What didn't work.** Watching long videos passively. I learned more from 10 minutes of shadowing than from one hour of watching.
>
> **Next steps.** Keep practicing 30 minutes a day, focus on listening to fast conversations, and keep interviewing until I get an offer I'm excited about.

## 4. Kế hoạch duy trì

### 4.1. Phiên bản "đang đi phỏng vấn" (45'/ngày)

| Thời gian | Việc |
| --- | --- |
| 10' | Shadowing (podcast/talk kỹ thuật) |
| 5' | Anki (cụm phỏng vấn + từ mới từ phỏng vấn thật) |
| 30' | Luyện 1 câu hỏi từ question-bank / 1 bài coding nói to / 1 system design rút gọn |
| Tuần | 1 mock interview (gia sư/Pramp/AI) + phỏng vấn thật |

### 4.2. Phiên bản "đã có việc" (30'/ngày)

| Thời gian | Việc |
| --- | --- |
| 10' | Nghe: podcast/tech talk khi đi đường |
| 5' | Anki |
| 15' | Viết hoặc nói: tóm tắt 1 cuộc họp, 1 bài blog kỹ thuật, ghi âm 2 phút |
| Tuần | 1 buổi gia sư (45') tập trung vào tình huống công việc thật |
| Tháng | 1 bài viết ngắn (blog nội bộ, LinkedIn post, README) bằng tiếng Anh |

### 4.3. Mục tiêu 6 tháng tới (ví dụ)

- [ ] Trình bày 1 tech talk 15 phút bằng tiếng Anh (nội bộ hoặc meetup)
- [ ] Viết 3 bài LinkedIn/blog kỹ thuật
- [ ] Tham gia 1 cuộc họp nhóm và đóng góp ít nhất 3 ý mà không chuẩn bị trước
- [ ] EF SET +5 điểm

## 5. Tiếng Anh cho những tuần đầu ở công ty quốc tế

### 5.1. Daily stand-up (mẫu)

> "Yesterday, I finished the API for the refund status endpoint and opened a PR — it's ready for review. Today, I'm going to work on the integration tests and then start on the Kafka consumer. No blockers for now, but I might need help from someone on the platform team with the topic permissions later today."

> **Khi có blocker:** "I'm blocked on the staging deployment — the pipeline fails on the database migration step. I've checked the logs, but I'm not sure if it's a permission issue. Could someone who knows the pipeline pair with me for 15 minutes after the stand-up?"

### 5.2. Tin nhắn Slack hay dùng

| Tình huống | Mẫu |
| --- | --- |
| Hỏi giúp đỡ | "Hey @Tom, quick question about the payment client: is there a reason we don't retry on 503? Happy to jump on a call if it's easier." |
| Xin review | "Hi team, could someone review this PR when you have a moment? It's a small change to the retry logic (~80 lines). Thanks!" |
| Báo sự cố | "Heads-up: error rate on the checkout API is up to 5% since 14:20. Investigating now, will post updates in #incident-123." |
| Đồng ý với góp ý review | "Good catch, thanks! Fixed in the latest commit." |
| Phản biện review lịch sự | "I see your point. I went with X because of Y, but I'm happy to change it if you feel strongly. What do you think?" |
| Hỏi lại khi không hiểu | "Sorry, I'm not sure I follow — do you mean we should change the API contract, or just the implementation?" |
| Cập nhật tiến độ | "Quick update: the migration is done on staging. I'll run it on production tomorrow morning, after the 10 a.m. release." |
| Xin thêm thời gian | "This is taking longer than I expected because of X. I think I'll need until Thursday. Does that still work?" |

### 5.3. 1-on-1 với manager (tuần đầu)

- "What would you like me to focus on in my first month?"
- "How do you prefer to communicate — Slack, email, or a quick call?"
- "Who are the key people I should meet in the first few weeks?"
- "How will we know if my first 90 days have gone well?"
- "I'd appreciate direct feedback, especially early on — including on my communication."

### 5.4. Trong cuộc họp

- Xin phát biểu: "Can I add something here?" / "Sorry to jump in, but..."
- Đồng ý một phần: "I agree with most of that, but I have a concern about..."
- Đề xuất: "What if we tried...?" / "One option could be..."
- Xác nhận việc cần làm: "So, just to recap: I'll do X by Friday, and Tom will check Y. Is that right?"
- Không theo kịp: "Sorry, could you go back to the previous point? I want to make sure I understood it."

## 6. Mốc kiểm tra cuối (theo README)

- [ ] 10 buổi phỏng vấn thử (đếm trong `log/progress.md`)
- [ ] Ít nhất 1 buổi phỏng vấn thật bằng tiếng Anh
- [ ] `interview/answers.md` đầy đủ: intro, why leaving, why us, 3 dự án, 6 STAR, strengths/weaknesses, câu hỏi cho interviewer
- [ ] Làm lại EF SET, ghi điểm
- [ ] Viết tổng kết (mục 3)
- [ ] Kế hoạch duy trì (mục 4)

## 7. Cụm từ hữu ích (30)

| # | English | Nghĩa |
| --- | --- | --- |
| 1 | Yesterday I finished..., today I'm going to... | Mẫu stand-up |
| 2 | No blockers for now. | Không có vướng mắc |
| 3 | I'm blocked on... | Bị chặn bởi |
| 4 | Could someone pair with me on...? | Ai đó làm cùng |
| 5 | It's ready for review. | Sẵn sàng review |
| 6 | when you have a moment | Khi bạn rảnh |
| 7 | Quick question about... | Câu hỏi nhanh |
| 8 | Happy to jump on a call. | Sẵn sàng gọi |
| 9 | Heads-up: ... | Báo trước / lưu ý |
| 10 | Good catch, thanks! | Phát hiện hay |
| 11 | I'm happy to change it if you feel strongly. | Sẵn lòng sửa nếu bạn thấy cần |
| 12 | I'm not sure I follow. | Tôi chưa theo kịp |
| 13 | It's taking longer than I expected. | Lâu hơn dự kiến |
| 14 | Does that still work? | Vẫn ổn chứ? |
| 15 | Can I add something here? | Tôi bổ sung được không |
| 16 | Sorry to jump in, but... | Xin lỗi ngắt lời |
| 17 | I have a concern about... | Tôi lo ngại về |
| 18 | What if we tried...? | Nếu thử ... thì sao |
| 19 | Just to recap, ... | Tóm tắt lại |
| 20 | action items / owners / deadline | Đầu việc / người phụ trách / hạn |
| 21 | Let's take this offline. | Bàn riêng sau |
| 22 | Let's circle back to this next week. | Quay lại tuần sau |
| 23 | I'll follow up on that. | Tôi sẽ theo dõi việc đó |
| 24 | Could you go back to the previous point? | Quay lại ý trước |
| 25 | What would you like me to focus on? | Tôi nên tập trung vào gì |
| 26 | I'd appreciate direct feedback. | Mong góp ý thẳng |
| 27 | ramp up / onboarding | Làm quen / hội nhập |
| 28 | It's on my radar. | Tôi đã để ý việc đó |
| 29 | I'll keep you posted. | Tôi sẽ cập nhật |
| 30 | Thanks for the context, that helps a lot. | Cảm ơn bối cảnh |

## 8. Lỗi người Việt hay mắc khi bắt đầu làm ở team quốc tế

1. **Im lặng trong họp** vì sợ sai → người khác nghĩ bạn không có ý kiến. Đặt mục tiêu: mỗi cuộc họp nói ít nhất 1 câu.
2. **Nói "Yes" khi chưa hiểu** → làm sai việc. Luôn recap: "Just to confirm, you want me to..."
3. **Tin nhắn Slack quá trang trọng hoặc quá cụt**: "Dear anh Tom, ..." / "fix?" → Dùng mẫu mục 5.2.
4. **Hỏi "Can I ask you a question?" rồi đợi** → hỏi luôn câu hỏi trong một tin nhắn (không "hello" rồi đợi).
5. **Ngừng luyện tiếng Anh khi đã có việc** → trình độ chững lại sau 3–6 tháng. Duy trì 30'/ngày.

## 9. Lịch trong tuần

| Ngày | Việc |
| --- | --- |
| T2 | Làm lại EF SET, ghi điểm, so với tuần 0. |
| T3 | Viết tổng kết theo khung mục 3 (tiếng Anh). Nhờ AI sửa, đọc to bản đã sửa. |
| T4 | Viết kế hoạch duy trì (mục 4). Chọn phiên bản phù hợp. |
| T5 | Phỏng vấn thật / luyện mục 5 (stand-up, Slack, meeting). |
| T6 | Phỏng vấn thật / mock tự do. |
| T7 | **Mốc kiểm tra cuối** (mục 6). Nhật ký giai đoạn. Ăn mừng! |

## 10. Prompt cho AI voice — luyện tình huống công việc

```
I just joined an international software team as a Senior Backend Engineer.
My English is B1-B2. Role-play my first week with me. Play these roles one
at a time, and speak naturally:

1. My engineering manager in our first 1-on-1. Ask what I want to focus on
   and tell me about the team. Let me ask questions.
2. A teammate in a daily stand-up. Ask for my update, then ask a follow-up
   about a blocker I mention.
3. A senior engineer who left a critical code review comment on my PR,
   saying my retry logic could cause duplicate payments. Discuss it with me.
4. A product manager who wants a feature earlier than I think is possible.

After each role-play, give me 3 corrections and 1 more natural way to say
something I said.
```

**Prompt viết tổng kết:**

```
Here is my 9-month English learning summary (written by me, B1-B2 level).
Please correct grammar and make it sound natural, but keep my voice and
keep it simple. Then list my 5 most common mistakes so I can practice them.
[paste your summary]
```

## 11. Checklist tự đánh giá

- [ ] Đã làm EF SET và ghi điểm
- [ ] Bản tổng kết có số liệu (giờ học, số mock, điểm, filler words)
- [ ] Liệt kê thành thật điểm còn yếu
- [ ] Kế hoạch duy trì cụ thể (phút/ngày, buổi/tuần)
- [ ] Nói được 1 bản stand-up tự nhiên không nhìn giấy
- [ ] Viết được 3 tin nhắn Slack mẫu cho tình huống của mình
- [ ] Mốc kiểm tra cuối: tất cả đã tick

## 12. Tài liệu tham khảo

- Tech Interview Handbook: https://www.techinterviewhandbook.org
- Levels.fyi (đánh giá offer): https://www.levels.fyi
- ByteByteGo — tiếp tục học system design: https://bytebytego.com · https://www.youtube.com/@ByteByteGo
- NeetCode — duy trì kỹ năng coding: https://neetcode.io
