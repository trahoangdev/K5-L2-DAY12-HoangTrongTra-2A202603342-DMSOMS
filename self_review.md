# Tự đánh giá — Hoàng Trọng Trà · G02

Bản nháp dựa trên lịch sử sửa nhãn, XML xuất từ CVAT và nhật ký IR. Hoàng Trọng Trà cần tự đối chiếu lại trong CVAT trước khi xác nhận phần tự đánh giá.

## 1. Tự rà soát 4 cảnh

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| `S01_ir.png` | Nôi ở `rear_left` | `wrong_class` | Ban đầu là `child_seat`. Bản cuối có `infant_seat`, `seat=rear_left`, `facing=rear`. | Có |
| `S02_ir.png` | Nôi ở `rear_right` | `missing` | Checkpoint A chưa có box nôi. Bản cuối có `infant_seat`, `facing=rear`. Cách xử lý nôi có hình giống em bé cần coach xác nhận. | Đã thêm box |
| `D02.png` | Hai mắt trong `face13` | `ok` | XML ghi `left_eye_outer` có y = 521,79 và `right_eye_outer` có y = 417,03, phù hợp chiều ảnh xoay của D##. | Không cần |
| `D04.png` | Môi và khóe miệng trong `face13` | `ok` | Cổ chai che miệng. XML ghi `occluded=1` cho giữa môi trên và dưới, `outside=1` cho hai khóe không xác định được. | Không cần |

## 2. Lỗi lặp lại

Hai cặp S01 và S02 đều phải sửa cách xử lý nôi. Lần đầu, S01 bị nhầm sang ghế trẻ em. S02 bị bỏ sót box nôi khi xử lý ca có hình giống em bé.

Lần sau, kiểm từng ghế theo hệ quy chiếu của xe trước khi gán. Đối chiếu hình dạng để phân biệt nôi và ghế trẻ em, rồi ghi riêng phần chưa xác định được về người hoặc vật bên trong.

## 3. Ghi chú về disagreement_log

Mình đã xác nhận phần review chéo với Dương Trí Dũng (2A202603341), cùng mã G02. `disagreement_log.csv` ghi kết quả và hướng xử lý cho 94 dòng bất đồng.

Một ca giúp mình hiểu rõ guideline là `S02_rgb.png`, ở ghế `rear_left`. Bản mình ghi `child_seat.occupied=unknown`, còn Dũng ghi `no`. Dòng này được ghi `ambiguous` trong CSV. Theo GUIDE §4.8, `no` phù hợp khi nhìn rõ lòng ghế trống trên chính ảnh RGB. Nếu lòng ghế vẫn quá tối hoặc bị che thì giữ `unknown`. Khi gặp ca tương tự, mình sẽ kiểm tra RGB ở mức sáng phù hợp trước khi chọn giá trị.
