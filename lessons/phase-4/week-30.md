# Tuần 30 — STAR: câu hỏi hành vi (2) + Strengths/Weaknesses

> Checklist gốc: [phase-4-interview.md](../../phase-4-interview.md#tuần-30--star-câu-hỏi-hành-vi-2) · Ghi vào [interview/answers.md](../../interview/answers.md)

## 1. Mục tiêu tuần này

- 3 câu chuyện STAR mới: **hướng dẫn junior / dẫn dắt team**, **quyết định kỹ thuật khó**, **xử lý sự cố production**.
- Trả lời 3 câu "kinh điển": **Strengths**, **Weaknesses**, **Where do you see yourself in 5 years?**
- **Phỏng vấn thử #2** (behavioral).

> Với role **Senior**, 3 câu chuyện tuần này đặc biệt quan trọng: interviewer muốn thấy bạn có **leadership** (không cần chức danh), **ra quyết định có cơ sở**, và **bình tĩnh khi có sự cố**.

## 2. Nhắc lại STAR + điểm nhấn cho Senior

| Phần | Senior cần thể hiện thêm |
| --- | --- |
| Situation | Quy mô (team, hệ thống, user) |
| Task | Bạn **tự nhận** việc (ownership), không chỉ được giao |
| Action | Ảnh hưởng tới **người khác** (mentor, thuyết phục, phối hợp nhiều team); cân nhắc **trade-off** |
| Result | Tác động lên **team/tổ chức**, không chỉ code |
| Learning | Thay đổi **quy trình** để cả team tốt hơn |

## 3. Model answers

### 3.1. Mentoring / dẫn dắt — "Tell me about a time you helped a junior developer grow."

> **Situation:** "About a year ago, two junior developers joined my team. One of them, let's call him Minh, was smart but struggled a lot in his first two months. His pull requests often had more than 30 review comments, and he was taking about three times longer than estimated on tickets.
>
> **Task:** My manager asked me to be his mentor. My goal was to help him become independent on normal backend tickets within about three months.
>
> **Action:** First, I wanted to understand the real problem, so I paired with him for a few sessions. I noticed that he jumped into coding immediately without understanding the existing code, and he was afraid to ask questions because he didn't want to look bad.
>
> So I did a few things. I set up a 30-minute one-on-one with him every week, and I told him clearly that asking questions early is a good thing, not a weakness. I introduced a simple habit: before coding any ticket, he writes five or six lines in the ticket about his plan, and I review that first. That way we caught design problems before he wrote 500 lines of code.
>
> I also changed how I did code reviews. Instead of leaving 30 small comments, I grouped them, marked which ones were blocking and which were just suggestions, and for bigger topics I did a short call to explain the 'why'. And I gave him a small but real feature to own end-to-end, so he could build confidence.
>
> **Result:** After about three months, his review comments went down to fewer than five per PR on average, and his estimates became much more accurate. Six months later, he was mentoring the next new joiner himself. The 'plan before coding' habit also got adopted by the whole team.
>
> **Learning:** I learned that mentoring is less about giving answers and more about creating a safe environment where people can ask questions early."

### 3.2. Quyết định kỹ thuật khó — "Tell me about a difficult technical decision you made."

> **Situation:** "At my current company, our order service used a single PostgreSQL database, and we were adding a new feature for real-time order tracking. The product team wanted live updates on the order status for customers and for the operations dashboard.
>
> **Task:** I was the tech lead for this feature, so I had to decide how to push updates to clients. The two main options were WebSockets and simple polling. I had to make a decision that the team could build in six weeks and maintain long term.
>
> **Action:** First, I wrote down the requirements with the product manager. It turned out that 'real-time' actually meant 'within about five seconds' for customers. Only the internal dashboard needed faster updates.
>
> Then I compared the options in a short design document. WebSockets would give instant updates, but we'd need sticky sessions or a pub/sub layer behind the load balancer, connection management on mobile networks, and our team had no experience operating it. Polling every five seconds was simple and worked with our existing caching and infrastructure, but at our scale — about 50,000 concurrent users at peak — that's 10,000 requests per second, which was too much for the database.
>
> So I proposed a hybrid: for customers, polling with a five-second interval, but served from Redis, not the database — the order service writes the latest status to Redis whenever it changes. For the internal dashboard, which has only about 200 users, we used Server-Sent Events, which is simpler than WebSockets because it's one-way and works over normal HTTP.
>
> I presented the document to the team and two architects, listened to their feedback — one of them suggested adding ETags so unchanged responses are cheap — and we went with it.
>
> **Result:** We delivered in five weeks. Redis handles the polling load easily with less than 5 milliseconds latency, and the database load didn't change. A year later, we still haven't needed WebSockets.
>
> **Learning:** The lesson for me was to clarify what 'real-time' really means before choosing the technology. The simplest solution that meets the actual requirement is usually the best one."

### 3.3. Sự cố production — "Tell me about a time you handled a production incident."

> **Situation:** "One Friday evening last year, I was the on-call engineer. At around 7 p.m., we got alerts that the payment API error rate had jumped from below 0.1 percent to about 20 percent. It was during a big sales campaign, so every minute was costing money.
>
> **Task:** As on-call, my job was to restore the service as fast as possible, and then find the root cause.
>
> **Action:** First, I opened an incident channel and posted a short status update, so the support team and managers knew we were working on it. That stopped people from messaging me directly, so I could focus.
>
> Then I checked our Grafana dashboards. The errors were connection timeouts to the database, and the connection pool — HikariCP — was completely exhausted. There had been no deployment that day, so it wasn't a code change. I checked the slow-query log and found one reporting query running hundreds of times, each taking several seconds. It came from a new campaign dashboard that the marketing team had started using that afternoon, and it was hitting the primary database.
>
> To mitigate quickly, I asked the marketing team to close the dashboard, and I temporarily disabled that endpoint with a feature flag. Within about five minutes, the connection pool recovered and the error rate went back to normal. Total impact was about 25 minutes.
>
> **Result:** On Monday, I led the post-mortem. We agreed on three action items: route all reporting queries to a read replica, set a statement timeout for that database user, and add an alert on connection pool usage above 80 percent. I implemented the first two myself that week.
>
> **Learning:** I learned that in an incident, communication is as important as debugging — a quick status update saves a lot of time. And the first goal is mitigation, not finding the perfect fix."

## 4. Strengths, Weaknesses, 5 years

### 4.1. "What are your strengths?"

**Khung:** 2–3 điểm mạnh **liên quan đến job**, mỗi điểm có **1 bằng chứng ngắn**.

> "I'd say my biggest strength is that I care about reliability and I'm good at debugging difficult production problems. For example, I'm usually the person my team asks when there's a strange performance issue, and I've led several post-mortems that improved our monitoring.
>
> The second one is that I can communicate well between technical and non-technical people. Because I've worked on both backend and frontend, I can talk with designers and product managers about trade-offs in a way they understand.
>
> And third, I'm a fast learner. When we adopted Kafka, I had no experience with it, but within a couple of months I became the go-to person on the team for Kafka consumer issues."

### 4.2. "What is your greatest weakness?"

**Khung:** Điểm yếu **thật** + **không phải kỹ năng cốt lõi của job** + **bạn đang làm gì để cải thiện** + **tiến bộ đã thấy**.

**Không dùng:** "I'm a perfectionist", "I work too hard" (sáo rỗng). Không chọn "I'm not good at Java" (cốt lõi).

> **Option 1 — Tiếng Anh (rất thật cho bạn, và cho thấy nỗ lực):** "To be honest, my spoken English is still not as strong as my technical skills. I read documentation and write in English every day without problems, but in fast discussions I sometimes need a moment to find the right words. About nine months ago, I started a structured plan: I practice speaking one hour every day, I have weekly sessions with a tutor, and I've done many mock interviews. I've improved a lot — a year ago, I couldn't have done this interview in English. I'm still working on it, and I think working in an international team will speed that up."

> **Option 2 — Delegation:** "In the past, I tended to take on too much myself. When something was urgent, I'd just do it instead of delegating, because it felt faster. But that created a bottleneck, and it wasn't good for the juniors' growth. So now I make a conscious effort to delegate — I ask myself, 'Who else could do this and learn from it?' Last quarter, I handed over our deployment pipeline work to a junior developer and supported him with reviews, and it went really well."

> **Option 3 — Public speaking:** "I used to be uncomfortable presenting in front of large groups. So last year I volunteered to give two internal tech talks — one about Kafka and one about database indexing. The first one was quite stressful, but the second one went much better, and I got good feedback. I still prepare more than others, but it's not a problem anymore."

### 4.3. "Where do you see yourself in five years?"

**Khung:** Hướng phát triển **phù hợp với công ty** (không nói "mở công ty riêng", "làm ở Google").

> "In five years, I'd like to be a staff engineer or a tech lead — someone who designs systems across several teams and helps other engineers grow. I'm more interested in the technical leadership path than pure people management, at least for now. I'd also like to be much deeper in distributed systems and cloud architecture. Ideally, I'd grow into that role here, because this team works on exactly the kind of large-scale problems I want to learn from."

## 5. Cụm từ hữu ích (35)

| # | English | Nghĩa |
| --- | --- | --- |
| 1 | I was asked to mentor... / I volunteered to... | Được giao / tự nguyện |
| 2 | He was struggling with... | Gặp khó khăn với |
| 3 | I paired with him on... | Pair programming với |
| 4 | I set up weekly one-on-ones. | Họp 1-1 hằng tuần |
| 5 | I wanted to create a safe environment to ask questions. | Môi trường an toàn |
| 6 | blocking vs. non-blocking comments | Comment bắt buộc / gợi ý |
| 7 | I gave him ownership of... | Giao quyền làm chủ |
| 8 | He became independent / self-sufficient. | Tự lập |
| 9 | The team adopted this practice. | Team áp dụng |
| 10 | I was the tech lead for this feature. | Tech lead của tính năng |
| 11 | I wrote a design document / an RFC. | Viết tài liệu thiết kế |
| 12 | I compared the options: ... | So sánh phương án |
| 13 | The pros were... and the cons were... | Ưu, nhược |
| 14 | On one hand..., on the other hand... | Một mặt..., mặt khác |
| 15 | It met the actual requirement. | Đáp ứng yêu cầu thực tế |
| 16 | I got buy-in from the team / stakeholders. | Được đồng thuận |
| 17 | I was on call that week. | Trực sự cố |
| 18 | We got an alert that... | Nhận cảnh báo |
| 19 | The error rate spiked to... | Tỉ lệ lỗi tăng vọt |
| 20 | I opened an incident channel. | Mở kênh xử lý sự cố |
| 21 | My first priority was to mitigate the impact. | Ưu tiên giảm thiệt hại |
| 22 | I rolled back the deployment. | Rollback |
| 23 | I disabled it behind a feature flag. | Tắt bằng feature flag |
| 24 | The connection pool was exhausted. | Pool kết nối cạn |
| 25 | Service was restored within X minutes. | Khôi phục trong X phút |
| 26 | We ran a blameless post-mortem. | Post-mortem không đổ lỗi |
| 27 | action items | Đầu việc khắc phục |
| 28 | My biggest strength is... For example, ... | Điểm mạnh + ví dụ |
| 29 | I'm the go-to person for... | Người mọi người tìm đến |
| 30 | One area I'm working on is... | Điểm đang cải thiện |
| 31 | To be honest, ... | Thành thật mà nói |
| 32 | I've made good progress, but I'm still working on it. | Tiến bộ nhưng vẫn cố gắng |
| 33 | I tended to... / I used to... | Tôi từng có xu hướng |
| 34 | In five years, I'd like to... | 5 năm tới |
| 35 | the technical leadership path / the management track | Hướng chuyên gia / quản lý |

## 6. Lỗi người Việt hay mắc

1. **Khiêm tốn quá mức ở câu Strengths:** "I don't have any special strength..." → Văn hoá phương Tây mong bạn **tự tin nói điểm mạnh kèm bằng chứng**.
2. **Weakness quá thật và nguy hiểm:** "I'm lazy", "I don't like to learn new things", "I can't handle pressure".
3. **Câu chuyện mentoring không có kết quả đo được.** Thêm: số comment giảm, thời gian onboarding, junior được thăng chức.
4. **Sự cố production — đi thẳng vào debug, quên communication.** Interviewer Senior đánh giá cao việc bạn cập nhật stakeholders.
5. **Quyết định kỹ thuật — không nói phương án bị loại.** Phải có "We considered X, but..."
6. **Từ vựng:** "I teach him" → "I **mentored/coached** him"; "The server is die" → "The server **went down** / **crashed**"; "fix bug hot" → "**hotfix**"; "I make a meeting" → "I **set up / scheduled** a meeting".
7. **5 năm:** "I want to be a manager" khi đang ứng tuyển IC role (nên nói "technical leadership"), hoặc "I don't know".

## 7. Lịch luyện trong tuần

| Ngày | Việc |
| --- | --- |
| T2 | Viết STAR gạch đầu dòng: **mentoring/lead**. Nói 5 lần. |
| T3 | **Quyết định kỹ thuật khó** — nhớ phần "options + trade-off". |
| T4 | **Sự cố production** — luyện phần timeline (7pm alert → 7:05 → 7:25 restored). |
| T5 | **Phỏng vấn thử #2** với prompt mục 8. |
| T6 | Viết + luyện Strengths / Weaknesses / 5 years. Ghi âm. |
| T7 | Ôn toàn bộ 6 câu chuyện STAR (tuần 29+30). Nhật ký. |

## 8. Prompt cho AI voice — Mock interview #2

```
You are a hiring manager for a Senior Backend Engineer (Java/Spring, microservices)
position at an international company. Run a 30-minute behavioral interview in
English. My level is B1, please speak clearly.

Questions (one at a time, with 1-2 follow-ups each):
1. Tell me about a time you mentored or helped a less experienced colleague.
2. Tell me about the most difficult technical decision you've made.
3. Tell me about a production incident you handled. Walk me through it.
4. What are your greatest strengths?
5. What is your biggest weakness?
6. Where do you see yourself in five years?

Follow-ups should challenge me, e.g. "What alternatives did you consider?",
"How did you know it worked?", "What would you do if your manager disagreed?"

At the end, evaluate me like a real hiring manager:
- Does this sound like a Senior engineer? Why / why not?
- Which story was strongest and which was weakest?
- Was my weakness answer honest and convincing?
- Top 5 language mistakes with corrections.
- Hire / no hire recommendation with 2 reasons.
```

## 9. Checklist tự đánh giá

- [ ] Chuyện mentoring: có hành động cụ thể (1-1, pair, review) và kết quả đo được
- [ ] Chuyện quyết định: có ít nhất 2 phương án + lý do chọn + trade-off
- [ ] Chuyện sự cố: có **mitigate trước, root cause sau**, có communication, có action items
- [ ] Strengths: 2–3 điểm, mỗi điểm có ví dụ
- [ ] Weakness: thật, không phải kỹ năng cốt lõi, có hành động cải thiện + tiến bộ
- [ ] 5 years: phù hợp với công ty, không mơ hồ
- [ ] Giọng tự tin, không xin lỗi ("Sorry, my English is bad...")
- [ ] Phát âm: *mentor* /ˈmentɔː/, *incident* /ˈɪnsɪdənt/, *mitigate* /ˈmɪtɪɡeɪt/, *strength* /streŋθ/, *weakness* /ˈwiːknəs/

## 10. Tài liệu tham khảo

- Tech Interview Handbook — behavioral questions list: https://www.techinterviewhandbook.org
- Levels.fyi — hiểu khác biệt Senior / Staff ở các công ty: https://www.levels.fyi
