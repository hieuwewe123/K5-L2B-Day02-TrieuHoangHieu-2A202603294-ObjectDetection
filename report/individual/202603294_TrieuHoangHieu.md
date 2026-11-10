# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: Triệu Hoàng Hiếu
- MSSV: 2A202603294
- Email: 26ai.hieuth@vinuni.edu.vn
- Lớp: L2B
- Link repo bài làm: https://github.com/hieuwewe123/K5-L2B-Day02-TrieuHoangHieu-2A202603294-ObjectDetection.git
- Link Colab đã chạy:

## 2. Schema và mini guideline

Dùng schema cố định `car=0`, `truck=1`, `bus=2`, `van=3`; mỗi xe được gán một box riêng quanh phần nhìn thấy nếu còn nhận diện được. Trong `drive_009`, xe lớn che khuất xe nhỏ; trong `drive_012`, các loại xe che khuất nhau; trong `drive_006`, xe ở xa quá nhỏ/mờ nên khó xác định lớp. Không suy đoán xe bị che hoàn toàn hoặc không thể nhận diện. Guideline chi tiết: [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Cần hỏi giảng viên cách xử lý thống nhất với xe quá nhỏ hoặc bị che đến mức không thể xác định lớp.

## 3. Annotation và self-QC

- Số file nhãn train: 50.
- Kết quả checker và lỗi đã xử lý: lần chạy gần nhất đạt 50/50. Đã sửa các box vượt biên được checker báo ở drive_002, drive_009, drive_015, drive_027, drive_029 và drive_048; chạy lại checker đạt.
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: `drive_002`, `drive_003`, `drive_004`, `drive_005`, `drive_006`, `drive_009`, `drive_011`, `drive_012`, `drive_017`, `drive_019`.
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa: Các ca khó đã ghi nhận ở `drive_006` (xe ở xa, nhỏ/mờ, chen lấp), `drive_009` (xe nhỏ bị xe lớn che khuất) và `drive_012` (các xe che khuất nhau). Chỉ gán xe còn nhận diện được và vẽ box quanh phần nhìn thấy; không đoán xe/lớp bị che hoàn toàn.
- Commit khóa nhãn ban đầu: Không tạo commit trước khi nhận gold labels.

## 4. Gold QC và rework

| Chỉ số | Trước sửa | Sau sửa nếu có |
|---|---:|---:|
| TP | 530 | 551 |
| FP | 117 | 96 |
| FN | 123 | 102 |
| Precision | 0.8192 | 0.8516 |
| Recall | 0.8116 | 0.8438 |
| F1 | 0.8154 | 0.8477 |
| mean_iou_of_matches | 0.9295 | 0.9318 |
| passed | true | true |

Dữ liệu kết quả: [annotation_evaluation.json](../../outputs/annotation_evaluation.json). Sau khi sửa các box vượt biên, lần chạy cuối đạt F1 0.8477 và mean IoU 0.9318 (`passed: true`). Rework được thực hiện trên các nhãn sinh viên; không chỉnh sửa gold labels.

## 5. Kết quả YOLO



## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| Self-QC nhãn YOLO | Checker báo một số box vượt biên ở `drive_002`, `drive_009`, `drive_015`, `drive_027`, `drive_029`, `drive_048`. | Chỉnh các box trong nhãn tương ứng, chạy lại checker và evaluator. | Checker đạt 50/50; evaluator sau chỉnh sửa đạt F1 0.8477, mean IoU 0.9318. |
| Gán nhãn xe xa/che khuất | Một số xe nhỏ, mờ hoặc bị xe khác che làm khó xác định lớp. | Chỉ gán khi còn nhận diện được lớp; không đoán vật thể bị che hoàn toàn. | Ghi các trường hợp vào mini guideline; cần hỏi giảng viên nếu chưa rõ cách xử lý ca không thể nhận diện. |

## 7. Tự đánh giá theo rubric

- Định dạng nhãn: có 50 file train và checker đạt 50/50.
- Guideline: đã ghi schema, quy tắc box và ba ca mơ hồ.
- Gold-set QC: F1 0.8477 và mean IoU 0.9318, đạt ngưỡng yêu cầu.
- Self-QC: đã rà 10 ảnh train được liệt kê ở mục 3.
- Pipeline YOLO: 

Đối chiếu chi tiết theo [RUBRIC.md](../../RUBRIC.md). Các nhận xét về độ đầy đủ, độ sát box và tính nhất quán lớp là tự đánh giá, không thay thế kết quả gold-set.

## 8. Công cụ AI và tài liệu tham khảo

Đã dùng Copilot/AI assistant trong VS Code để giải thích các bước của lab và hỗ trợ diễn đạt mini guideline. Trước khi nộp, tự kiểm tra các quyết định trong guideline và tự chịu trách nhiệm về nhãn. Liệt kê thêm nguồn ngoài repo nếu có. Không ghi mật khẩu/token hoặc đính kèm gold train.
