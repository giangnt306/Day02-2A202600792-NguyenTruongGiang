# Individual Problem Discovery — VinUni

## 1 — Individual Problem Scan (Scan rộng)

| # | Lăng kính | Problem quan sát được | Ai đang đau? | Dấu hiệu thật |
|---|---|---|---|---|
| 1 | Tốn thời gian | Check thông báo từ nhiều nguồn: Zalo, Discord, Outlook, V-app... | VinUni student | ~60 phút/tuần, dễ sót thông tin |
| 2 | Tốn thời gian | Nắm bắt thông tin hướng dẫn thực hiện các lab | VinUni student | 20 phút/buổi |
| 3 | Tốn thời gian | Lên thực đơn nấu cơm trong ngày | VinUni student | 10 phút/buổi |
| 4 | Tốn thời gian | Kiểm soát lượng calories nạp vào trong ngày | VinUni student | 10 phút/buổi |
| 5 | Tốn thời gian | Viết lesson notes sau mỗi buổi học | VinUni student | 30 phút/buổi |
| 6 | Tốn thời gian | Tổng hợp kiến thức rải rác từ nhiều slide/references/notes thành tài liệu ôn thi cuối kỳ | VinUni student | 2–3 giờ/môn, dễ sót chủ đề |
| 7 | Lặp đi lặp lại | Tìm và format trích dẫn/references đúng chuẩn khi viết essay/report | VinUni student | 15–20 phút/bài |
| 8 | Tốn thời gian | Theo dõi & rà soát chi tiêu sinh hoạt hàng tháng (ăn, đi lại, mua sắm) | VinUni student | ~60 phút/tháng |

**Vì sao phần scan này mạnh:**
- Có scan rộng trước khi hội tụ.
- Có nhiều lăng kính khác nhau (thời gian, tải nhận thức, lặp lại, tiền) → không chỉ tối ưu một loại pain.
- Mỗi problem có actor và dấu hiệu thật.
- Không bắt đầu bằng "làm chatbot" hoặc "xây agent".


## 2 — Top 3

| Rank | Problem | Vì sao chọn | Điều còn chưa chắc |
|---|---|---|---|
| 1 | Check & Summarize Notifications | Workflow rõ, mất nhiều thời gian, có metric tốt | Summarize "đủ tốt" đo thế nào |
| 2 | Review LAB Instruction | Có pain thật, AI có thể giúp đọc/tóm tắt | Quality improvement khó đo |
| 3 | Write lesson notes | Pain lặp lại mỗi buổi, input/output rõ (slide+ghi chú → notes), AI tổng hợp tốt | Notes AI có "đúng trọng tâm GV nhấn mạnh" không |


## Problem Card #1 — Check & Summarize Notifications

**Problem 1 câu:** Mỗi tuần sinh viên VinUni mất ~60 phút rải rác để check thông báo từ nhiều kênh (Zalo, Discord, Outlook, V-app...), và dễ miss thông tin quan trọng vì nó nằm phân tán.

**Actor:** Sinh viên VinUni

**Thời điểm / bối cảnh:** Rải rác trong ngày mỗi lần mở máy.

**Current workflow:**

1. Mở Zalo -> lướt nhóm lớp/CLB
2. Mở Discord -> check server môn học
3. Mở Outlook -> đọc email trường
4. Mở V-app -> check thông báo học vụ
5. Tự lọc cái nào quan trọng / cần hành động
6. Note lại deadline & việc cần làm

**Bottleneck:** Bước 5 — phải chuyển đổi liên tục giữa nhiều app và tự đánh giá độ ưu tiên. Đây không chỉ là chi phí thời gian mà còn là chi phí attention.

**Impact:** ~60 phút/tuần/sinh viên + chi phí ẩn khi miss deadline (nộp trễ, miss event). Càng nhiều kênh càng khó scale.

**Success metric:** Thời gian check còn <20 phút/tuần và số lần miss thông tin "cần hành động" ≈ 0.

**Non-AI alternative:** Tắt nhóm ít quan trọng + forward email + dùng 1 app gom thông báo. Giảm noise nhưng không tóm tắt và không phân loại "cần hành động".

**AI hypothesis:** AI gom thông báo từ các nguồn -> lọc noise -> phân loại ưu tiên + gắn cờ "cần hành động" -> xuất 1 nguồn duy nhất để sinh viên theo dõi.

**Quick gut:** Workflow (aggregation + summarization pipeline), có lõi Tool ở bước summarize.

**Điều còn chưa chắc:** "Summarize đủ tốt đo thế nào" → metric đề xuất: precision/recall của việc gắn cờ "cần hành động" trên 1 tuần mẫu. Rủi ro feasibility: Zalo và V-app gần như không có API mở -> cần kiểm chứng sớm.

```
CURRENT STATE — ~60'/tuần
┌────────────────┐   ┌────────────────┐   ┌────────────────┐
│1 Mở Zalo       │   │2 Mở Discord    │   │3 Mở Outlook    │
│nhóm lớp/CLB    │ → │server môn      │ → │email trường    │
│ ○ 10'          │   │ ○ 8'           │   │ ○ 7'           │
└────────────────┘   └────────────────┘   └────────────────┘
                                                   ↓
┌────────────────┐   ┌────────────────┐   ┌────────────────┐
│6 Note          │   │5 Tự lọc        │   │4 Mở V-app      │
│deadline/việc   │ ← │quan trọng ⚠    │ ← │thông báo       │
│ ○ 10'          │   │ ○ 20'          │   │ ○ 5'           │
└────────────────┘   └────────────────┘   └────────────────┘
⚠ bottleneck = chuyển đổi nhiều app + tự đánh giá ưu tiên
```

```
FUTURE STATE — ~6'/tuần
┌────────────────┐   ┌────────────────┐   ┌────────────────┐
│1 AI auto-pull  │   │2 AI trích      │   │3 AI gom thành  │
│từ group chat   │ → │xuất deadline   │ → │dashboard       │
│ ○ 2'           │   │ ○ 1'           │   │timeline ○ 1'   │
└────────────────┘   └────────────────┘   └────────────────┘
                                                   ↓
                     ┌────────────────┐   ┌────────────────┐
                     │5 Sync to       │   │4 Sinh viên     │
                     │Google Cal      │ ← │review          │
                     │ ○ 1'           │   │○ 1' ● green    │
                     └────────────────┘   └────────────────┘
● green = human checkpoint  ·  Fallback: AI sai -> SV mở app gốc
```


## Problem Card #2 — Review LAB Instruction

**Problem 1 câu:** Mỗi buổi lab, sinh viên mất ~20 phút đọc/hiểu tài liệu hướng dẫn dài và rải rác trước khi bắt tay làm, và thường không chắc đã nắm đúng các bước/yêu cầu.

**Actor:** Sinh viên VinUni chuẩn bị hoặc đang làm một buổi lab.

**Bối cảnh:** Đầu buổi lab khi mở file hướng dẫn trên github.

**Current workflow:**

1. Mở tài liệu hướng dẫn
2. Đọc lướt để nắm mục tiêu
3. Đọc kỹ từng bước
4. Lọc ra: cần chuẩn bị gì, các bước thực hiện, tiêu chí chấm
5. Tự note checklist các bước
6. Bắt đầu làm, quay lại tra cứu khi quên

**Bottleneck:** Bước 2 - 4 — thông tin quan trọng (yêu cầu nộp, rubric) lẫn trong văn bản dài -> mất thời gian định vị "phải làm gì".

**Impact:** ~20 phút/buổi × số buổi lab. Hiểu sai hướng dẫn -> làm lại / mất điểm. Phần "hiểu đúng" khó đo trực tiếp.

**Success metric:** Thời gian chuẩn bị còn <8 phút và giảm số lần hỏi lại TA về "đề bài yêu cầu gì"; sinh viên nắm bắt thông tin nhanh chóng trước khi làm.

**Non-AI alternative:** TA cung cấp sẵn checklist + rubric tóm tắt. Hiệu quả nhưng phụ thuộc TA, không tự động, không trả lời được câu hỏi tức thời lúc đang làm.

**AI hypothesis:** AI đọc tài liệu lab -> tóm tắt mục tiêu / các bước / rubric thành checklist, và trả lời Q&A bám theo tài liệu.

**Quick gut:** Tool (đọc + tóm tắt + Q&A trên 1 tài liệu).

**Điều còn chưa chắc:** Quality "hiểu đúng" khó đo -> proxy metric: số lần hỏi-lại TA và tỉ lệ nộp đúng yêu cầu ngay lần đầu.

```
CURRENT STATE — ~20'/buổi
┌────────────────┐   ┌────────────────┐   ┌────────────────┐
│1 Mở tài liệu   │   │2 Đọc lướt      │   │3 Đọc kỹ        │
│lab (PDF dài)   │ → │mục tiêu        │ → │từng bước ⚠     │
│ ○ ~0'          │   │ ○ 3'           │   │ ○ 8'           │
└────────────────┘   └────────────────┘   └────────────────┘
                                                   ↓
                     ┌────────────────┐   ┌────────────────┐
                     │5 Tự note       │   │4 Lọc           │
                     │checklist       │ ← │deliverable     │
                     │ ○ 4'           │   │+rubric ⚠ ○5'   │
                     └────────────────┘   └────────────────┘
⚠ bottleneck = định vị deliverable + rubric trong văn bản dài
```

```
FUTURE STATE — ~7'/buổi (+ Q&A khi cần)
┌────────────────┐   ┌────────────────┐   ┌────────────────┐
│1 AI tóm tắt    │   │2 AI sinh       │   │3 SV đọc +      │
│mục tiêu/bước/  │ → │checklist       │ → │đối chiếu gốc   │
│deliv+rubric ○2 │   │hành động ○ 1'  │   │○4' ● green     │
└────────────────┘   └────────────────┘   └────────────────┘
                                                   ↓
                                          ┌────────────────┐
                                          │4 Hỏi AI Q&A    │
                                          │bám tài liệu    │
                                          │ ○ khi cần      │
                                          └────────────────┘
● green = human checkpoint  ·  Fallback: AI không chắc -> trỏ trang gốc, không bịa
```


## Problem Card #3 — Write Lesson Notes

**Problem 1 câu:** Sau mỗi buổi học, sinh viên VinUni mất ~30 phút để viết lại lesson notes từ slide, ghi chú tay và trí nhớ, và notes thường rời rạc nên khó dùng để ôn lại về sau.

**Actor:** Sinh viên VinUni sau mỗi buổi học.

**Thời điểm / bối cảnh:** Ngay sau buổi học hoặc cuối ngày, khi ngồi tổng hợp lại bài.

**Current workflow:**

1. Mở lại slide bài giảng
2. Xem lại ghi chú tay / ảnh chụp bảng
3. Nhớ lại các điểm giảng viên nhấn mạnh
4. Tái cấu trúc thông tin thành dàn ý mạch lạc
5. Viết notes hoàn chỉnh
6. Lưu & đặt tên file để tìm lại sau

**Bottleneck:** Bước 3 - 4 -  phải tái cấu trúc thông tin rời rạc từ nhiều nguồn (slide + ghi chú + trí nhớ) thành notes mạch lạc. Vừa tốn thời gian vừa dễ sót ý quan trọng.

**Impact:** ~30 phút/buổi × số buổi học. Notes kém chất lượng -> ôn thi phải đọc lại slide từ đầu, nhân đôi chi phí về sau.

**Success metric:** Thời gian viết notes còn <10 phút/buổi và notes đủ để ôn thi mà gần như không cần mở lại slide gốc.

**Non-AI alternative:** Dùng template note có sẵn (Cornell notes) + ghi âm buổi học. Có cấu trúc nhưng vẫn phải tự viết tay, không tự tóm tắt và không gắn được câu hỏi ôn tập.

**AI hypothesis:** AI nhận slide + ghi chú thô (hoặc transcript) -> tóm tắt thành notes có cấu trúc (mục tiêu, key concepts, ví dụ, câu hỏi ôn tập) -> sinh viên review & chỉnh.

**Quick gut:** Tool (đọc nhiều nguồn + tổng hợp thành 1 output có cấu trúc), có chút Workflow ở khâu gom nguồn.

**Điều còn chưa chắc:** Notes do AI tạo có "đúng trọng tâm giảng viên nhấn mạnh" không -> khó đo trực tiếp. Proxy metric: % notes sinh viên giữ nguyên (ít phải sửa) và điểm/độ tự tin khi ôn tập từ notes đó.

```
CURRENT STATE — ~30'/buổi
┌────────────────┐   ┌────────────────┐   ┌────────────────┐
│1 Mở lại slide  │   │2 Xem ghi chú   │   │3 Nhớ điểm GV   │
│bài giảng       │ → │tay/ảnh bảng    │ → │nhấn mạnh ⚠     │
│ ○ 3'           │   │ ○ 5'           │   │ ○ 5'           │
└────────────────┘   └────────────────┘   └────────────────┘
                                                   ↓
┌────────────────┐   ┌────────────────┐   ┌────────────────┐
│6 Lưu & đặt     │   │5 Viết notes    │   │4 Tái cấu trúc  │
│tên file        │ ← │hoàn chỉnh      │ ← │mạch lạc ⚠      │
│ ○ 2'           │   │ ○ 8'           │   │ ○ 7'           │
└────────────────┘   └────────────────┘   └────────────────┘
⚠ bottleneck = tái cấu trúc thông tin rời rạc từ nhiều nguồn
```

```
FUTURE STATE — ~9'/buổi
┌────────────────┐   ┌────────────────┐   ┌────────────────┐
│1 AI nhận slide │   │2 AI tóm tắt    │   │3 AI sinh câu   │
│+ ghi chú thô   │ → │notes cấu trúc  │ → │hỏi ôn tập      │
│ ○ 1'           │   │ ○ 2'           │   │ ○ 1'           │
└────────────────┘   └────────────────┘   └────────────────┘
                                                   ↓
                     ┌────────────────┐   ┌────────────────┐
                     │5 Lưu vào kho   │   │4 SV review &   │
                     │notes / sync    │ ← │chỉnh           │
                     │ ○ 1'           │   │○4' ● green     │
                     └────────────────┘   └────────────────┘
● green = human checkpoint  ·  Fallback: AI bịa -> SV đối chiếu slide gốc
```


## Tóm tắt Card #2 & #3

| Card | Actor | Bottleneck | Metric | Quick gut | Vì sao chưa chọn #1 |
|---|---|---|---|---|---|
| #2 Review LAB | SV chuẩn bị buổi lab | Định vị deliverable + rubric trong tài liệu dài | <8'/buổi; giảm hỏi lại TA; first-pass correctness | Tool | Quality "hiểu đúng" khó đo trực tiếp |
| #3 Write notes | SV sau mỗi buổi học | Tái cấu trúc thông tin rời rạc từ nhiều nguồn | <10'/buổi; ôn thi không cần mở lại slide | Tool | Khó đo notes có "đúng trọng tâm GV" không |


**Legend:** ○ = thời gian bước · ⚠ = bottleneck · ● green = human checkpoint (điểm sinh viên kiểm soát)