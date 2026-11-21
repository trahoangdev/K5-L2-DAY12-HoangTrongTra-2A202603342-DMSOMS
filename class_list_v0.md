# Danh sách lớp v0 — Hoàng Trọng Trà · G02

## DMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `face.eye_left`, `face.eye_right` | `open` / `closed` / `unknown` cho từng mắt | Kết hợp nhiều khung để đo thời gian nhắm mắt, phục vụ phát hiện buồn ngủ. | Có khi thấy khe mắt. Phản xạ và vùng tối có thể làm mất dấu mí. |
| 2 | `face.gaze_zone` | `road`, `mirror_l`, `mirror_r`, `mirror_c`, `cluster`, `center`, `lap`, `other` | Ước lượng tài xế đang hướng chú ý về đâu và theo dõi thời gian rời mắt khỏi đường. | Phụ thuộc góc đầu, mức thấy mắt và thông tin về vị trí camera. |
| 3 | `face13` | 13 điểm mặt, mỗi điểm có cờ `occluded` và `outside` | Tính độ mở mắt và hỗ trợ ước lượng hướng đầu từ các điểm tin cậy. | Có với mốc nhìn rõ. Kính, tay và chai có thể che điểm. |
| 4 | `face.glasses` | `unknown` / `none` / `clear` / `sun` | Điều chỉnh độ tin cậy của phép đo mắt khi kính che hoặc gây phản xạ. | Thường thấy gọng. Độ sáng của tròng trên NIR có thể làm loại kính khó xác định. |
| 5 | `hand.on_wheel` | `yes` / `no` / `unknown`, theo từng tay và người | Theo dõi tay tài xế có tiếp xúc vô lăng khi chức năng hỗ trợ lái cần tín hiệu này. | Có nếu nhìn rõ bàn tay và vị trí tiếp xúc. |
| 6 | `phone.state` | `held` / `mounted` / `lap` | Phân biệt điện thoại cầm tay với máy gắn trên giá hoặc đặt trên đùi để hỗ trợ đánh giá thao tác gây xao nhãng. | Có khi nhận ra cạnh, góc hoặc màn hình. |
| 7 | `person.seatbelt` | `worn_correct` / `worn_incorrect` / `not_worn` / `unknown` | Phát hiện dây an toàn của tài xế chưa cài hoặc đi sai vị trí. | Có khi theo được dải dây qua vai và thân. |

## OMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` | Box người lớn theo ghế | Xác định ghế có hành khách để nhắc dây an toàn đúng chỗ. | Thường thấy hình dáng người. Vật cản có thể che một phần cơ thể. |
| 2 | `seat` | `driver`, `front_passenger`, `rear_left`, `rear_middle`, `rear_right` | Gắn người hoặc vật với vị trí ghế theo hệ quy chiếu của xe. | Suy được từ hình học cabin khi thấy được hàng ghế. |
| 3 | `child_seat.occupied` | `unknown` / `no` / `yes` theo Raw cập nhật của coach | Phân biệt ghế trẻ em trống với ghế có người ngồi để hỗ trợ giám sát theo ghế. | Có khi thấy rõ lòng ghế. Bóng tối hoặc vật che làm trạng thái khó xác định. |
| 4 | `infant_seat.facing` | `rear` / `front` | Xác định hướng lắp nôi để hệ thống đối chiếu với vị trí ghế. | Có khi đường viền và thế đặt nôi còn rõ. |
| 5 | `object.type` | `bag` / `box` / `cup` / `other` | Phân biệt đồ vật trên ghế với hành khách để giảm nhắc nhầm. | Dựa vào hình dạng. Dấu hiệu màu bị mất và vật nhỏ có thể khó phân loại. |
| 6 | `frame_meta.camera_blocked` | `yes` / `no` | Phát hiện tầm nhìn camera bị che để hệ thống đánh dấu kết quả giám sát có độ tin cậy thấp. | Có khi vật che hoặc phần ảnh mất tầm nhìn thể hiện rõ. |

## 2 câu hỏi leo thang

1. **Khung ví dụ:** `S02_rgb.png`, `S02_ir.png`. Ở `rear_right` có nôi quay về sau và hình giống em bé nằm trong nôi. Khi GUIDE §4.1 mô tả `infant_seat` cho nôi trống, coach muốn giữ box nôi hay xử lý ca này theo quy tắc riêng? Bản hiện tại giữ box `infant_seat` với `seat=rear_right`, `facing=rear` vì hình dạng và hướng của nôi nhận ra được. Phần hình trong nôi đang chờ xác nhận.
2. **Khung ví dụ:** `D03.png`. Thấy rõ gọng kính đang đeo, còn tròng trên NIR khá tối và có phản xạ. Coach dùng dấu hiệu nào để phân biệt `clear` với `sun` khi sắc độ NIR khó diễn giải? Bản hiện tại dùng `glasses=unknown` vì nhìn thấy gọng nhưng chưa đủ bằng chứng để xác định loại tròng.
