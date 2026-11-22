# Danh sách lớp v0 — Nguyen Son Tung · G09

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `eye_state` | `open` / `closed` / `unknown` | Phát hiện tài xế buồn ngủ (tính toán chỉ số PERCLOS - tỷ lệ thời gian mí mắt khép > 80%) và cảnh báo vi ngủ (microsleep) | Có, camera NIR cho phép quan sát rõ con ngươi và mí mắt cả ngày lẫn đêm, trừ khi kính phản xạ chói mạnh |
| 2 | `gaze_zone` | `road` / `mirror_l` / `mirror_r` / `mirror_c` / `cluster` / `center` / `lap` / `other` | Xác định vùng chú ý thị giác của tài xế, cảnh báo mất tập trung (Distraction Detection) khi mắt rời đường lái quá 2-3 giây | Có, suy luận từ hướng đồng tử và góc xoay đầu dưới ánh sáng NIR |
| 3 | `head_pose` | `pitch`, `yaw`, `roll` | Nhận diện hành vi gục đầu (ngủ gật), quay đầu nói chuyện với hành khách hoặc ngó nghiêng ra cửa sổ | Có, hình thái hộp sọ và 13 điểm mốc khuôn mặt (face13) hiển thị rõ trên IR |
| 4 | `hand_on_wheel` | `yes` / `no` / `unknown` | Giám sát tiếp xúc tay trên vô lăng (Hands-On Detection) theo quy chuẩn an toàn ADAS / Euro NCAP khi xe bật chế độ lái hỗ trợ | Có, hình dạng bàn tay và vành vô lăng phân biệt rõ nét trên IR |
| 5 | `phone_use` | `held` / `mounted` / `lap` | Phát hiện vi phạm sử dụng điện thoại khi lái xe (nghe gọi cầm tay, đặt trên đùi nhắn tin cúi nhìn) | Có, hình dạng chữ nhật và viền phản xạ kim loại/kính của điện thoại hiện rõ trên IR |
| 6 | `yawn_state` | `open_yawn` / `normal` / `talking` | Phát hiện dấu hiệu mệt mỏi giai đoạn sớm qua khẩu độ miệng mở rộng liên tục (ngáp ngủ) trước khi tài xế rơi vào ngủ gật | Có, viền môi và khoang miệng nhìn thấy rõ trên ảnh NIR |
| 7 | `smoking_state` | `smoking` / `none` | Cảnh báo hành vi hút thuốc gây giảm tập trung, khói làm mờ tầm nhìn trong khoang kín và nguy cơ hỏa hoạn | Có, đầu lọc/điếu thuốc và cử chỉ đưa tay lên miệng phát hiện được qua IR |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` | `seat` (vị trí ghế), `posture` (tư thế) | Xác định sự hiện diện hành khách để điều khiển kích hoạt cụm túi khí tương ứng (Smart Airbag Deployment Control) | Có, thân nhiệt hoặc hình khối cơ thể phân biệt rõ với ghế |
| 2 | `child_seat` | `seat`, `occupied` (`no` / `unknown`) | Nhận diện ghế trẻ em lắp trên xe để điều chỉnh lực bung túi khí hoặc vô hiệu hóa túi khí ghế trước | Có, khung nhựa cứng và đệm ghế trẻ em có hình dạng đặc thù trên IR |
| 3 | `infant_seat` | `seat`, `facing` (`rear` / `front`) | Bắt buộc ngắt túi khí hành khách phía trước khi lắp nôi trẻ em quay lưng (Rear-Facing Infant Seat) tránh gây chấn thương tử vong cho trẻ | Có, quai xách và biên dạng nôi em bé hiển thị rõ trên IR |
| 4 | `seatbelt_status` | `worn_correct` / `worn_incorrect` / `not_worn` / `unknown` | Hệ thống nhắc nhở thắt dây an toàn thông minh (Seatbelt Reminder - SBR) cho toàn bộ hàng ghế sau theo chuẩn Euro NCAP | Có phần hạn chế; IR thấy được viền dây phản xạ nếu áo sáng màu, khó thấy trên áo tối màu |
| 5 | `left_behind_child` | `present` / `absent` | Cảnh báo khẩn cấp bỏ quên trẻ em trong xe (Child Presence Detection - CPD theo Euro NCAP 2025) khi tài xế tắt máy rời xe | Có, camera IR phát hiện được chuyển động hoặc hình thái trẻ nhỏ khi xe đã tắt máy |
| 6 | `left_behind_object` | `bag` / `box` / `cup` / `other` | Cảnh báo hành khách để quên tài sản giá trị, hành lý hoặc vật nuôi trên xe khi rời cửa | Có, phân biệt được hình khối đồ vật dựa vào độ tương phản độ sáng IR |
| 7 | `zone_occupancy` | `empty` / `occupied` | Tối ưu hóa hệ thống điều hòa không khí đa vùng (Zone HVAC), tự động tắt cửa gió ở các ghế trống nhằm tiết kiệm năng lượng | Có, phân biệt ghế có người/vật hay không để điều phối luồng gió |

## 2 câu hỏi leo thang

Câu hỏi bạn muốn hỏi người viết guideline (hoặc khách hàng) vì guideline v1.0 chưa trả lời. Mỗi câu kèm **tên khung** làm ví dụ.

1. Câu hỏi: Khi ghế trẻ em là loại đa năng có thể chuyển đổi (Convertible Car Seat) dùng được cho cả trẻ sơ sinh dạng nôi quay sau và trẻ lớn dạng ghế nâng quay trước, trong trường hợp ghế đang trống thì ưu tiên gán là `child_seat` hay `infant_seat`?
   Khung ví dụ: `S01_rgb.png` (ghế bên trái ảnh / rear_right)
   Bạn tạm gán thế nào và vì sao: Tạm gán theo hình thái lắp đặt thực tế: nếu có quai xách dạng nôi di động hoặc lắp quay sau thì gán `infant_seat`; nếu là ghế cố định có đệm lưng cao và tựa đầu thì gán `child_seat`, để thuật toán phân loại đúng kích cỡ tải trọng an toàn túi khí.

2. Câu hỏi: Trong ảnh DMS (Drive&Act), khi tài xế đeo kính râm tối màu hoặc tròng kính cận bị phản xạ đốm sáng LED NIR che lấp hoàn toàn vùng con ngươi và mí mắt, quy ước chuẩn cho cờ `occluded` của 4 điểm `face13` mắt và thuộc tính `eye_state` là gì?
   Khung ví dụ: `D02.png` và `D04.png`
   Bạn tạm gán thế nào và vì sao: Tạm gán `eye_state = unknown` và bật cờ `occluded = 1` cho các điểm mốc mắt `face13`, vì theo nguyên tắc cốt lõi của Guideline Cabin v1.0: "không thấy rõ thì ghi unknown, không suy đoán", nhằm tránh đưa nhãn sai (false label) vào tập huấn luyện model nhận diện buồn ngủ.
