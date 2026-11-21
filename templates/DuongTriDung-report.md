# Báo cáo cá nhân — Ngày 11
Họ tên: Dương Trí Dũng
Mã học viên: 2A202603341
Phiên bản CVAT (Help → About):  2.74.1
Guideline: Road v1.0   
Lần nộp (`revision` trong manifest):  
Thời điểm export (ngày giờ trên CVAT): 21/11/2026
Số lần nộp lại sau Rework: 0

## 1. Kiểm project
| Mục                   | Đúng như guideline Road v1.0? | Ghi chú |
| --------------------- | ----------------------------- | ------- |
| 6 label, đúng kiểu    | đúng như guideline            |         |
| Thuộc tính và giá trị | đúng như guideline            |         |
| 4 tag ảnh             | đúng như guideline            |         |
Cách kết thúc polyline trên bản CVAT này:  Khi vẽ xong bấm "N"
Cách đặt tag ảnh trên bản CVAT này: chọn "tag" ở góc trái màn hình

## 2. Số lượng đã gán
| Task                          | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| ----------------------------- | --: | ---: | --------: | --------: | -------: | ------------: | -----------: |
| front                         |  12 |   29 |         3 |         4 |       24 |            22 |            8 |
| front-extra (đã làm __ / 4)   |   4 |    8 |         2 |         2 |        9 |            12 |            9 |
| fisheye                       |   8 |    9 |         9 |         7 |        6 |             0 |            0 |
| fisheye-extra (đã làm __ / 4) |   4 |    0 |         1 |         4 |        4 |             0 |            0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | ---- | ------------- | ------- | ----- |
|     |      |               |         |       |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Bùi Thanh Tân
Quyết định nhận được:  

| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| ------ | -----: | ------- | ------- |
|        |        |         |         |

## 5. Kiểm file export
| File          | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML?                 |
| ------------- | ------------ | --------------------------- | --------------------------- | ---------------------------------------- |
| front         | có           | A01: 46 / 7                 | A02: 46 / 7                 | có (camera = front)                      |
| front-extra   | có           | A13: 47 / 5                 | A14: 47/ 10                 | có (camera = front)                      |
| fisheye       | có           | B01: 48 / 3                 | B02: 48 / 4                 | có (fisheye_front)                       |
| fisheye-extra | có           | B09: 49 / 4                 | B10: 49 / 2                 | có (B09 fisheye_front, B10 fisheye_left) |

## 6. Ảnh chụp màn hình
1. Tab Labels của project.
		![[anh1.png]]
		
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển).
		![[anh2.png]]
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong.
		![[anh3.png]]
4. Một đoạn XML có polyline label="lane".
	"<polyline label="lane" source="manual" occluded="0" points="110.31,720.00;299.38,556.67;336.81,526.13;360.59,509.32" z_order="0">
    <attribute name="position">L1</attribute>
    <attribute name="style">dashed</attribute>
    <attribute name="color">white</attribute>
    <attribute name="kind">single</attribute>
    </polyline>"

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  Lỗi mắc nhiều nhất: QC1-04. Cách tránh: vẽ từ gần ra xa
Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:  Nhãn đi vào model ở bước training. Lỗi sẽ khiến model bị học theo data sai, dẫn đến dự đoán sai.
## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi |  |  |  |  |  |
| x của bạn kia |  |  |  |  |  |

Trả lời 3 câu:

1. Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?
2. So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?
3. Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?
