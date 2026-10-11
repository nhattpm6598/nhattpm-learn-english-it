# Bài học Giai đoạn 3 — Tiếng Anh IT và công việc (Tuần 18–26)

Đây là **tài liệu học thật** cho từng tuần, đi kèm checklist trong [phase-3-it-english.md](../../phase-3-it-english.md). Checklist cho biết *làm gì mỗi ngày*; các file dưới đây cung cấp *nội dung để học*: từ vựng có phiên âm, mẫu câu, hội thoại, bài giải thích kỹ thuật mẫu, mẫu viết, bài tập và đáp án.

**Trình độ nhắm tới:** B1 → B2. Câu văn tiếng Anh được viết đơn giản, đúng kỹ thuật, dùng được ngay trong công việc và phỏng vấn.

## Danh sách bài

| Tuần | Chủ đề | Bài giải thích kỹ thuật mẫu | Mẫu viết chính |
| --- | --- | --- | --- |
| [18](week-18.md) | Phát âm từ IT, đọc ký hiệu, version, Big O, URL, code | What is an API? · REST vs GraphQL | Tin nhắn giới thiệu bản thân |
| [19](week-19.md) | Daily standup và Agile | Scrum vs Kanban · Standup mẫu 5 ngày | Async standup, user story, ghi chú retro |
| [20](week-20.md) | Họp và thảo luận kỹ thuật | Monolith vs Microservices · SQL vs NoSQL | Meeting notes, ADR |
| [21](week-21.md) | Code review và giải thích code | Giải thích hàm Java từng dòng · Multithreading & race conditions · SOLID | Comment review, tổng kết review |
| [22](week-22.md) | Bug và sự cố | Logging, monitoring, alerting · Java garbage collection | Bug report, cập nhật sự cố, postmortem |
| [23](week-23.md) | Kiến trúc hệ thống | Caching strategies · Message queues (Kafka, RabbitMQ) · Khung trình bày kiến trúc 5' | Architecture overview, bảng quyết định công nghệ |
| [24](week-24.md) | UI/UX và frontend | How a browser renders a page · Frontend state management | PR cho thay đổi UI, góp ý design |
| [25](week-25.md) | Email và viết | Giải thích PR · "Tell me about yourself" 60 giây | Email (xin nghỉ, báo trễ, hỏi rõ, follow-up), commit, PR, CV bullets, LinkedIn summary |
| [26](week-26.md) | Tổng ôn: trình bày dự án 5' | Bài trình bày mẫu ~650 từ · 10 câu hỏi đào sâu có đáp án | Dàn ý, phiếu chấm, checklist quay video |

## Cấu trúc mỗi bài

1. **Mục tiêu tuần** — làm được gì vào cuối tuần.
2. **Từ vựng IT** — 30–40 từ: IPA giọng Mỹ, cách đọc dễ nhớ cho người Việt, nghĩa, câu ví dụ trong công việc.
3. **Mẫu câu công việc** — 25–40 câu chia theo tình huống.
4. **Hội thoại / tình huống mẫu** — 2 đoạn hội thoại thực tế (standup, họp, review, incident call...).
5. **Bài giải thích kỹ thuật mẫu** — 150–250 từ/bài, kèm 5 cụm từ để dùng lại.
6. **Mẫu viết** — template copy-paste được.
7. **Bài tập** — 5–8 bài.
8. **Tài liệu** — link tham khảo.
9. **Đáp án**.

## Cách dùng một bài trong tuần

| Ngày | Cách dùng file bài học |
| --- | --- |
| T2 | Đọc mục 1–2. Đưa từ vựng vào Anki (mặt trước: từ + câu ví dụ; mặt sau: IPA + nghĩa + audio từ YouGlish/Cambridge). Làm bài tập từ vựng. |
| T3 | Đọc to mục 3 và 4. Đóng vai cả hai người trong hội thoại, ghi âm. |
| T4 | Bài giải thích mẫu thứ nhất: đọc to 3 lần → shadowing → gấp bài, chỉ nhìn 5 cụm từ, nói lại 2 phút, ghi âm. |
| T5 | Buổi gia sư: mang bài giải thích và hội thoại đến, nhờ gia sư hỏi đào sâu. |
| T6 | Bài giải thích mẫu thứ hai (như T4). Làm bài tập viết ở mục 6–7. |
| T7 | Làm hết bài tập còn lại, xem đáp án, ghi từ/câu mới vào `log/vocabulary.md`, viết nhật ký vào `log/progress.md`. |

**Quy tắc quan trọng với bài mẫu:** đừng học thuộc lòng từng chữ. Học thuộc **khung** và **5 cụm từ**, rồi nói bằng ví dụ từ dự án thật của bạn. Người phỏng vấn nhận ra ngay câu trả lời học thuộc.

## Cách đọc cột phát âm

- IPA theo giọng Mỹ (General American). Tra lại trên [Cambridge Dictionary](https://dictionary.cambridge.org) (bấm nút **US**).
- "Cách đọc dễ nhớ" chỉ là gần đúng bằng chữ Việt, **chữ IN HOA = âm nhấn**. Luôn nghe audio thật trên [YouGlish](https://youglish.com).
- Âm cuối (-s, -ed, -t, -k) là lỗi số một của người Việt: luôn đọc rõ.

## 20 khái niệm cần giải thích được khi hết giai đoạn

Danh sách và bảng tự đánh giá nằm ở [week-26.md, bài tập 1](week-26.md#7-bài-tập). Các khái niệm có bài mẫu đầy đủ: API, REST vs GraphQL, Scrum vs Kanban, Monolith vs Microservices, SQL vs NoSQL, multithreading & race conditions, SOLID, logging/monitoring/alerting, Java GC, caching, message queues, browser rendering, frontend state management. Các khái niệm còn lại (story points, ACID, code review, load balancing, replication vs sharding, CDN, idempotency) có trong bảng từ vựng, mẫu câu và hội thoại; hãy tự viết bài giải thích theo cùng khung rồi nhờ AI hoặc gia sư sửa.

## Ghi chú về link tài liệu

Chỉ dùng trang chủ hoặc trang mục lục ổn định của các nguồn nổi tiếng (Fireship, ByteByteGo, GOTO, InfoQ, roadmap.sh, Refactoring.Guru, Oracle Java Tutorials, MDN, web.dev, Scrum Guide, Atlassian Agile, Google SRE, Google Engineering Practices, Conventional Commits, Kafka, RabbitMQ, Grammarly). Không có link tới video cụ thể: hãy dùng ô tìm kiếm của kênh với từ khóa gợi ý trong từng bài. Các link chưa được kiểm tra trực tuyến tại thời điểm viết (10/2026) vì môi trường soạn không có mạng; nếu link nào đã đổi, tìm tên trang trên Google.
