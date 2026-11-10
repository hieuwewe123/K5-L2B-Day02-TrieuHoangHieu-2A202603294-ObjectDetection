# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: Triệu Hoàng Hiếu
- MSSV: 202603294
- Email: 26ai.hieuth@vinuni.edu.vn
- Lớp: L2B
- Link repo bài làm: https://github.com/hieuwewe123/K5-L2B-Day02-TrieuHoangHieu-2A202603294-ObjectDetection.git
- Link Colab đã chạy: https://colab.research.google.com/github/hieuwewe123/K5-L2B-Day02-TrieuHoangHieu-2A202603294-ObjectDetection/blob/main/notebooks/day2_annotation_to_yolo.ipynb

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

- Runtime: Google Colab, Python 3.13.16, Tesla T4 (CUDA:0); Ultralytics 8.4.208, PyTorch 2.14.1+cu130.
- Mô hình: YOLO26n; đánh giá `best.pt` trên 10 ảnh eval (113 instances).
- Checkpoint trong phiên Colab: `/content/Day2-Lab/outputs/yolo26_runs/vehicle_annotation/weights/best.pt`.

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision | 0.4043 |
| Recall | 0.3721 |
| mAP50 | 0.3762 |
| mAP50–95 | 0.2572 |

Theo kết quả per-class, `bus` có recall thấp nhất (0/2 instances); tiếp theo là `van` (0.0481, 12 instances), `truck` (0.600, 5 instances), và `car` (0.840, 94 instances). Số lượng eval của `bus` và `truck` ít nên các chỉ số này biến động mạnh.

Quan sát [ảnh prediction drive_053](assets/eval_predictions/visuals/drive_053.jpg): model dự đoán thừa một `van` dù ảnh không có van (false positive); box dự đoán cho `bus` cũng rộng hơn vật thể thực tế. Ở [drive_058](assets/eval_predictions/visuals/drive_058.jpg), có nhóm ba xe bus bị gom trong một box và nhóm hai xe bus bị gom trong một box, thay vì một box riêng cho từng xe; đây là lỗi tách vật thể và localization. Các artifacts gồm [kết quả train](assets/yolo26_runs/vehicle_annotation/results.csv), [confusion matrix eval](assets/yolo26_runs/vehicle_eval/confusion_matrix.png) và [PR curve eval](assets/yolo26_runs/vehicle_eval/BoxPR_curve.png).

1. Recall thấp nhất là `bus` (0/2 instances). `drive_058` minh họa dự đoán không tách từng xe bus thành box riêng; `drive_053` có box bus rộng hơn vật thể.
2. mAP50–95 thấp hơn mAP50 vì metric này kiểm tra box ở nhiều ngưỡng IoU cao hơn; cần xem box có ôm sát và đúng ranh giới vật thể không.
3. Ảnh `drive_053` có dự đoán thừa `van`; cần đối chiếu ảnh và guideline phân biệt `van` với các lớp khác. Một ảnh chưa đủ để kết luận nguyên nhân tổng thể.
4. Không dùng eval để train để tránh rò rỉ dữ liệu đánh giá. Notebook dùng eval làm validation để theo dõi/chọn checkpoint và đánh giá, nên eval không phải test set độc lập.

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
- Pipeline YOLO: Đã chạy YOLO26n trên Colab và đánh giá trên 10 ảnh eval; metrics và nhận xét lỗi được ghi ở mục 5.

Đối chiếu chi tiết theo [RUBRIC.md](../../RUBRIC.md). Các nhận xét về độ đầy đủ, độ sát box và tính nhất quán lớp là tự đánh giá, không thay thế kết quả gold-set.

## 8. Công cụ AI và tài liệu tham khảo

Đã dùng Copilot/AI assistant trong VS Code để giải thích các bước của lab và hỗ trợ diễn đạt mini guideline. Trước khi nộp, tự kiểm tra các quyết định trong guideline và tự chịu trách nhiệm về nhãn. Liệt kê thêm nguồn ngoài repo nếu có. Không ghi mật khẩu/token hoặc đính kèm gold train.
