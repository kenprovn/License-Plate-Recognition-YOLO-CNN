Form README
Tên github - Tên
1.Nhiệm vụ được giao
2.Cách tiếp cận nhiệm vụ & thuật toán (nếu có, trình bày logic xử lý là được)
3.Quy trình thực hiện (Các bước làm cụ thể)
4.Kết quả đạt được
5.Khó khăn gặp phải
Dựa vào form như này để viết nếu có thể chi tiết hơn thì có thể viết thêm nhưng cứ theo như này là được

BÁO CÁO QUY TRÌNH XÂY DỰNG DATASET KÝ TỰ (Thành viên 2: Minh Khanh)
QUY TRÌNH THỰC HIỆN
Tôi đã thực hiện xử lý dữ liệu qua 4 bước chính:

Bước 1: Tiền xử lý ảnh (Pre-processing)
Để làm nổi bật ký tự và loại bỏ các yếu tố gây nhiễu từ môi trường (ánh sáng, bóng râm), tôi áp dụng các kỹ thuật xử lý ảnh cơ bản:

Chuyển xám (Grayscale): Đưa ảnh về dạng đơn sắc.

Khử nhiễu (Gaussian Blur): Làm mịn ảnh để loại bỏ nhiễu hạt (noise).

Nhị phân hóa (Adaptive Threshold): Tách ký tự (màu đen) ra khỏi nền (màu trắng) dựa trên độ tương phản cục bộ.

Bước 2: Cắt tách ký tự (Segmentation)
Sử dụng thuật toán tìm đường viền (Contours) trong OpenCV để xác định vị trí các ký tự:

Tìm vùng bao: Xác định khung hình chữ nhật bao quanh vật thể.

Lọc nhiễu: Loại bỏ các vùng không phải ký tự (vết bẩn, đinh ốc, viền xe) dựa trên tỷ lệ chiều cao và diện tích.

Cắt ảnh: Cắt từng ký tự và lưu thành từng file ảnh riêng biệt.

Bước 3: Làm sạch và Chọn lọc thủ công (Manual Cleaning)
Đây là bước tốn nhiều thời gian nhất để đảm bảo chất lượng dữ liệu:

Lọc rác: Kiểm tra từng thư mục, xóa bỏ các hình ảnh mờ, nhòe, hoặc cắt sai.

Sửa lỗi: Di chuyển các ký tự bị nhận diện nhầm về đúng lớp (Ví dụ: nhầm lẫn giữa số 8 và chữ B).

Cân bằng dữ liệu: Tuyển chọn thủ công 400 ảnh rõ nét nhất cho mỗi lớp ký tự để đảm bảo bộ dữ liệu đồng đều.

Bước 4: Tăng cường dữ liệu (Data Augmentation)
Để mô hình học tốt hơn trong thực tế, tôi đã tạo thêm dữ liệu mới (khoảng 3%) bằng cách:

Xoay ảnh nhẹ (Rotation).

Thêm nhiễu hạt (Noise).

Thay đổi độ sáng (Brightness).
