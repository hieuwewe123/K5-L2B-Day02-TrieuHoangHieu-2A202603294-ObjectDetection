# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` | Xe con, sedan, SUV, taxi hoặc xe bán tải. | Không xếp xe buýt, xe tải hoặc mô tô vào lớp này. |
| `truck` | Xe tải chở hàng hoặc xe đầu kéo. | Phân biệt với xe bán tải/cabin nhỏ thuộc `car`. |
| `bus` | Xe buýt hoặc minibus chở khách. | Van/minivan không xếp vào `bus`. |
| `van` | Xe van hoặc minivan chở hàng hay chở người. | Phân biệt với xe buýt lớn (`bus`) và xe con thông thường (`car`). |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: ôm sát phần thân xe nhìn thấy được, không lấy thừa nền hoặc xe bên cạnh.
- Vật thể bị che khuất: vẽ box riêng quanh phần nhìn thấy nếu vẫn nhận diện được lớp; không gộp các xe.
- Vật thể bị cắt bởi rìa ảnh: box chạm đúng mép ảnh, không đoán phần xe nằm ngoài khung.
- Vật thể rất nhỏ/mơ hồ: không tự đoán lớp nếu phần nhìn thấy không đủ để nhận diện; ghi lại và hỏi giảng viên.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_009` | Ùn tắc; xe lớn che khuất một phần hoặc gần hết xe nhỏ. | Vẽ box riêng cho xe nhỏ nếu còn phần nhìn thấy đủ để nhận diện; không gán xe bị che hoàn toàn hoặc không xác định được lớp. | Chỉ gán xe thuộc schema có thể nhận diện từ phần quan sát được; không suy đoán phần bị che. |
| `drive_012` | Nhiều xe con và xe thuộc các loại khác che khuất nhau. | Tách box theo từng xe; gán lớp theo phần nhìn thấy được, không để xe phía trước che mất box của xe phía sau nếu xe đó vẫn nhận diện được. | Mỗi xe có một box riêng và class theo loại xe; không đoán phần bị che. |
| `drive_006` | Nhiều xe ở xa, rất nhỏ/mờ và chen lấp nên không xác định chắc loại xe. | Không gán những xe không thể nhận diện chắc lớp; hỏi giảng viên nếu cần xác nhận. | Chỉ gán vật thể thuộc schema khi có đủ dấu hiệu nhận diện, tránh đoán class. |
