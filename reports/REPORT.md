# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602282
- Ngày / CVAT local: 17/09/2026 / CVAT local
- Công cụ đã dùng: CVAT local, Brush/Polygon

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic | 2 / 2 | 30 |
| cp1_holes | cp1_holes | 1 / 1 | 3 |
| cp2_slice | cp2_slice | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion | 1 / 1 | 3 |
| cp3_thin | cp3_thin | 1 / 1 | 3 |
| cp4_curb | cp4_curb | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage | 1 / 1 | 3 |
| **Tổng tối đa** | | 14 / 14 | **100** |

## 2. Một quyết định trước khi dùng gợi ý

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: 000000181542.jpg, người ở vùng giữa lệch trái ảnh, khoảng từ (189,131) đến (306,462).
- Class và quy tắc tôi dùng để chọn biên: person; tôi chỉ lấy phần người nhìn thấy trong ảnh, bám theo đường viền cơ thể và không mở rộng mask vào nền hoặc vật phía sau.
- Nếu dùng gợi ý sau đó: tôi kiểm tra lại mask theo biên nhìn thấy, đặc biệt ở vùng tiếp giáp với các object khác; phần nào không đúng biên thì chỉnh lại thay vì giữ nguyên gợi ý.
- Nếu không dùng gợi ý: quyết định đầu tiên được thực hiện thủ công theo phần nhìn thấy của object và quy tắc biên của task.

## 3. Một lỗi tôi tìm thấy và sửa

- Task/ảnh/vùng: cp2_slice, vùng giữa ảnh có các xe nằm sát nhau.
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: gộp-tách.
- Bằng chứng tôi nhìn thấy: các xe cùng class nằm gần nhau nên nếu vẽ liền một mask sẽ làm mất ranh giới giữa hai instance.
- Quy tắc và hành động sửa: tôi kiểm tra từng xe là một instance riêng, tách mask theo đường biên nhìn thấy giữa các xe và kiểm tra lại danh sách object trước khi Save.
- Sau sửa đã Save và export lại chưa? Có.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1 | Có thể xem phần nhỏ sát mép là một phần của person hoặc nền/đối tượng khác | Chỉ gán phần có dấu hiệu rõ là cơ thể người và nằm trong vùng nhìn thấy | Giữ riêng từng person, không mở rộng mask vào nền |
| 2 | Có thể gộp các xe sát nhau hoặc tách thành nhiều instance | Task yêu cầu hai xe sát nhau vẫn là hai instance riêng | Tách từng xe thành một instance |
| 3 | Có thể chọn ranh theo màu ảnh hoặc theo mép bó vỉa/chức năng sử dụng | Quy tắc task ưu tiên ranh road–sidewalk theo chức năng/bó vỉa, không chỉ theo màu | Chọn ranh theo mép bó vỉa và chức năng của vùng đường/vỉa hè |
