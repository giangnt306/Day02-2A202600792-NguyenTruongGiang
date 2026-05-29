# 02 — Group Problem Statement

## Group convergence

| Cluster | Candidate examples | Pattern chung |
|---|---|---|
| Cam kết & theo dõi | PM commit deadline trước khi align eng; Dev leader không có plan/tracking; BA khai thác requirement chưa đủ rõ | Cam kết hoặc input đầu vào không được align & track rõ downstream (dev/QA) lãnh hậu quả |
| Tổng hợp / tóm tắt | Check & Summarize Notifications; Write Lesson Notes; Review LAB Instruction | Đọc nhiều nội dung rồi nén lại để nắm nhanh |
| Tìm thông tin rải rác | Tìm lịch/deadline trong nhiều group chat; Mỗi môn 1 platform nộp bài | Thông tin cần thì nằm rải ở nhiều nơi, khó tra đúng lúc |
| Chuẩn hóa / định dạng tài liệu | Chỉnh format báo cáo Word theo chuẩn trường | Đã có nội dung nhưng phải sửa cho khớp một bộ chuẩn |

## Shortlist và score

| Candidate | Actor rõ | Workflow rõ | Pain có evidence | Impact đo được | Làm trong lab | So sánh R/W/A được | Nhóm hiểu domain | Tổng |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Chỉnh format Word theo chuẩn | 5 | 5 | 4 | 5 | 5 | 4 | 5 | 33 |
| Check & Summarize Notifications | 5 | 5 | 4 | 4 | 4 | 4 | 5 | 31 |
| Tìm lịch/deadline trong group chat | 5 | 4 | 4 | 4 | 3 | 4 | 5 | 29 |
| Slack Search | 4 | 4 | 4 | 4 | 3 | 4 | 4 | 27 |

Nhóm chọn: **Chỉnh format báo cáo Word theo chuẩn trường.**

Vì sao chọn:
- **Workflow rõ nhất:** input (draft) + bộ chuẩn output đúng chuẩn. Không mơ hồ.
- **Impact đo objective:** đếm được số lỗi format và thời gian sửa trước/sau, không phụ thuộc cảm tính.
- **Data access đơn giản nhất:** chỉ cần 1 file Word + 1 bộ chuẩn. Không cần quyền truy cập LMS/nhiều nền tảng.
- **Before/after vẽ rất rõ:** dễ demo, dễ validate nhanh với bạn cùng lớp.

Vì sao không chọn các bài khác:
- **Summarize Notifications:** workflow rõ nhưng "summarize đủ tốt" là quality metric khó thống nhất trong thời gian lab.
- **Tìm lịch trong group chat / multi-platform:** impact rộng nhưng đều vướng data access nhiều nguồn dễ trượt sang một hệ thống search/đồng bộ quá lớn so với phạm vi lab.

## Quick validation

Nhóm hỏi nhanh 3 sinh viên/TA + mini poll trong lớp.

| Nguồn | Số người | Tín hiệu xác nhận | Tín hiệu phản bác | Nhóm sửa problem thế nào |
|---|---:|---|---|---|
| Quick interview | 3 | 2/3 từng mất 1–2h chỉnh format ngay trước hạn nộp; đau nhất ở mục lục, heading, caption hình/bảng, trích dẫn | 1 người nói khoa họ có template sẵn nên gần như không đau | Thu hẹp: không phải "auto-format mọi loại doc", mà "đối chiếu draft với một bộ chuẩn cụ thể" |
| Mini poll trong lớp | 8 | 5/8 từng bị trả lại / trừ điểm vì sai format | Vài người nói chỉ cần một template chuẩn là đủ, chưa cần AI | Thêm non-AI alternative để so sánh: template + style guide |

Insight sau validation:

```text
Pain thật không nằm ở việc "áp một cái template".
Pain nằm ở đoạn đối chiếu một bản nháp lộn xộn với bộ chuẩn, mà bộ chuẩn đó một phần là quy tắc ngầm, cần phán đoán
(heading mức mấy, đánh số mục lục, caption, kiểu trích dẫn) rồi sửa cho đúng. Đây chính là phần template tĩnh KHÔNG giải quyết được,
và là chỗ AI có giá trị thật.
```

## Research giải pháp

 Nguồn / Tool / Case | Họ giải quyết phần nào? | Điểm mạnh | Khoảng trống / Rủi ro | Bài học cho nhóm |
|---|---|---|---|---|
| **Word Styles + Template `.dotx`** ([microsoft.com](https://support.microsoft.com/en-us/office/create-a-template-86a1d089-5ae2-4d53-9042-1191bce57deb)) | Áp chuẩn font, margin, heading styles từ file template gốc của trường | Miễn phí, hoạt động offline, không cần cài thêm gì. Sinh viên chỉ cần mở file template là đúng ngay. | Phải phân phối template đúng cách; sinh viên vẫn có thể tự override styles thủ công. Không tự detect lỗi format. | Bước nền tảng bắt buộc mọi giải pháp khác đều build trên template chuẩn này. Trường nên lock styles quan trọng (heading, body) để tránh override. |
| **Macro VBA trong Word** ([learn.microsoft.com](https://learn.microsoft.com/en-us/office/vba/word/concepts/words-object-model/apply-a-style)) | Tự động hóa: chạy 1 click để re-apply toàn bộ styles theo chuẩn trường lên file bất kỳ | Batch được nhiều file. Admin/giảng viên có thể chạy hàng loạt file nộp. Logic kiểm tra từng paragraph style. | Cần người biết VBA viết và maintain. Sinh viên không tự chạy được nếu không có file `.dotm`. Macro bị disable ở một số máy trường. | Phù hợp cho admin chuẩn hóa hàng loạt sau khi sinh viên nộp, không phải cho sinh viên tự dùng. Cần đội IT enable macro trust. |
| **python-docx (Python)** ([python-docx.readthedocs.io](https://python-docx.readthedocs.io/en/latest/)) | Script batch-format nhiều file `.docx`: đổi font, margin, heading style theo quy định | Xử lý 100+ file tự động. Có thể output báo cáo lỗi từng file. Tích hợp CI/pipeline. | Cần dev setup Python environment. Không handle được trường hợp nội dung phức tạp (bảng lồng nhau, textbox). Không có giao diện cho người không biết code. | Giải pháp tốt nhất cho admin muốn chuẩn hóa hàng loạt. Nên wrap bằng script đơn giản + GUI nhỏ (Streamlit/Gradio) để giảng viên không biết code vẫn dùng được. |
| **Grammarly / LanguageTool (Word add-in)** ([grammarly.com](https://www.grammarly.com/office-addin)) | Kiểm tra lỗi ngôn ngữ trong báo cáo; một phần check consistency | Inline trong Word, dễ tiếp cận cho sinh viên. LanguageTool có hỗ trợ tiếng Việt cơ bản. | Không check format theo chuẩn trường (font, margin, heading). Chỉ giải quyết grammar/spelling, không phải layout. | Input bổ trợ tốt cho chất lượng văn bản, không phải giải pháp format. Dùng song song, không thay thế tool format. |
| **Docxtools / FormatMatch (Word add-in)** ([appsource.microsoft.com](https://appsource.microsoft.com/en-us/marketplace/apps?product=office%3Bword&page=1)) | Add-in Word cho phép compare style của file hiện tại với template chuẩn, highlight chỗ sai | Sinh viên thấy ngay chỗ sai trong Word mà không cần export/upload đâu cả. Visual feedback rõ ràng. | Phụ thuộc vào chất lượng add-in bên thứ ba; phí license nếu dùng ở cấp độ trường lớn. Cần test kỹ với template của trường. | Pattern tốt: detect lỗi inline ngay trong Word thay vì sau khi nộp. Nên pilot với 1 lớp trước khi rollout toàn trường. |
| **Claude / GPT-4o (AI assistant)** ([claude.ai](https://claude.ai)) | Upload file `.docx` AI check format theo rubric trường, liệt kê lỗi cụ thể, gợi ý sửa | Linh hoạt, không cần cài thêm gì. Hiểu ngữ nghĩa quy định (ví dụ: "heading cấp 1 cần in đậm, cỡ 14") và áp dụng đúng. | Không tự sửa file trực tiếp (chỉ gợi ý). Kết quả phụ thuộc vào prompt chất lượng. Cần người thật review output trước khi nộp. | Dùng làm bước pre-check cho sinh viên: upload -> nhận checklist lỗi -> tự sửa. AI draft checklist, người thật confirm. Không nên dùng để tự động phê duyệt. |
| **SharePoint / Google Drive + template link** ([microsoft.com/sharepoint](https://support.microsoft.com/sharepoint)) | Phân phối template chuẩn; sinh viên luôn mở đúng version mới nhất từ link trường cấp | Version control tốt: trường cập nhật template 1 lần, toàn bộ sinh viên nhận ngay. Không lo dùng template cũ. | Chỉ giải quyết khâu phân phối, không check xem sinh viên có dùng đúng không. Cần kết hợp với tool check format. | Bước hạ tầng cần thiết. Nên kết hợp: SharePoint cung cấp template -> python-docx/macro check format khi nộp. Hai bước bổ trợ nhau. |
 
Không có tool nào "all-in-one". Stack thực tế gợi ý:
 
1. **Template chuẩn**: (phân phối qua SharePoint/Drive) nền tảng bắt buộc
2. **Script python-docx hoặc Macro VBA**: batch-format/check hàng loạt cho admin
3. **AI pre-check (Claude/GPT-4o)**: tùy chọn cho sinh viên tự kiểm tra trước khi nộp

## Workflow before / after

### Current state — 5 bước, ~80 phút

```
┌──────────────────┐     ┌────────────────────┐     ┌────────────────────┐
│ 1 Đọc rubric /   │     │ 2 Đối chiếu draft  │     │ 3 Sửa heading +    │
│   bộ chuẩn trường│ →   │   ↔ chuẩn, dò lỗi  │ →   │   cập nhật mục lục │
│       ○ 10'      │     │       ● 35'        │     │       ○ 15'        │
└──────────────────┘     └────────────────────┘     └────────────────────┘
                                                              ↓
                         ┌────────────────────┐     ┌────────────────────┐
                         │ 5 Soát cuối + nộp  │     │ 4 Sửa caption hình │
                         │                    │ ←   │   /bảng + trích dẫn│
                         │       ○ 5'         │     │       ○ 15'        │
                         └────────────────────┘     └────────────────────┘
```

> **Bottleneck:** Bước 2 — sinh viên phải tự đối chiếu một bản nháp lộn xộn với bộ chuẩn, trong đó nhiều quy tắc là ngầm và cần phán đoán (heading cấp mấy, đánh số mục lục, caption hình/bảng, kiểu trích dẫn).

---

### Future state — 5 bước, ~21 phút

```
┌──────────────────┐     ┌────────────────────┐     ┌────────────────────┐
│ 1 Mở draft trong │     │ 2 Upload cho AI    │     │ 3 AI trả checklist │
│   template chuẩn │ →   │   đối chiếu rubric │ →   │   lỗi + gợi ý sửa  │
│       ○ 2'       │     │       ○ 1'         │     │       ○ 1'         │
│  [rule/template] │     │     [workflow]     │     │     [workflow]     │
└──────────────────┘     └────────────────────┘     └────────────────────┘
                                                              ↓
                         ┌────────────────────┐     ┌────────────────────┐
                         │ 5 Soát cuối + nộp  │     │ 4 SV sửa theo      │
                         │                    │ ←   │   checklist        │
                         │       ○ 2'         │     │       ● 15'        │
                         │                    │     │  [human boundary]  │
                         └────────────────────┘     └────────────────────┘
```

> **Fallback:** AI bỏ sót hoặc báo nhầm lỗi -> sinh viên vẫn soát thủ công đối chiếu rubric trước khi nộp.
>
> **Bottleneck mới:** Bước sinh viên sửa theo checklist (15') — chấp nhận được vì đó là điểm kiểm soát chất lượng, phần khó (phán đoán quy tắc ngầm) đã do AI lo.

---

### Before/after impact

| Metric           | Trước                        | Sau kỳ vọng                | Ghi chú                                          |
|------------------|------------------------------|----------------------------|--------------------------------------------------|
| Tổng thời gian   | ~80 phút (1–2h trước hạn)    | Dưới 25 phút               | Target chính                                     |
| Số bước          | 5                            | 5                          | Không chỉ giảm bước, mà giảm effort ở bước đối chiếu/dò lỗi |
| Bước thủ công    | 5/5                          | 2/5                        | Sinh viên vẫn sửa và nộp                         |
| Bottleneck chính | Đối chiếu draft ↔ chuẩn (phán đoán quy tắc ngầm) | Sửa theo checklist | Human boundary                                   |
| Risk mới         | Không có AI sai sót          | AI bỏ sót / báo nhầm lỗi   | Cần sinh viên soát trước khi nộp                 |

---

## Problem Statement v0

| Field          | Nội dung |
|----------------|----------|
| Actor          | Sinh viên phải nộp báo cáo Word đúng bộ chuẩn format của trường/khoa. |
| Workflow       | Viết xong nội dung -> đọc rubric/bộ chuẩn -> đối chiếu draft với chuẩn -> sửa heading, mục lục, caption hình/bảng, trích dẫn -> soát cuối -> nộp. |
| Bottleneck     | Bước đối chiếu bản nháp lộn xộn với bộ chuẩn (~35 phút): nhiều quy tắc ngầm cần phán đoán (heading cấp mấy, đánh số mục lục, caption hình/bảng, kiểu trích dẫn). |
| Impact         | Tốn khoảng 1–2h ngay trước hạn nộp; dễ bị trả lại hoặc trừ điểm vì sai format (5/8 trong poll từng bị). |
| Success Metric | Giảm thời gian chỉnh format từ ~80 phút xuống dưới 25 phút; giảm số lỗi format còn sót khi nộp. |
| Boundary       | AI không tự sửa và nộp file thay sinh viên; không tự bịa quy tắc ngoài rubric; chỉ đối chiếu với bộ chuẩn được cung cấp; sinh viên là người confirm và sửa cuối. |

---

## Rule / Workflow / Agent

| Mức      | Phương án                                                            | Khi nào đủ                                                       | Rủi ro                                              | Chọn? |
|----------|----------------------------------------------------------------------|------------------------------------------------------------------|-----------------------------------------------------|-------|
| Rule     | Template `.dotx` chuẩn (phân phối qua SharePoint) + lock styles      | Đủ nếu lỗi chỉ là font/margin/heading style cố định             | Không bắt được các quy tắc ngầm cần phán đoán (caption, trích dẫn, ...) | Dùng cho bước cơ bản |
| Workflow | Template chuẩn -> AI đối chiếu draft với rubric -> trả checklist lỗi -> sinh viên sửa | Hợp vì workflow tuyến tính, AI chỉ lo phần dò lỗi/phán đoán, người sửa | AI bỏ sót / báo nhầm lỗi, cần sinh viên soát   | Chọn |
| Agent    | Agent tự đọc nhiều file, tự sửa, tự nộp                              | Chỉ cần nếu batch nhiều file, nhiều định dạng, và tự quyết bước tiếp | Quá rộng, risk tự sửa sai và tự nộp             | Chưa chọn |

**Mức chọn: Workflow.**

Vì sao:
- Phân phối template và áp style cơ bản có thể dùng rule/script.
- Phần đối chiếu quy tắc ngầm cần AI phán đoán ngữ nghĩa.
- Sinh viên vẫn sửa và nộp nên risk kiểm soát được.
- Chưa cần agent vì workflow không cần tự lập kế hoạch động hay đụng nhiều tool.
---

## Problem Statement v1

| Field                       | Nội dung |
|-----------------------------|----------|
| Actor                       | Sinh viên phải nộp báo cáo Word đúng bộ chuẩn format của trường/khoa. |
| Workflow                    | Viết nội dung -> đọc rubric -> đối chiếu draft với chuẩn -> sửa heading/mục lục/caption/trích dẫn -> soát -> nộp. |
| Bottleneck                  | Đối chiếu draft lộn xộn với bộ chuẩn mất ~35 phút và dễ sót lỗi vì quy tắc ngầm. |
| Impact                      | Khoảng 1–2h ngay trước hạn/bài; dễ bị trả lại hoặc trừ điểm vì sai format. |
| Success Metric              | Giảm thời gian chỉnh format xuống dưới 25 phút; giảm số lỗi format còn sót khi nộp. |
| Boundary                    | AI không tự sửa và nộp file, không tự bịa quy tắc ngoài rubric, không thay sinh viên confirm cuối. |
| AI intervention point       | Sau khi sinh viên có draft và mở trong template chuẩn, trước bước sinh viên sửa: AI đối chiếu draft với rubric và trả checklist lỗi. |
| Mức chọn                    | Workflow: rule phân phối template + áp style, AI dò lỗi theo rubric, sinh viên sửa và nộp. |
| Rủi ro & người thật kiểm tra | Risk: AI bỏ sót lỗi, báo nhầm, hiểu sai quy tắc ngầm. Người thật review: sinh viên đối chiếu checklist với rubric và soát file trước khi nộp. |

---

## Final decision

**Decision: Go với scope nhỏ.**

**Pilot nhỏ nhất:**
- Dùng 2–3 bài báo cáo thật của bạn cùng lớp + bộ rubric format của 1 môn cụ thể.
- Chạy bán thủ công: sinh viên upload draft vào prompt chuẩn -> AI trả checklist lỗi theo rubric.
- Sinh viên sửa theo checklist; đo thời gian sửa và số lỗi format còn sót khi nộp so với cách thủ công.
**Exit / rollback:**
- Nếu AI bỏ sót quá nhiều lỗi hoặc báo nhầm khiến sinh viên mất công verify hơn tự làm trong 2 lần liên tiếp, hạ xuống template + checklist tĩnh.
- Nếu AI diễn giải sai quy tắc gây nộp sai format, chỉ dùng như gợi ý, không tin trực tiếp.
**Decision rationale:**
- Problem rõ, workflow rõ, metric đo được (số lỗi format, thời gian sửa).
- Có non-AI components (template chuẩn, lock styles).
- AI nằm ở một bước cụ thể (dò lỗi theo rubric), không ôm toàn bộ workflow.
- Human review rõ (sinh viên là người sửa và nộp cuối).
