# Ứng Dụng Thuật Toán Học Máy Trong Phân Loại Email Spam và Tin Nhắn Lừa Đảo

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Scikit-Learn](https://img.shields.io/badge/Library-Scikit--Learn-orange)
![Status](https://img.shields.io/badge/Status-Completed-success)

> **Môn học:** Chuyên đề 2  
> **Giảng viên hướng dẫn:** TS. Nguyễn Văn Hiếu  
> **Đơn vị:** Khoa Điện tử Viễn thông - Trường Đại học Bách Khoa, Đại học Đà Nẵng 

## 1. Giới thiệu Dự án

Trước sự bùng nổ của công nghệ, email và tin nhắn điện tử đã trở thành phương tiện giao tiếp chính yếu, nhưng cũng kéo theo rủi ro lớn về an ninh mạng, đặc biệt là **Phishing Email** (Email lừa đảo). Kẻ tấn công thường mạo danh các tổ chức uy tín để đánh cắp thông tin nhạy cảm của người dùng.

Dự án này xây dựng một hệ thống phát hiện tự động sử dụng các thuật toán **Học máy (Machine Learning)** để phân loại email/tin nhắn thành hai lớp:
* **Hợp lệ (Legit)**: Email an toàn, công việc bình thường.
* **Lừa đảo/Spam (Phishing)**: Email chứa mã độc, liên kết giả mạo hoặc nội dung lừa đảo.

## 2. Thành viên Thực hiện (Nhóm 16)

| STT | Họ và tên | Mã sinh viên | Vai trò và Đóng góp |
|:---:|-----------|:---:|---|
| 1 | **Nguyễn Văn Chí** | 106210207 | - Viết phần mở đầu, đặt vấn đề.<br>- Phân tích kỹ thuật Phishing.<br>- Xây dựng bộ đặc trưng dữ liệu (Feature Engineering).<br>- Triển khai thuật toán **KNN**.  |
| 2 | **Lê Quang Hùng** | 106210238 | - Mô hình hóa toán học (Hàm mất mát, tối ưu).<br>- Triển khai và viết lý thuyết thuật toán **Decision Tree, Random Forest**.<br>- Phân tích độ phức tạp thuật toán.  |
| 3 | **Trần Thanh Tín** | 106210253 | - Triển khai thuật toán **Naive Bayes, Logistic Regression**.<br>- Phân tích kết quả, tính toán chỉ số (Precision, Recall, F1).<br>- Tổng hợp báo cáo.  |

## 3. Bộ Dữ liệu (Dataset)

Dữ liệu được tổng hợp từ hai nguồn uy tín với tổng cộng **9804 mẫu**:

* **Email Lừa đảo (Phishing/Spam):** 2604 mẫu (Nguồn: *monkey.org*).
* **Email Hợp lệ (Legit):** 7200 mẫu (Nguồn: *Enron dataset*).

**Phân chia dữ liệu:**
* **Tập Huấn luyện (Training):** 7843 mẫu (~80%).
* **Tập Kiểm thử (Testing):** 1961 mẫu (~20%).

## 4. Trích chọn Đặc trưng (Feature Engineering)

Hệ thống không chỉ dựa vào văn bản thuần túy mà trích xuất các đặc trưng kỹ thuật để phát hiện lừa đảo. Các đặc trưng chính bao gồm:

### 4.1. Cấu trúc và Nội dung 
* `HTML_Content`: Email có chứa mã HTML hay không.
* `bodyImg`: Có chứa thẻ `<img>` (thường dùng để che giấu văn bản).
* **Từ khóa nhạy cảm:** Phát hiện các từ như `bank`, `verify`, `account`, `password` trong tiêu đề hoặc nội dung.

### 4.2. Đặc trưng URL & Liên kết 
* `NumURL`, `NumIP`: Số lượng URL, URL dùng IP thay tên miền.
* `HaveAt (@)`: Dấu hiệu che giấu tên miền thật.
* `Redirection (//)`: Dấu hiệu chuyển hướng trang web.
* `tinyURL`: Sử dụng dịch vụ rút gọn link để che giấu đích đến.
* `Prefix-Suffix (-)`: Giả mạo tên miền (ví dụ: *pay-pal.com*).

### 4.3. Kỹ thuật Che giấu & Mã độc 
* `NumScript`: Số lượng thẻ `<script>`.
* `OnMouseOver`, `RightClick`: Các sự kiện Javascript dùng để đánh lừa người dùng hoặc chặn kiểm tra mã nguồn.

## 5. Các Mô hình và Kết quả

Dự án đã triển khai và so sánh 5 thuật toán phổ biến: **Logistic Regression (LR), Naive Bayes (NB), Decision Tree (DT), Random Forest (RF), và K-Nearest Neighbors (KNN)**.

**Bảng so sánh hiệu năng trên tập Test (1961 mẫu):**

| Model | Accuracy | Precision | Recall | F1-Score | False Positive Rate (FPR) |
|-------|----------|-----------|--------|----------|---------------------------|
| **Logistic Regression** | **0.9939** | **1.0000** | 0.9760 | **0.9879** | **0.0000** |
| **Random Forest** | **0.9939** | **1.0000** | 0.9760 | **0.9879** | **0.0000** |
| Decision Tree | 0.9929 | 0.9959 | 0.9760 | 0.9859 | 0.0014 |
| Naive Bayes | 0.9786 | 0.9370 | **0.9820** | 0.9590 | 0.0226 |
| KNN | 0.9796 | 0.9600 | 0.9600 | 0.9600 | 0.0137 |

*[Số liệu chi tiết xem tại Bảng 6 của báo cáo]* 

### Nhận xét & Kết luận:

1.  **Độ an toàn tuyệt đối:** Hai mô hình **Logistic Regression** và **Random Forest** đạt **Precision = 1.0** và **FPR = 0.0**. Điều này có nghĩa là trên tập kiểm thử, **không có email hợp lệ nào bị đánh dấu nhầm là Spam**. Đây là tiêu chuẩn quan trọng nhất cho hệ thống lọc thư.
2.  **Khả năng phát hiện:** **Naive Bayes** có Recall cao nhất (98.2%), tức là phát hiện được nhiều spam nhất, nhưng lại hay báo nhầm (FPR cao nhất 2.26%).
3.  **Khuyến nghị:** Nhóm đề xuất sử dụng **Logistic Regression** cho bài toán thực tế. Mặc dù hiệu năng ngang bằng Random Forest, nhưng LR có tốc độ dự đoán nhanh hơn ($O(d)$ so với $O(M \cdot d)$) và chi phí tính toán thấp hơn, phù hợp cho hệ thống xử lý thời gian thực.

---
*Đà Nẵng, Tháng 12 năm 2025* 
