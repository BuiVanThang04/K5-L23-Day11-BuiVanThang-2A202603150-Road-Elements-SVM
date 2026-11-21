# Phiếu QC 1 — Road v1.0

**Lô được kiểm** — Phạm Văn Hùng  
**Người kiểm** — Bùi Văn Thắng  
**Mã học viên người kiểm** — 2A202603150  
**Ngày kiểm** — 21/11/2026  
**File được kiểm** — `phamvanhung-front.zip` và `phamvanhung-fisheye.zip`. Chưa có manifest kèm theo để xác nhận `revision`.  
**Số ảnh kiểm** — 6 ảnh bắt buộc, 0 ảnh thêm.  
**Số nhãn đã kiểm** — 77, gồm 53 hình và 24 tag.

Mình chọn 3 ảnh camera trước và 3 ảnh fisheye để kiểm vạch làn, vùng lái, đèn, biển và quy tắc riêng của camera bên. Hình được đối chiếu trực tiếp với ảnh gốc của lab. Ký hiệu `#` là thứ tự hình trong XML của từng ảnh, bắt đầu từ 0. Tọa độ tính theo pixel ảnh gốc.

| Ảnh | Hình | Tag | Tổng nhãn |
| --- | ---: | ---: | ---: |
| A01 | 9 | 4 | 13 |
| A04 | 9 | 4 | 13 |
| A08 | 17 | 4 | 21 |
| B02 | 5 | 4 | 9 |
| B03 | 9 | 4 | 13 |
| B06 | 4 | 4 | 8 |
| **Tổng** | **53** | **24** | **77** |

## Tổng hợp theo mã

| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 tag | 0 | nặng với camera, nhẹ với tag khác |
| QC1-02 đủ L1, R1 | bỏ sót | 6 vị trí trên 3 ảnh front | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 12 vạch | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 9 vạch front | 4 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 12 vạch | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 12 vạch | 1 | chính |
| QC1-07 vùng lái và vạch qua đường | sai phạm vi / bỏ sót / thừa | 14 polygon | 3 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 13 box đèn | 4 | chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 26 box đèn và biển | 1 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 14 mục, gồm 13 box và 1 biển bị bỏ sót | 1 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 4 polyline và 8 cờ `edge_zone` | 0 | chính |
| QC1-12 file | lỗi file | 2 ZIP | 0 | nhẹ / nặng |

## Danh sách lỗi

| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| ---: | --- | --- | --- | --- | --- |
| 1 | QC1-04 | A01 | `lane #2` · R1 | chính | Điểm đầu ở khoảng (723, 719) kéo qua đầu gần nhìn thấy của vệt trắng ở khoảng (650, 678). Cắt phần kéo xuống đáy ảnh và đặt điểm đầu trên tâm vệt sơn. |
| 2 | QC1-04 | A01 | `lane #3` · R2 | chính | Vạch vàng dừng tại (529, 524), trong khi còn nhìn thấy đoạn vạch tiếp tục về phía xa, qua khoảng (470, 513). |
| 3 | QC1-06 | A01 | `lane #0` · L2 | chính | Mép trái có hai nét trắng song song thấy rõ ở phần gần. Sửa `kind=single` thành `double`. |
| 4 | QC1-04 | A04 | `lane #0` · L1 | chính | Vạch vàng đôi dừng ở (487, 365), trước đoạn sơn vẫn nhìn thấy gần (525, 344). Kéo tiếp tới phần sơn xa nhất còn nhìn rõ. |
| 5 | QC1-04 | A04 | `lane #2` · R2 | chính | Điểm gần ở (1218, 514), nhưng cặp vạch trắng còn chạy tới sát mép phải ảnh quanh hàng y=530. Bổ sung đoạn nhìn thấy ở đầu gần. |
| 6 | QC1-07 | A08 | `drivable #2` · direct | chính | Polygon tự cắt gần biên phải của vùng lái. Hai cạnh giao nhau là (822, 524) → (653.5, 320) và (762, 447) → (600, 302). Vẽ lại viền theo một vòng liên tục. |
| 7 | QC1-08 | A08 | `traffic_light #8` | chính | Box (290, 175)–(302, 201) bao tấm màu cam trên cột. Ảnh phóng to không cho thấy mặt đèn người đi bộ ở vị trí này. Rà lại và bỏ nhãn đèn nếu đối chiếu xác nhận đó là tấm biển. |
| 8 | QC1-08 | A08 | `traffic_light #9` | chính | Box (415, 188)–(424, 218) ôm một tấm trắng hẹp trên cột. Không thấy cụm đèn người đi bộ hoặc tín hiệu xanh trong box. Rà lại đối tượng trước khi gán màu. |
| 9 | QC1-10 | A08 | Thiếu `traffic_sign` | chính | Có biển đứng bên phải gần (1001, 224), với ký hiệu vòng đỏ, chưa có box. Gán box sát mép tấm biển nhìn rõ. |
| 10 | QC1-08 | B02 | `traffic_light #2` | chính | Box góc trên trái bắt đầu ở y=86 và chứa phần cột phía trên vỏ đèn. Thu mép box sát vỏ, phần vỏ bắt đầu khoảng y=112. |
| 11 | QC1-08 | B02 | `traffic_light #3` | chính | Box góc trên phải (1080, 15)–(1200, 195) bao hai cụm vỏ nhìn thấy. Tách box theo từng cụm. |
| 12 | QC1-07 | B03 | `drivable #3` · alternative | chính | Biên phải chạy qua phần đảo nổi cạnh cọc vàng, khoảng (1090, 465). Cắt polygon theo mép phần đường xe chạy. |
| 13 | QC1-09 | B03 | `traffic_sign #8` | chính | Biển xanh tròn có mũi tên trắng chỉ hướng phải đi quanh đảo. Đổi `group=information` thành `mandatory`. |
| 14 | QC1-07 | B06 | `drivable #2` · direct | chính | Mép xa của polygon phủ lên dải phân cách nổi gần hàng y=40–80 và đoạn sau cọc. Cắt theo mép mặt đường ở phía xe. |

## Ca mơ hồ

| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A08 | Lint báo thiếu L1. Ở phần gần xe chưa thấy vạch sơn dọc bên trái đủ rõ để xác định L1. Slide của lớp có yêu cầu L1 ở ảnh này và vạch cụ thể là đoạn nào? | Chờ xác nhận. Chưa tính là lỗi nặng. |
| B03 | Ở camera sau, `position` của vạch phía phải ảnh tính theo hướng xe hay theo chiều nhìn của ảnh? | Chờ xác nhận. Chưa tính vào lỗi `position`. |
| B06 | Dải trắng ngay sát đảo ở `lane #0` là vạch sơn trên mặt đường hay phần mép đảo? | Chờ xác nhận. Chưa tính nhãn thừa. |

Hai ZIP mở được, đều có XML phiên bản 1.1 và chỉ chứa `annotations.xml`. Lint toàn lô báo 9 cảnh báo thiếu L1/R1. Chỉ các lỗi đã đối chiếu trên mẫu 6 ảnh được đưa vào quyết định dưới đây.

## Quyết định

**Lỗi nặng đã xác nhận** — 0  
**Lỗi chính** — 14 / 77 nhãn = **18,18%**  
**Lỗi nhẹ** — 0  
**Ca chờ lead** — 3  
**Quyết định** — **Rework**

Tỉ lệ lỗi chính vượt ngưỡng 5%. Ưu tiên sửa polygon `direct` tự cắt ở A08, rà lại các box đèn A08 và B02, rồi kiểm lại các điểm dừng của vạch và biên vùng lái.

[Thang mức lỗi QC 1](docs/qc_severity_road_v1.0.md)
