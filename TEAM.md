# TEAM — Ngày 12

Mã bộ ảnh: **G09** · Hình thức: cá nhân

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Nguyen Son Tung | 2A202603053 | có | Phạm Quang Nam | 83 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- D02.png (face, face13): Thảo luận về việc tài xế cúi đầu nghiêng mặt, mắt mở nhưng hốc mắt và góc chụp làm tối 4 điểm mắt (gắn occluded=1). Thống nhất theo nguyên tắc: điểm bị che khuất thì bật occluded=1, thuộc tính eye_state ghi nhận theo trạng thái mở/khép thực tế quan sát được.

## Cá nhân

Mỗi người một mục, 1–2 dòng mỗi ý.

### NguyenSonTung-2A202603053
- Phần mình làm: Hoàn thành 22 ảnh cốt lõi, chạy script `cabin_check.py diff` với bài làm của bạn Phạm Quang Nam (`phamquangnam.zip`), đối chiếu và xử lý toàn bộ 83 dòng bất đồng trong `disagreement_log.csv`, cập nhật sửa đổi trong `export_final_v2.zip` và chạy kiểm tra `check_final_v2.txt`.
- Điều mình học được hôm nay: Nhận thức rõ sự khác biệt giữa quy ước xe và quy ước ảnh (camera OMS nhìn về sau thì trái ảnh là phải xe); học hỏi từ bạn Nam về việc cẩn trọng quan sát hành vi vô lăng trong xe tự lái (`on_wheel=no` ở D04); và tầm quan trọng của việc kiểm tra kỹ schema (`child_seat occupied` không được gán `yes`).
