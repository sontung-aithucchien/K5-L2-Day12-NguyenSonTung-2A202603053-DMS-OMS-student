# Tự đánh giá — Nguyen Son Tung · G09

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_rgb.png | infant_seat, child_seat | ok | Vị trí ghế gọi chuẩn theo xe: bên trái ảnh là rear_right, bên phải ảnh là rear_left. Hộp bao sát vật | Đã chuẩn |
| S02_ir.png | child_seat | wrong_class | Ban đầu nhầm lẫn thuộc tính occupied='yes', theo schema guideline chỉ cho phép no/unknown | Đã sửa về 'no' |
| D01.png | face13, hand | ok | Mắt trái người lái có y lớn hơn mắt phải do ảnh xoay 90°; đủ 13 điểm face13; 2 tay phân biệt left/right chuẩn theo người | Đã chuẩn |
| D02.png | face, face13 | flag | Mắt bị che khuất một phần bởi góc nghiêng và tay, cần bật occluded=1 cho các điểm mắt tương ứng | Đã xử lý và giải thích trong check_final.txt |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Nhầm lẫn quy ước tọa độ và trái/phải trên ảnh DMS do ảnh bị xoay ~90°, cũng như gán thuộc tính `occupied` cho `child_seat`.

Vì sao mình mắc:
1. Thói quen thị giác phản xạ nhìn ảnh thông thường: dễ nhìn mắt bên trên là mắt trái, nhưng trên ảnh xoay 90° (đầu quay sang phải), mắt trái của người lái thực tế nằm thấp hơn trên màn hình (tọa độ y lớn hơn).
2. Chưa đọc kỹ schema của `child_seat` trong `labels_cabin_v1.json`, quen suy nghĩ "ghế trẻ em có người ngồi thì occupied=yes", trong khi guideline quy định ghế trẻ em chỉ gán khi trống (`occupied=no/unknown`), người ngồi bên trong phải có box `person` riêng.

Lần sau tránh bằng cách:
1. Luôn tự xoay đầu hoặc nghiêng người theo góc nhìn của tài xế trước khi đánh dấu keypoints `face13` và thuộc tính `hand`. Kiểm tra chéo: mắt trái của người luôn có y lớn hơn mắt phải trên ảnh xoay 90°.
2. Đọc kỹ file định nghĩa `labels_cabin_v1.json` và bảng quy đổi nhãn trong GUIDE §4.1 trước khi bắt đầu gán nhãn, chạy script `cabin_check.py` thường xuyên ở từng checkpoint để phát hiện sớm.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó:
Tại ảnh D04.png, đối tượng `hand` (tay trái tài xế): Mình gán `on_wheel = yes` theo phản xạ thói quen nghĩ rằng tài xế phải luôn cầm vô lăng. Bạn Phạm Quang Nam gán `on_wheel = no`. Sau khi đối chiếu lại khung hình và tham chiếu GUIDE §3 & COMMON_ERRORS §DMS ("Drive&Act quay xe ở chế độ tự lái: tay rời vô lăng là bình thường"), mình nhận thấy tay tài xế đang buông khỏi vành lái để thao tác khác. Bạn Nam đã đúng, mình đã tiếp thu và cập nhật sửa giá trị này về `no` trong `export_final_v2.zip`.
