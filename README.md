# Dự án Phân Tích Dữ Liệu Sức Khỏe

## Tổng Quan

Hiện nay, các phong trào tập thể dục thể thao đang ngày càng phát triển, thu hút nhiều nhóm tuổi và giới tính. Dữ liệu `bodyPerformance.csv` chứa thông tin của **13,393 người** tập luyện thể thao tại Hàn Quốc, với **12 biến**:

- `age`: độ tuổi (20–64)
- `gender`: giới tính (`F` – nữ, `M` – nam)
- `height_cm`: chiều cao (cm)
- `weight_kg`: cân nặng (kg)
- `body fat_%`: tỷ lệ mỡ cơ thể (%)
- `diastolic`: huyết áp tâm trương
- `systolic`: huyết áp tâm thu
- `gripForce`: lực kẹp
- `sit and bend forward_cm`: khả năng gập người
- `sit-ups counts`: số lần gập bụng
- `broad jump_cm`: nhảy xa
- `class`: phân lớp hiệu suất (`A` tốt nhất → `D` kém nhất)

**Mục tiêu:** Phân tích các yếu tố ảnh hưởng đến hiệu suất thể thao và xây dựng mô hình dự đoán phân lớp hiệu suất (`class`).

---

## Quy Trình Phân Tích
+----------------------------+
| Đọc và tiền xử lý dữ liệu|
+------------+--------------+
|
v
+----------------------------+
| Phân tích thống kê mô tả |
+------------+--------------+
|
v
+----------------------------+
| Kiểm định ANOVA |
| (so sánh giữa các nhóm) |
+------------+--------------+
|
v
+----------------------------+
| Xây dựng mô hình ML |
| Logistic, LDA, QDA, RF |
+------------+--------------+
|
v
+----------------------------+
| Đánh giá & Kết luận |
+----------------------------+


---

## Các Bước Chi Tiết

### 1. Đề Xuất Phân Tích

- Làm sạch và xử lý dữ liệu.
- Chuẩn hóa tên biến.
- Kiểm tra missing values và phân phối biến.

### 2. Mục Tiêu Phân Tích

- Dự đoán hiệu suất thể thao (`class`).
- Tìm ra các biến ảnh hưởng đến hiệu suất.
- So sánh hiệu suất giữa các nhóm qua ANOVA test.

### 3. Phương Pháp & Chiến Lược

- **Kiểm định ANOVA**: xác định biến định lượng nào khác biệt giữa các lớp.
- **Mô hình phân loại:**
  - Multinomial Logistic Regression
  - LDA (Linear Discriminant Analysis)
  - QDA (Quadratic Discriminant Analysis)
  - Random Forest

---

## Phân Tích ANOVA

- So sánh trung bình các biến như `sit-ups`, `broad_jump_cm`, `body_fat_%`,... giữa các lớp hiệu suất (`A`, `B`, `C`, `D`).
- Phát hiện các biến có sự khác biệt rõ rệt giữa nhóm.

---

## Mô Hình Học Máy

**Biến mục tiêu:** `class`  
**Biến đầu vào:** 11 biến còn lại

### Mô hình huấn luyện:
- `train_test_split`
- Huấn luyện trên tập train, kiểm tra trên tập test
- Đánh giá bằng độ chính xác (accuracy), confusion matrix

### Các mô hình:
| Mô Hình                 | Đặc Điểm                                                         |
|------------------------|------------------------------------------------------------------|
| Multinomial Logistic   | Mô hình tuyến tính, dễ giải thích                                 |
| LDA                    | Phân phối chuẩn, giả định phương sai bằng nhau                   |
| QDA                    | Không giả định phương sai bằng nhau                              |
| Random Forest       | Xử lý tốt biến định tính + định lượng, chống overfitting mạnh   |

---

## Kết Luận

- Các biến **diastolic**, **systolic**, **height_cm**, **body_fat_%**, **gender** → không ảnh hưởng rõ rệt → có thể loại bỏ.
- Biến **sit_ups_counts**, **broad_jump_cm**, **age** → ảnh hưởng mạnh nhất.

### Random Forest là mô hình hiệu quả nhất:
- Hoạt động tốt với nhiều loại biến.
- Chống overfitting tốt.
- Không yêu cầu phân phối chuẩn hay độc lập giữa các biến.

### Khuyến nghị:
- Biến `age` là không thay đổi được → tập trung cải thiện:
  - **sit_ups_counts** → tập gập bụng, plank, tăng dần cường độ.
  - **broad_jump_cm** → tập squat jump, box jump, plyometric.

> Nên theo dõi tiến độ và điều chỉnh chế độ luyện tập + nghỉ ngơi phù hợp để tối ưu hiệu quả.






