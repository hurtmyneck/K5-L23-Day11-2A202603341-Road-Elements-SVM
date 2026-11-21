# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Bùi Thanh Tân - 2A202603304
Người kiểm (học viên): Dương Trí Dũng - 2A202603341  
Ngày: 2026-11-20 
Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `job_17_annotations_2026_11_20_10_59_43_cvat for images 1.1.zip` (task front, job 17; chưa có manifest nên chưa có revision) 
Số ảnh kiểm: 6 (A01–A06)
Số nhãn đã kiểm(shape + tag): 61  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 12 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 17 | 2 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 17 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 17 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 17 | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 17 | 2 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 0 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 0 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 0 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 0 | 0 | chính |
| QC1-12 file | lỗi file | 1 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-03 | A02 | lane, vạch đứt bên trái (bắt đầu ~(0,589)) | nặng | position = L1 trùng với vạch đứt giữa đường cũng là L1; vạch này nằm ngoài vạch giữa nên phải là L2. |
| 2 | QC1-03 | A02 | lane, vạch trắng liền mép phải (bắt đầu ~(1154,720)) | nặng | position = R2 nhưng đây là vạch phải sát nhất, đúng ra là R1; ảnh hiện không có R1 (lint cũng báo thiếu R1). |
| 3 | QC1-06 | A03 | lane L1, vạch vàng bên trái (bắt đầu ~(224,699)) | chính | kind = single nhưng là vạch vàng đôi; sửa thành double. |
| 4 | QC1-07 | A02 | drivable alternative, polygon bên phải (bắt đầu ~(1169,720)) | chính | Polygon tràn ra ngoài vạch mép phải, gồm cả phần lề đường nhựa; guideline không tính lề vào vùng lái. |
| 5 | QC1-07 | A04 | drivable direct, polygon bên trái (bắt đầu ~(2,430)) | chính | Vùng lái direct ở phía bên kia vạch vàng đôi (làn ngược chiều); direct chỉ là làn đang đi. |

## Ca mơ hồ
| Ảnh           | Câu hỏi cho lead                                                                                                                                         | Lời đáp (nếu có) |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| A05, A06      | `lint` báo QC1-02 chưa có L1/R1 (A05 cả hai, A06 thiếu R1). Trong ảnh không thấy vạch kẻ làn sát xe (A05 đường không vạch; A06 gầm cầu). Coach có xác nhận miễn QC1-02 không? | hỏi lab coach    |
| A06           | Ảnh A06 có nhiều đèn giao thông và biển nhìn rõ nhưng chưa có hộp traffic_light / traffic_sign nào. Ảnh này có yêu cầu gán đèn, biển không (kế hoạch ảnh)? Nếu có thì bỏ sót QC1-08 và QC1-10 (chính). | hỏi lab coach    |
| A03           | Vùng sơn vằn giữa L1 và L2 (và polygon alternative phủ lên nó), cùng các nhãn bên kia dải phân cách ở góc trái (lane position = other và hai polygon alternative): có phải làn cùng chiều không? Nếu không thì thừa, tính QC1-03 / QC1-07. | hỏi lab coach    |
| A04           | Vạch L2 (trắng, ngoài cùng bên trái), road_curb bên trái: thuộc làn ngược chiều. Có nên gán không? | hỏi lab coach    |
| A03, A04, A05, A06 | Tag weather = clear nhưng trời nhiều mây, overcast có đúng hơn không? (A03 timeofday = day, trời hoàng hôn, dusk có đúng hơn không?) | hỏi lab coach    |

## Quyết định
Lỗi nặng: 2   Lỗi chính: 3 / 61 nhãn = 4,9 %   Lỗi nhẹ: 0   
Ca chờ lead: 5  
Quyết định (Release / Hold / Rework): Rework  
Lý do (theo luật của phiếu): Còn lỗi nặng (sai position hai vạch ở A02) nên Rework. Lỗi chính 4,9 % sát ngưỡng 5 %; nếu các ca mơ hồ ở A03, A04, A06 bị tính là lỗi thì vượt ngưỡng. Các ca chờ lead không đổi kết luận vì đã có lỗi nặng.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
