# Tuần 24 — UI/UX và frontend

> Giai đoạn 3 · Tuần 7/9 · Checklist gốc: [phase-3-it-english.md](../../phase-3-it-english.md#tuần-24--uiux-và-frontend-theo-hướng-việc-bạn-đang-nhắm)

## 1. Mục tiêu tuần

- Dùng đúng từ vựng thiết kế và frontend: *wireframe, user flow, accessibility, responsive, breakpoint, design system...*
- Giải thích một màn hình bạn từng thiết kế/làm (T3): **mục đích → người dùng → bố cục → tương tác → trạng thái (loading/empty/error) → quyết định thiết kế**.
- Nhận và đưa góp ý về sản phẩm một cách xây dựng (T5).
- Giải thích **How does a browser render a page?** và **State management in frontend**.

**Mẹo:** người làm cả backend lẫn UI rất có giá trị. Khi phỏng vấn, hãy nói về UI bằng **ngôn ngữ của người dùng** ("users couldn't find the button") chứ không chỉ bằng ngôn ngữ code.

## 2. Từ vựng IT

| # | Từ | IPA (Mỹ) | Cách đọc dễ nhớ | Nghĩa | Câu ví dụ |
| --- | --- | --- | --- | --- | --- |
| 1 | wireframe | /ˈwaɪərfreɪm/ | "UAI-ơ-frêym" | khung sơ đồ màn hình | I made a quick wireframe in Figma. |
| 2 | mockup | /ˈmɑːkʌp/ | "MAK-âp" | bản thiết kế tĩnh chi tiết | The mockup shows the final colors. |
| 3 | prototype | /ˈproʊtətaɪp/ | "PRÂU-tơ-taip" | bản mẫu bấm thử được | We tested the prototype with five users. |
| 4 | user flow | /ˈjuːzər floʊ/ | "DIU-zơ FLÂU" | luồng thao tác người dùng | The sign-up flow has too many steps. |
| 5 | user journey | /ˈdʒɝːni/ | "GIƠ-ni" | hành trình người dùng | We mapped the whole user journey, from ad to purchase. |
| 6 | persona | /pərˈsoʊnə/ | "pơ-SÂU-nờ" | chân dung người dùng | Our main persona is a busy small-shop owner. |
| 7 | usability | /ˌjuːzəˈbɪləti/ | "diu-zơ-BI-lơ-ri" | tính dễ dùng | We ran a usability test last week. |
| 8 | accessibility (a11y) | /əkˌsɛsəˈbɪləti/ | "ơk-se-sơ-BI-lơ-ri", a11y đọc "A-eleven-Y" | khả năng tiếp cận | Accessibility is not optional. |
| 9 | screen reader | | | phần mềm đọc màn hình | The icon button has no label, so screen readers can't read it. |
| 10 | alt text | /ɔːlt tɛkst/ | "OLT TÉKST" | mô tả ảnh | Every product image needs alt text. |
| 11 | contrast | /ˈkɑːntræst/ | "KAN-trést" | độ tương phản | The grey text fails the contrast check. |
| 12 | keyboard navigation | | | điều hướng bằng bàn phím | You can't close the modal with the keyboard. |
| 13 | focus state | /ˈfoʊkəs/ | "FÂU-kợs" | trạng thái được focus | Don't remove the focus outline. |
| 14 | responsive | /rɪˈspɑːnsɪv/ | "ri-SPAN-siv" | tự co giãn theo màn hình | The dashboard isn't responsive yet. |
| 15 | breakpoint | /ˈbreɪkpɔɪnt/ | "BRÂYK-point" | mốc chiều rộng đổi layout | At the 768-pixel breakpoint, the sidebar collapses. |
| 16 | viewport | /ˈvjuːpɔːrt/ | "VIU-port" | vùng hiển thị | The banner takes the full viewport height. |
| 17 | mobile-first | | | thiết kế cho mobile trước | We use a mobile-first approach. |
| 18 | layout / grid | /ˈleɪaʊt/ | "LÂY-ao(t)" | bố cục / lưới | It's a 12-column grid layout. |
| 19 | spacing / padding / margin | /ˈpædɪŋ/, /ˈmɑːrdʒɪn/ | "PÉ-đing", "MAR-gin" | khoảng cách trong/ngoài | Add more padding inside the card. |
| 20 | typography | /taɪˈpɑːɡrəfi/ | "tai-PA-grơ-fi" | kiểu chữ | Typography makes the page feel professional. |
| 21 | visual hierarchy | /ˈhaɪərɑːrki/ | "HAI-ơ-rar-ki" | thứ bậc thị giác | The main action should be first in the visual hierarchy. |
| 22 | call to action (CTA) | | "XI-TI-ÂY" | nút kêu gọi hành động | The CTA should say "Start free trial". |
| 23 | modal / dialog | /ˈmoʊdəl/ | "MÂU-đồ" | hộp thoại nổi | Confirm the deletion in a modal. |
| 24 | dropdown / tooltip / toast | /ˈtuːltɪp/ | "ĐRAP-đaon", "TUL-tip", "TÂUST" | menu thả / chú thích / thông báo nhỏ | Show a toast after saving. |
| 25 | empty state | | | màn hình khi chưa có dữ liệu | The empty state should explain how to create the first project. |
| 26 | loading state / skeleton | /ˈskɛlɪtən/ | "SKÉ-li-tần" | trạng thái tải / khung xương | We show a skeleton while data loads. |
| 27 | form validation | /ˌvælɪˈdeɪʃən/ | "ve-li-ĐÂY-shần" | kiểm tra dữ liệu nhập | Show validation errors next to each field. |
| 28 | design system | | | hệ thống thiết kế chung | Use the button from the design system. |
| 29 | component | /kəmˈpoʊnənt/ | "kầm-PÂU-nần(t)" | thành phần UI | I built a reusable table component. |
| 30 | props / state | /prɑːps/ | "PRAPS", "STÊYT" | dữ liệu truyền vào / trạng thái | The parent passes the user as a prop. |
| 31 | DOM | /dɑːm/ | "ĐAM" (một từ) | cây tài liệu HTML | Avoid touching the DOM directly in React. |
| 32 | CSSOM | | "XI-ÉS-ÉS-ÂU-EM" | cây style CSS | The browser builds the CSSOM from CSS. |
| 33 | render tree | | | cây hiển thị | Hidden elements are not in the render tree. |
| 34 | layout / reflow | /ˈriːfloʊ/ | "RI-flâu" | tính vị trí, kích thước | Changing the width triggers a reflow. |
| 35 | paint / composite | /kəmˈpɑːzɪt/ | "kầm-PA-zit" | vẽ pixel / ghép lớp | Animating `transform` only needs compositing. |
| 36 | render-blocking | | | chặn hiển thị | Large CSS files are render-blocking. |
| 37 | hydration | /haɪˈdreɪʃən/ | "hai-ĐRÂY-shần" | gắn JS vào HTML render sẵn từ server | Hydration makes the server-rendered page interactive. |
| 38 | single source of truth | | | nguồn dữ liệu duy nhất | The store is the single source of truth. |

## 3. Mẫu câu công việc

**Giải thích một màn hình**
1. This is the order history page. Its main goal is to help customers find a past order quickly.
2. The main users are returning customers, often on mobile.
3. At the top there's a search bar, and below it a list of orders, newest first.
4. Each card shows the date, the total and the status.
5. When you tap a card, it opens the order details.
6. While data is loading, we show a skeleton. If there are no orders, we show an empty state with a "Start shopping" button.
7. On desktop it's a table; below 768 pixels, it switches to cards.

**Lý do thiết kế**
8. We put the status first because that's what users ask support about most.
9. We removed two fields from the form to reduce friction.
10. User testing showed that people didn't notice the filter, so we made it more visible.
11. We followed the design system for spacing and colors.

**Accessibility và responsive**
12. All buttons can be reached with the keyboard.
13. Icon-only buttons have an `aria-label`.
14. The text meets the WCAG AA contrast ratio.
15. We tested it on small screens, down to 360 pixels wide.

**Đưa góp ý về UI**
16. I really like how clean the dashboard looks.
17. One thing I noticed: it's not clear what this icon does.
18. I wasn't sure where to click next.
19. Could we make the primary button stand out more?
20. The error message says "Invalid input"; could we tell the user how to fix it?
21. From an accessibility point of view, the grey text is a bit too light.

**Nhận góp ý**
22. Thanks, that's really helpful.
23. Could you show me where you got stuck?
24. That's a fair point. We'll test it with a few users.
25. I see. We did that because ..., but I agree it's confusing.
26. Let me note that down and discuss it with the designer.

**Làm việc với designer / backend**
27. Is this spacing 16 or 24 pixels?
28. What should happen when the request fails?
29. The API doesn't return that field yet. Can we use a placeholder for now?
30. Do we have a design for the empty state?

## 4. Hội thoại mẫu

### Hội thoại 1: Giải thích màn hình cho gia sư / người phỏng vấn

> **Tutor:** Can you show me a screen you built?
> **Nhat:** Sure. This is the checkout page for an online shop. The goal is simple: help users pay as quickly as possible, without mistakes.
> **Tutor:** What's on the page?
> **Nhat:** On the left, there's a short form: shipping address and payment. On the right, a summary of the cart with the total. On mobile, the summary moves to the top and collapses.
> **Tutor:** Why did you design it like that?
> **Nhat:** We looked at analytics and saw that many users dropped off at the address step. So we reduced the form from eleven fields to seven, added address auto-complete, and we show validation errors next to each field instead of at the top.
> **Tutor:** Did it work?
> **Nhat:** Yes. The checkout completion rate went up by about eight percent in the first month.
> **Tutor:** Impressive. What about accessibility?
> **Nhat:** Every field has a proper label, you can complete the whole form with the keyboard, and the error messages are announced to screen readers.

### Hội thoại 2: Nhận góp ý về sản phẩm

> **PM (Laura):** I tried the new dashboard. Can I give you some feedback?
> **Nhat:** Of course, please.
> **Laura:** Overall it looks great. But I wasn't sure what the numbers in the top cards mean. Is it today or this month?
> **Nhat:** Good point. It's the last thirty days. We should make that clear. Maybe a small label under each number?
> **Laura:** Yes, that would help. Also, on my phone, the chart was cut off.
> **Nhat:** Thanks for catching that. Which phone were you using?
> **Laura:** An iPhone SE, so quite small.
> **Nhat:** OK, that's 375 pixels wide. I'll check the breakpoints and make the chart scroll horizontally on small screens. I'll send you a preview link tomorrow.

## 5. Bài giải thích kỹ thuật mẫu

### 5.1 T4 — How does a browser render a page?

> When you type a URL and press Enter, the browser first finds the server's IP address with a DNS lookup, opens a connection, usually with TLS for HTTPS, and sends an HTTP request. The server responds with an HTML document.
>
> The browser parses the HTML from top to bottom and builds the DOM, a tree of all the elements. When it finds CSS, it downloads and parses it into the CSSOM, a tree of styles. CSS is render-blocking: the browser won't paint the page until it has the CSS, because otherwise the page would flash without styles. A normal script tag blocks HTML parsing, because the script might change the DOM. That's why we use `defer` or `async`, or put scripts at the end.
>
> Next, the browser combines the DOM and the CSSOM into the render tree, which contains only the visible elements with their computed styles. Then comes layout, also called reflow: the browser calculates the exact position and size of each element. After that, it paints the pixels, colors, text, borders and images, often into several layers. Finally, the compositor combines the layers and shows them on the screen, often using the GPU.
>
> This matters for performance. Changing an element's width or height triggers layout again, which is expensive. Changing only `transform` or `opacity` can often skip layout and paint, which is why smooth animations use them.

**5 cụm từ dùng lại:**
1. *When you ..., the browser first ...*
2. *X is render-blocking: ...*
3. *Next, the browser combines X and Y into Z.*
4. *Then comes ..., also called ...*
5. *This matters for performance.*

### 5.2 T6 — State management in frontend

> State is any data that can change over time and affects what the user sees: the logged-in user, the items in a cart, whether a modal is open, or the text in an input. State management is about deciding where that data lives and how it changes.
>
> There are a few kinds of state. **Local state** belongs to one component, like a dropdown being open; in React we use `useState`. When two sibling components need the same data, we lift the state up to their common parent and pass it down as props. **Global state**, like the current user or the theme, is needed in many places. Passing props through many levels becomes painful, which we call prop drilling, so we use React Context or a store library like Redux, Zustand, or Pinia in Vue.
>
> A separate and very important kind is **server state**: data that really lives in the backend, like a list of orders. It needs caching, loading and error states, and refetching. Libraries like TanStack Query handle this much better than putting API data into Redux by hand. Finally, some state belongs in the **URL**, like filters or the current page, so users can share and bookmark it.
>
> Most modern approaches follow a one-way data flow: state flows down, and events flow up. My rule is to keep state as local as possible, and only make it global when you really need to.

**5 cụm từ dùng lại:**
1. *X is any data that ...*
2. *X is about deciding where ... lives and how it changes.*
3. *There are a few kinds of ...*
4. *A separate and very important kind is ...*
5. *My rule is to keep ... as ... as possible.*

## 6. Mẫu viết

**Mô tả PR cho thay đổi UI**

```
## What
Redesigned the order history page for mobile.

## Why
62% of visits to this page are on mobile, and the table was hard to read
on small screens (see PROD-418).

## How
- Below 768px, the table becomes a list of cards.
- Added a skeleton loading state and an empty state.
- Status badges use the design system colors (WCAG AA contrast).

## Screenshots
| Before | After |
| ------ | ----- |
| (img)  | (img) |

## Testing
- Chrome, Safari, Firefox; iPhone SE (375px) and Pixel 7.
- Keyboard-only navigation and VoiceOver.
```

**Góp ý design trong Figma/Slack**

```
Hi Mai, a few thoughts on the new settings page:
1. Love the grouping, it's much easier to scan now.
2. The "Delete account" button is right next to "Save". Could we move it to
   a separate "Danger zone" section to avoid accidental clicks?
3. What should we show while the settings are loading?
Happy to jump on a call if it's easier!
```

## 7. Bài tập

1. **Ghép:** (a) wireframe (b) prototype (c) breakpoint (d) empty state (e) alt text — (1) mô tả ảnh cho screen reader (2) bản phác thảo bố cục đơn giản (3) màn hình khi chưa có dữ liệu (4) mốc chiều rộng đổi layout (5) bản bấm thử được.
2. **Sắp xếp các bước render:** Paint, Build the DOM, Layout, Composite, Build the render tree, Build the CSSOM.
3. **Đúng hay sai?** (a) Elements with `display: none` are in the render tree. (b) A normal `<script>` tag blocks HTML parsing. (c) Animating `transform` is usually cheaper than animating `width`. (d) Server state should always be stored in Redux.
4. **Chọn loại state:** (a) Một dropdown đang mở hay đóng. (b) Người dùng đang đăng nhập. (c) Danh sách đơn hàng lấy từ API. (d) Bộ lọc "status=shipped&page=2" mà người dùng muốn gửi link cho đồng nghiệp.
5. **Viết lại góp ý cho mang tính xây dựng:** (a) "This page is ugly." (b) "Nobody will understand this icon." (c) "The form is bad."
6. **Nói (T3):** giải thích một màn hình bạn từng làm, 2–3 phút, theo khung ở mục 1. Có ít nhất 1 con số (kết quả hoặc dữ liệu).
7. **Nói:** giải thích browser rendering và state management, mỗi bài ≤ 3 phút.

## 8. Tài liệu

- [MDN Web Docs](https://developer.mozilla.org) — tìm "How browsers work", "Critical rendering path", "Accessibility". Tiếng Anh chuẩn, rõ.
- [web.dev](https://web.dev/learn) — các khóa miễn phí của Google: *Learn CSS*, *Learn Accessibility*, *Learn Performance*.
- [W3C Web Accessibility Initiative](https://www.w3.org/WAI/) — giới thiệu WCAG.
- [Fireship](https://www.youtube.com/@Fireship) — tìm "React state management", "how browsers render".
- [ByteByteGo YouTube](https://www.youtube.com/@ByteByteGo) — tìm "what happens when you type a URL".
- [roadmap.sh](https://roadmap.sh) — roadmap "Frontend" và "UX Design".

## 9. Đáp án

**Bài 1:** a-2, b-5, c-4, d-3, e-1.

**Bài 2:** Build the DOM → Build the CSSOM → Build the render tree → Layout → Paint → Composite. (DOM và CSSOM có thể được xây song song.)

**Bài 3:** (a) Sai (b) Đúng (c) Đúng (d) Sai — nên dùng thư viện server state như TanStack Query.

**Bài 4:** (a) local state (b) global state (c) server state (d) URL state.

**Bài 5 (gợi ý):**
(a) "I think the visual hierarchy could be stronger. Right now everything has the same weight, so it's hard to know where to look first."
(b) "I'm not sure users will understand this icon. Could we add a label or a tooltip?"
(c) "The form feels a bit long. Could we remove optional fields or split it into two steps?"

**Bài 6, 7:** tự chấm: có mục đích, người dùng, trạng thái loading/empty/error, ít nhất 1 lý do thiết kế.
