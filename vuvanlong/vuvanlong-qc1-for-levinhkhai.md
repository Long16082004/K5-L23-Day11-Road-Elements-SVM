# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): levinhkhai (MSSV 2A202603322)        Người kiểm (học viên): vuvanlong (MSSV 2A202603312)  
Ngày: 2026-11-20                         Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `levinhkhai-front.zip` (chưa nhận manifest, nên chưa biết revision)  
Số ảnh kiểm: 6 (A01–A06) (+ 0 ảnh thêm)   Số nhãn đã kiểm (shape + tag): 108 (84 shape + 24 tag)

Cách kiểm: không có GT, nên mình đối chiếu từng nhãn với ảnh gốc bằng ảnh phủ nhãn tự dựng từ `annotations.xml`, và dùng thêm `road_check lint`. Các lỗi dưới đây là phán đoán bằng mắt, chưa đối chiếu GT.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 12 | 1 (+1 chờ lead) | nặng |
| QC1-03 position | sai thuộc tính / thừa | 18 | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 18 | 4 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 18 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 18 | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 12 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 15 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 22 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 22 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 0 | 0 | chính |
| QC1-12 file | lỗi file | 1 | 0 | nhẹ / nặng |

Cả 6 ảnh đủ bốn tag (camera = front, timeofday, weather, source). File mở được, không có label lạ.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-03 | A03 | lane, position L2 (solid, yellow) | nặng | Polyline nằm trên các vệt vàng ngắn của dải đảo/vỉa bên trái, không phải vạch kẻ làn. Thừa nhãn. Cần coach/GT xác nhận. |
| 2 | QC1-02 | A06 | thiếu R1 | nặng | Lint cũng báo thiếu R1. Có vạch trắng đứt ở góc phải dưới ảnh mà không được vẽ. Nếu GT coi là R1 thì lỗi nặng. Xem mục ca mơ hồ. |
| 3 | QC1-06 | A03 | lane L1 (solid, white, single) | chính | Vạch sát xe bên trái là vạch vàng đôi nhìn thấy rõ, nhãn ghi white/single. Sai color và kind. |
| 4 | QC1-04 | A02 | lane L1 (dashed, white) | chính | Polyline bắt đầu ở y≈502 trong khi vạch đứt còn thấy tới sát xe ở dưới. Thiếu đoạn gần xe. |
| 5 | QC1-04 | A02 | lane L2 (dashed, white) | chính | Bắt đầu ở x≈252, vạch còn thấy kéo ra mép trái ảnh. Thiếu đoạn gần. |
| 6 | QC1-04 | A04 | lane R2 (#11) | chính | Vẽ từ xa về gần (lint báo điểm đầu cao hơn điểm cuối). |
| 7 | QC1-04 | A04 | lane R2 (#12) | chính | Như trên: sai chiều vẽ. |

Lỗi nhẹ: A03 có 3 hộp (1 biển, 2 đèn) thấp hơn 8 px. Lint chỉ gợi ý, không tính vào tỉ lệ.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Không thấy vạch kẻ nào (đường hai chiều hẹp, hai bên xe đỗ). Thiếu L1/R1 có được miễn không? | |
| A06 | Vạch trắng đứt ở góc phải dưới có phải R1 không, hay là vạch của dải khác? Nếu là R1 thì lỗi #2 thành nặng chắc chắn. | |
| A06 | Hộp đèn góc trái trên đang là `unknown` nhưng bóng sáng màu cam/đỏ nhìn thấy được. Có phải sai màu trên đèn hướng về xe? | |
| A04 | Hai polyline R2 chạy hai mép làn xe đạp (xanh). Một trong hai nên là `other` hay cả hai là một vạch? | |
| A01 | L2 ghi white/double, nhưng vạch sát dải phân cách bên trái trông là màu vàng. Sai color? | |
| A01, A03, A04 | Vùng `alternative` có gồm làn khẩn cấp, làn xe đạp hay dải đỗ xe không? Guideline không nói rõ. | |
| A03 | R1 chỉ vẽ ngắn ở xa, còn vạch đứt còn thấy kéo về gần xe? R2 ghi dashed white chạy sát hàng xe đỗ có phải vạch làn không? | |
| A05 | `drivable direct` phủ cả hai chiều đường vì không có vạch tim. Chỉ nửa đường cùng chiều thì đúng hơn? | |

## Quyết định
Lỗi nặng: 2 (1 chắc, 1 chờ lead)   Lỗi chính: 5 / 108 nhãn = 4,6 %   Lỗi nhẹ: 3   Ca chờ lead: 8  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Có ít nhất một lỗi nặng (lỗi #1: vẽ thừa vạch ở A03; lỗi #2 chờ xác nhận) nên Rework theo luật "có lỗi nặng → Rework". Lỗi chính là 4,6 %, dưới ngưỡng 5 %, nhưng ca mơ hồ nhiều (chủ yếu A04, A06) có thể đẩy tỉ lệ này vượt 5 %. Mình ưu tiên Rework hơn Hold vì lỗi #1 độc lập với các câu hỏi chờ.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
