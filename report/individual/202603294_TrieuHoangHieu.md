# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: Triệu Hoàng Hiếu
- MSSV: 2A202603294
- Email: 26ai.hieuth@vinuni.edu.vn
- Lớp: L2B
- Link repo bài làm: https://github.com/hieuwewe123/K5-L2-Day02-TrieuHoangHieu-2A202603294-ObjectDetection.git
- Link Colab đã chạy:

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt ba ca mơ hồ đã quyết định, cách áp dụng schema và phần cần giảng viên làm rõ.

## 3. Annotation và self-QC

- Số file nhãn train: 50.
- Kết quả checker và lỗi đã xử lý: lần chạy gần nhất đạt 50/50. Đã sửa các box vượt biên được checker báo ở drive_002, drive_009, drive_015, drive_027, drive_029 và drive_048; chạy lại checker đạt.
- Danh sách ít nhất 10 ảnh đã rà bằng mắt:
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa:
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

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Lần chạy sau khi sửa các box vượt biên cho kết quả F1 0.8477 và mean IoU 0.9318. Ghi rõ các ảnh đã kiểm và quyết định rework sau khi tự đối chiếu ảnh; không suy nguyên nhân chỉ từ FP/FN.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch:
- Các tham số thay đổi so với notebook nếu có và lý do:
- Đường dẫn best checkpoint trong phiên chạy:

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision | |
| Recall | |
| mAP50 | |
| mAP50–95 | |

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| | | | |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.

## 8. Công cụ AI và tài liệu tham khảo

Đã dùng Copilot/AI assistant trong VS Code để giải thích các bước của lab và hỗ trợ diễn đạt mini guideline. Trước khi nộp, tự kiểm tra các quyết định trong guideline và tự chịu trách nhiệm về nhãn. Liệt kê thêm nguồn ngoài repo nếu có. Không ghi mật khẩu/token hoặc đính kèm gold train.
