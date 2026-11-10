# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp     | Định nghĩa của bạn                           | Ví dụ/điểm phân biệt      |
| ------- | -------------------------------------------- | ------------------------- |
| `car`   | Xe ô tô chở người, thường có tối đa 5–7 chỗ. | Sedan, SUV, hatchback.    |
| `truck` | Xe tải được chủ yếu để vận chuyển hàng hóa.  | Xe tải thùng, xe đầu kéo. |
| `bus`   | Vận chuyển nhiều hành khách                  | xe khách                  |
| `van`   | hoang hành khách liền thân.                  | Cargo van, passenger van  |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: Box chạm đúng rìa ảnh khi vật thể bị cắt khung; không đoán phần nằm ngoài ảnh.
- Vật thể bị che khuất: Vật thể bị che một phần vẫn gán box quanh phần nhìn thấy được nếu nhận diện được lớp.
- Vật thể bị cắt bởi rìa ảnh: Box chạm đúng rìa ảnh khi vật thể bị cắt khung; không đoán phần nằm ngoài ảnh.
- Vật thể rất nhỏ/mơ hồ: Nếu chỉ còn mảnh rất nhỏ, không thể xác định chắc lớp, không tự đoán. Ghi vào mini guideline và hỏi giảng viên.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh         | Tình huống                                                                   | Quyết định cuối                             | Lý do theo schema                                                 |
| ----------- | ---------------------------------------------------------------------------- | ------------------------------------------- | ----------------------------------------------------------------- |
| `drive_011` | Một xe van bị che khuất một phần bởi xe phía trước.                          | Label van, box phần nhìn thấy.              | Vẫn nhận diện được class và xác định được vùng vật thể nhìn thấy. |
| `drive_050` | Một car bị cắt mất phần đuôi.                                                | Label van, box dừng tại mép ảnh.            | Nhận diện được class, chỉ annotate phần nằm trong ảnh.            |
| `drive_011` | Một số phương tiện ở xa, kích thước rất nhỏ, không phân biệt rõ car hay van. | Đưa reviewer kiểm tra, không tự đoán class. | Không đủ bằng chứng để xác định class theo schema.                |
