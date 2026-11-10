# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: Nguyen Manh Quang
- MSSV:2A202603241
- Email:quangkebg123@gmail.com
- Lớp:L2
- Link repo bài làm: https://github.com/quangkebg123/K5-L2B-DAY02-NguyenManhQuang-2A202603241-ObjectDetection
- Link Colab đã chạy:https://colab.research.google.com/github/quangkebg123/K5-L2B-DAY02-NguyenManhQuang-2A202603241-ObjectDetection/blob/main/notebooks/day2_annotation_to_yolo.ipynb#scrollTo=HbO49NoqPROj

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt ba ca mơ hồ đã quyết định, cách áp dụng schema và phần cần giảng viên làm rõ.

## 3. Annotation và self-QC

- Số file nhãn train: 50
- Kết quả checker và lỗi đã xử lý: 50 file
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: 'driver_050,'driver_013,'driver_15,'driver_16,'driver_21,'driver_23,'driver_24,'driver_25,'driver_12,'driver_11,
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa:
- Commit khóa nhãn ban đầu:

## 4. Gold QC và rework

| Chỉ số              | Trước sửa | Sau sửa nếu có |
| ------------------- | --------: | -------------: |
| TP                  |       383 |                |
| FP                  |       284 |                |
| FN                  |       270 |                |
| Precision           |    0.5742 |                |
| Recall              |    0.5865 |                |
| F1                  |    0.5803 |                |
| mean_iou_of_matches |    0.8253 |                |
| passed              |     false |                |

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Nếu rework, ghi ảnh, lỗi đã kiểm, quyết định sửa/giữ và lý do. Không suy nguyên nhân chỉ từ FP/FN. Không có rework thì ghi rõ.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch:
- Các tham số thay đổi so với notebook nếu có và lý do:
- Đường dẫn best checkpoint trong phiên chạy:

| Chỉ số trên 10 ảnh eval |             Giá trị |
| ----------------------- | ------------------: |
| Precision               |  0.3156193471665181 |
| Recall                  | 0.30664893617021277 |
| mAP50                   |  0.2739647516429376 |
| mAP50–95                | 0.20063156304965743 |

"checkpoint": "/content/Day2-Lab/outputs/yolo26_runs/vehicle_annotation/weights/best.pt"
Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?
   Không dùng 10 ảnh eval để train vì chúng ta muốn đánh giá khách quan khả năng dự đoán của model trên những dữ liệu model chưa từng học.

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
| -------------- | ------------ | ----------- | ----------------- |
|                |              |             |                   |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.

## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.
