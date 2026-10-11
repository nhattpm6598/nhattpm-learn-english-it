# Tuần 29 — STAR: câu hỏi hành vi (1)

> Checklist gốc: [phase-4-interview.md](../../phase-4-interview.md#tuần-29--star-câu-hỏi-hành-vi-1) · Ghi câu chuyện vào bảng STAR trong [interview/answers.md](../../interview/answers.md#câu-chuyện-star)

## 1. Mục tiêu tuần này

- Hiểu và dùng thành thạo khung **STAR**.
- Viết và luyện 3 câu chuyện: **xung đột trong team**, **deadline gấp**, **sai lầm và bài học**.
- Hoàn thành **phỏng vấn thử #1** (behavioral).

> Behavioral question = câu hỏi về **hành vi trong quá khứ**, thường bắt đầu bằng: *"Tell me about a time when..."*, *"Give me an example of..."*, *"Describe a situation where..."*, *"Have you ever...?"*. Logic: cách bạn đã hành xử trước đây là dự đoán tốt nhất cho cách bạn sẽ hành xử sau này.

## 2. Khung STAR (+R)

| Phần | Ý nghĩa | Tỉ lệ thời gian | Thì động từ |
| --- | --- | --- | --- |
| **S – Situation** | Bối cảnh: ở đâu, khi nào, ai | ~15% | past simple / past continuous |
| **T – Task** | Nhiệm vụ / vấn đề **của bạn** | ~10% | past simple ("I needed to...", "My job was to...") |
| **A – Action** | Bạn **đã làm gì**, từng bước | **~50–60%** | past simple, chủ ngữ "**I**" |
| **R – Result** | Kết quả (số liệu nếu được) | ~15% | past simple |
| **(+L) – Learning** | Bài học, lần sau làm gì | ~5–10% | present ("Now I always...") |

**Tổng thời lượng:** 1,5–2,5 phút.

**Bí quyết:**
- Phần **Action** là quan trọng nhất. Chia thành 2–4 bước: "First, I... Then, I... Finally, I..."
- Câu chuyện phải **thật** (có thể đơn giản hoá). Interviewer giỏi sẽ hỏi sâu và phát hiện chuyện bịa.
- Câu chuyện **xung đột/sai lầm** phải kết thúc **tích cực** (giải quyết được, học được).
- Một câu chuyện tốt có thể dùng cho nhiều câu hỏi. Ví dụ chuyện "deadline gấp" có thể dùng cho "pressure", "prioritization", "trade-off with product".

## 3. Story bank — câu hỏi nào dùng câu chuyện nào

| Câu chuyện | Dùng cho câu hỏi |
| --- | --- |
| Xung đột trong team | "Tell me about a disagreement with a colleague", "...with your manager", "How do you handle conflict?", "Tell me about a time you had to persuade someone" |
| Deadline gấp | "Working under pressure", "Tight deadline", "How do you prioritize?", "A time you had to cut scope" |
| Sai lầm | "Tell me about a mistake / failure", "A time you received critical feedback", "What would you do differently?" |

## 4. Model answers

### 4.1. Xung đột trong team — "Tell me about a time you disagreed with a colleague."

> **Situation:** "In my current company, about a year ago, we were designing a new refund service. A senior colleague on my team, who had been at the company longer than me, wanted to call the payment provider synchronously from the API and return the result immediately.
>
> **Task:** I was the one writing the design document, and I was worried about that approach. The provider sometimes took up to 30 seconds to respond, and if it timed out, we wouldn't know if the refund had happened or not. I needed to raise this without making it personal, and we needed a decision within a week.
>
> **Action:** First, I asked him for a one-on-one call instead of arguing in the team channel. I started by asking about his reasons, and I learned that his main concern was simplicity — he didn't want to add a queue and more moving parts for a small feature. That was a fair point.
>
> Then, instead of just giving my opinion, I collected data: I pulled the provider's response times from our logs for the last month. The p99 was 18 seconds, and about 0.5 percent of calls timed out. I showed him that with the synchronous design, we'd have roughly 50 refunds per day in an unknown state, which support would have to fix manually.
>
> Finally, I suggested a middle ground: keep the API simple for the client — it returns 'refund accepted' immediately — but process the refund asynchronously with a status we can poll, and use an idempotency key so retries are safe. I also offered to write the extra code myself.
>
> **Result:** He agreed after seeing the numbers, and we presented the design together to the team. Since launch, we've had zero refunds stuck in an unknown state. And actually, our relationship became better — he later asked me to review his designs.
>
> **Learning:** What I learned is that in technical disagreements, data works much better than opinions, and it's important to understand the other person's concern first — usually it's a valid concern."

### 4.2. Deadline gấp — "Tell me about a time you worked under a tight deadline."

> **Situation:** "Last year, our company signed a contract with a big retail partner. Two weeks before launch, the partner told us they needed a reconciliation report API — a daily file of all transactions — which wasn't in the original scope. Without it, they wouldn't go live.
>
> **Task:** I was asked to deliver it in ten working days, while also finishing my other sprint work. Normally a feature like that would take us three to four weeks.
>
> **Action:** First, I set up a 30-minute call with the partner's tech team to understand the real minimum requirements. It turned out they needed only CSV format and only five fields for the first version — not the full spec of twenty fields.
>
> Second, I talked with my manager and the product owner to reprioritize. We agreed to move two of my lower-priority tickets to the next sprint, so I could focus.
>
> Third, I split the work into small pieces and reused our existing reporting job framework with Spring Batch instead of building something new. I asked a teammate to help with the SFTP upload part, so we could work in parallel.
>
> And I sent a short status update to everyone every two days, so there were no surprises.
>
> **Result:** We delivered the first version in eight working days, two days before the deadline, and the partner went live on time. That partner now brings us about 15 percent of our monthly transaction volume. We added the remaining fields in the next month.
>
> **Learning:** The biggest lesson for me was that under pressure, the most valuable thing is to clarify the real minimum requirement. Often the scope can be cut much more than people think."

### 4.3. Sai lầm và bài học — "Tell me about a mistake you made."

> **Situation:** "About two years ago, I was working on a database migration for our user service. I wrote a Flyway migration that added a new column with a default value and a NOT NULL constraint to a table with about 40 million rows.
>
> **Task:** It was my task, and I tested it on our staging environment, where it ran in a few seconds — but staging only had about 100,000 rows.
>
> **Action / what happened:** When it ran in production during a normal deployment, the table was locked for almost four minutes on our older database version. During that time, logins failed for a lot of users. I noticed the alerts right away, so I told my team lead immediately in the incident channel — I didn't try to hide it. We decided not to kill the migration because rolling back could take even longer, and it finished a few minutes later.
>
> After the incident, I wrote the post-mortem myself. I explained the root cause honestly: I assumed staging was representative, but it wasn't. Then I proposed three changes: first, a checklist for risky migrations on big tables; second, we test heavy migrations on a copy of production-sized data; and third, we split changes like this into several steps — add a nullable column, backfill in batches, then add the constraint.
>
> **Result:** The team adopted all three changes. Since then, we've done more than 30 large-table migrations without any downtime.
>
> **Learning:** I learned two things. Technically, never assume staging behaves like production for data size. And personally, owning a mistake quickly and openly is much better than trying to fix it quietly — the team trusted me more after that, not less."

**Lưu ý khi nói về sai lầm:**
- Chọn sai lầm **thật** nhưng **không phải thảm hoạ** (không làm mất dữ liệu khách hàng, không vi phạm bảo mật).
- Nhận trách nhiệm: "**I** made a mistake" — không đổ lỗi ("the QA didn't catch it").
- Phần lớn thời gian dành cho **bạn đã làm gì để sửa và ngăn lặp lại**.

## 5. Cụm từ hữu ích (35)

| # | English | Nghĩa |
| --- | --- | --- |
| 1 | Sure, let me think of a good example. | Câu "mua thời gian" tự nhiên |
| 2 | One situation that comes to mind is... | Một tình huống tôi nhớ ra là |
| 3 | This was back in 2023, when I was working at... | Bối cảnh thời gian |
| 4 | At the time, I was... | Lúc đó tôi đang |
| 5 | My task was to... / I was responsible for... | Nhiệm vụ |
| 6 | The challenge was that... | Thách thức là |
| 7 | I was worried that... / My concern was that... | Lo ngại |
| 8 | We had a different opinion on... | Có ý kiến khác nhau về |
| 9 | I asked for a quick one-on-one call. | Gặp riêng |
| 10 | I wanted to understand his point of view first. | Hiểu quan điểm người kia |
| 11 | That was a fair point. | Đó là ý hợp lý |
| 12 | Instead of arguing, I collected some data. | Thay vì tranh cãi |
| 13 | I suggested a middle ground / a compromise. | Phương án dung hoà |
| 14 | We agreed to... | Chúng tôi thống nhất |
| 15 | We ended up... | Cuối cùng chúng tôi |
| 16 | First, ... Then, ... After that, ... Finally, ... | Trình tự Action |
| 17 | It turned out that... | Hoá ra |
| 18 | I reprioritized / We cut the scope to... | Ưu tiên lại / cắt phạm vi |
| 19 | I pushed back on... (politely) | Phản đối (lịch sự) |
| 20 | I kept everyone in the loop. | Cập nhật cho mọi người |
| 21 | I sent a status update every two days. | Cập nhật tiến độ |
| 22 | I made a mistake. / That was my mistake. | Nhận lỗi |
| 23 | I took full ownership of it. | Nhận trách nhiệm hoàn toàn |
| 24 | I raised it immediately. | Báo ngay |
| 25 | I wrote a post-mortem. | Viết báo cáo sau sự cố |
| 26 | The root cause was... | Nguyên nhân gốc |
| 27 | To prevent this from happening again, ... | Để không lặp lại |
| 28 | As a result, ... / In the end, ... | Kết quả |
| 29 | We delivered it two days ahead of schedule. | Giao sớm 2 ngày |
| 30 | The relationship actually improved. | Mối quan hệ tốt hơn |
| 31 | What I learned from this is... | Bài học |
| 32 | Since then, I always... | Từ đó tôi luôn |
| 33 | Looking back, I should have... | Nhìn lại, lẽ ra tôi nên |
| 34 | I'd handle it the same way again. | Sẽ làm y như vậy |
| 35 | Does that answer your question? | Kiểm tra lại |

## 6. Lỗi người Việt hay mắc

1. **Trả lời giả định** thay vì kể chuyện thật: "I would talk to him and..." → Câu hỏi là "Tell me about **a time**" → phải kể chuyện **đã xảy ra**: "I **talked** to him..."
2. **Bỏ qua Action, nói nhiều Situation:** 1 phút kể bối cảnh, 10 giây hành động.
3. **"We" thay vì "I"** — đặc biệt với văn hoá tập thể của người Việt. Ở công ty nước ngoài, nói "I" **không bị coi là khoe**.
4. **Chọn xung đột không có xung đột thật** ("We never have conflict in my team") → interviewer nghĩ bạn né tránh.
5. **Đổ lỗi** cho đồng nghiệp/sếp/QA trong câu chuyện sai lầm.
6. **Chọn "điểm yếu giả"** làm sai lầm: "My mistake is I work too hard." → nghe không thật.
7. **Thiếu đuôi -ed:** "I talk to him and we decide..." → "I talk**ed** /tɔːkt/ to him and we decid**ed** /dɪˈsaɪdɪd/". Ba cách đọc -ed: /t/ (worked, fixed), /d/ (planned, agreed), /ɪd/ (decided, wanted, needed).
8. **Không có kết thúc:** Câu chuyện dừng ở Action. Luôn thêm "As a result..." và "What I learned...".

## 7. Lịch luyện trong tuần

| Ngày | Việc cụ thể |
| --- | --- |
| T2 | Đọc mục 2, xem story bank mục 3. Viết chuyện **xung đột** theo STAR (gạch đầu dòng, không viết văn). Nói 5 lần. |
| T3 | Viết + nói chuyện **deadline gấp**. |
| T4 | Viết + nói chuyện **sai lầm**. Ghi âm cả 3. |
| T5 | **Phỏng vấn thử #1**: dùng prompt mục 8 hoặc nhờ gia sư. Quay video. |
| T6 | Xem lại video với checklist mục 9. Sửa câu trả lời trong answers.md. |
| T7 | Ôn + nhật ký tuần. |

**Viết STAR dạng gạch đầu dòng (ví dụ):**
```
S: refund service design, senior colleague wants sync call
T: I write design doc; provider slow (30s), timeout -> unknown state
A1: 1-1 call, ask his reasons -> simplicity
A2: data: p99 18s, 0.5% timeout = ~50/day unknown
A3: middle ground: async + status polling + idempotency key; I write extra code
R: agreed, 0 stuck refunds, better relationship
L: data > opinion; understand concern first
```

## 8. Prompt cho AI voice — Mock interview #1 (behavioral)

```
Act as an interviewer from a big international tech company running a
30-minute behavioral interview for a Senior Software Engineer role.
I am a Vietnamese Java backend engineer, English level B1.

Ask me these 4 questions, one at a time:
1. Tell me about a time you disagreed with a teammate. How did you handle it?
2. Tell me about a time you had to deliver something under a very tight deadline.
3. Tell me about a mistake you made at work and what you learned.
4. Tell me about a time you received critical feedback.

After each of my answers, ask 1-2 realistic follow-up questions
(e.g. "What would you do differently?", "What did your manager say?",
"What exactly was YOUR part?").

Don't give feedback until the end. Then, for EACH answer, tell me:
- Did I follow STAR? Which part was weak or missing?
- Did I use "I" enough, or too much "we"?
- Was the result clear and measurable?
- Grammar mistakes, especially past tense (-ed) mistakes, with corrections.
- A score from 1 to 5 as a real interviewer would give.
```

## 9. Checklist tự đánh giá

- [ ] Mỗi câu chuyện có đủ **S – T – A – R** (+ Learning)
- [ ] Action chiếm ít nhất một nửa thời lượng
- [ ] Action chia thành bước rõ ràng (First / Then / Finally)
- [ ] Dùng **"I"** cho hành động của mình
- [ ] Động từ **quá khứ** đúng, đọc rõ đuôi -ed
- [ ] Result có số liệu hoặc kết quả cụ thể
- [ ] Chuyện xung đột: không nói xấu đồng nghiệp, thể hiện sự tôn trọng
- [ ] Chuyện sai lầm: nhận trách nhiệm, không đổ lỗi
- [ ] Mỗi câu chuyện 1,5–2,5 phút
- [ ] Trả lời được follow-up mà không mâu thuẫn với câu chuyện

## 10. Tài liệu tham khảo

- Tech Interview Handbook — Behavioral interview, STAR: https://www.techinterviewhandbook.org
- Pramp (có cả behavioral mock): https://www.pramp.com
