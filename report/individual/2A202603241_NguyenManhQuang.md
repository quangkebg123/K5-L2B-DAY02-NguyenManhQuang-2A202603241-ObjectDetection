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
- Commit khóa nhãn ban đầu:https://github.com/quangkebg123/K5-L2B-DAY02-NguyenManhQuang-2A202603241-ObjectDetection/commit/07ce52d023d9b877c5c3c7183dfa7ffa86a8afbb

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
   `bus` có recall thấp nhất: đường cong Recall-Confidence của lớp bus giảm về 0 ở ngưỡng confidence thấp (xem `assets/yolo26_runs/vehicle_eval/BoxR_curve.png`); confusion matrix cũng không có true positive cho bus. `drive_051` minh họa trường hợp này: nhãn ground truth có một bus nhưng ảnh dự đoán không nhận diện nó là bus (bị nhầm lớp hoặc bỏ sót). Xem [ảnh dự đoán](assets/eval_predictions/visuals/drive_051.jpg) và nhãn [drive_051.txt](../../dataset/labels/eval/drive_051.txt).

2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
   Điều đó thường cho thấy box đủ chồng lấn để đạt ngưỡng IoU 0.50 nhưng chưa định vị sát và ổn định ở các ngưỡng IoU cao hơn. Cần so sánh box dự đoán với ground truth: box lệch tâm, quá rộng/nhỏ, cắt mất xe, hoặc nhập hai xe gần nhau. Không thể kết luận nguyên nhân chỉ từ hai chỉ số; cần kiểm tra ảnh dự đoán cụ thể.

3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
   Cần kiểm tra nhầm lẫn `bus`/`van` và `car`/`van`. Trong `GUIDELINE_MINI.md`, định nghĩa `van` chưa rõ ràng, còn ca `drive_050` ghi tình huống là `car` bị cắt ảnh nhưng quyết định lại là `van` mà không nêu căn cứ phân biệt lớp. Dữ kiện đầu ra cũng đáng rà soát: nhãn `drive_053.txt` gán vật thể xe buýt lớn là class `van`, trong khi ảnh dự đoán gọi vật thể đó là `bus` ([ảnh dự đoán](assets/eval_predictions/visuals/drive_053.jpg)). Đây là dấu hiệu có thể liên quan đến ranh giới guideline/nhãn; cần người rà ảnh xác nhận, không thể khẳng định guideline là nguyên nhân duy nhất.

4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?
   Không đưa 10 ảnh eval vào cập nhật trọng số để tránh rò rỉ dữ liệu và giữ phép đánh giá có ý nghĩa. Tuy nhiên, theo notebook, tập này được dùng làm `val` trong lúc train và để chọn `best.pt`; vì vậy nó là validation set, không phải test set độc lập hoàn toàn. Không nên gọi đây là dữ liệu mô hình chưa từng được dùng trong quá trình phát triển.

## 6. Khó khăn và cách xử lý

| Bước/thời điểm       | Lỗi quan sát                                            | Cách đã thử                                 | Kết quả/còn thiếu                                              |
| -------------------- | ------------------------------------------------------- | ------------------------------------------- | -------------------------------------------------------------- |
| Annotation trên CVAT | Bounding Box quá rộng hoặc quá hẹp, chưa ôm sát vật thể | Kiểm tra và chỉnh sửa Bounding Box thủ công | Box chính xác hơn, nhưng cần tiếp tục kiểm tra toàn bộ dataset |

## 7. Tự đánh giá theo rubric

dc 70d
Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.

## 8. Công cụ AI và tài liệu tham khảo

cong cu su dung Cvat
Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.
