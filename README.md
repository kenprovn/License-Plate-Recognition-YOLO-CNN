Form README
Tên github - Tên
1.Nhiệm vụ được giao
2.Cách tiếp cận nhiệm vụ & thuật toán (nếu có, trình bày logic xử lý là được)
3.Quy trình thực hiện (Các bước làm cụ thể)
4.Kết quả đạt được
5.Khó khăn gặp phải
Dựa vào form như này để viết nếu có thể chi tiết hơn thì có thể viết thêm nhưng cứ theo như này là được

Tên GitHub: kenprovn - Minh Khanh.

1 Nhiệm vụ được giao: Thực hiện lấy ảnh biển số xe từ đầu ra của mô hình YOLO để tiến hành quy trình tiền xử lý ảnh nhằm làm cho chữ nổi rõ, nền ít nhiễu và hỗ trợ việc cắt ký tự diễn ra thuận lợi thông qua các bước đọc ảnh, chuyển sang ảnh xám, khử nhiễu và nhị phân hóa để đưa về dạng chữ trắng nền đen. Tiếp theo là công đoạn cắt ký tự bằng cách tìm vùng bao quanh vật thể như chữ, số và loại bỏ các thành phần nhiễu như đinh ốc hay vết bẩn, sau đó sắp xếp ký tự từ trái sang phải để tiến hành cắt rời, làm sạch ảnh và chuẩn hóa kích thước chuẩn đồng bộ. Cuối cùng thực hiện gán nhãn tự động kết hợp tăng cường dữ liệu bằng các phép xoay, làm mờ, thêm nhiễu và thay đổi ánh sáng trên khoảng 2-3% số lượng ảnh để mô hình học tập tốt hơn, đồng thời kiểm tra kỹ lưỡng toàn bộ dataset để tránh sai sót nhãn như nhầm giữa B và 8 hay 0 và O nhằm bàn giao một thư mục chứa các lớp nhãn sạch với kích thước ảnh đồng nhất mà không sử dụng phương pháp cắt tay thủ công.

2 Cách tiếp cận nhiệm vụ và Thuật toán: Phương pháp tiếp cận tập trung hoàn toàn vào việc tự động hóa quy trình thông qua thư viện OpenCV để đảm bảo tính khách quan và hiệu suất cao. Thuật toán CLAHE được áp dụng để cân bằng ánh sáng cục bộ giúp ký tự nổi bật trong mọi điều kiện môi trường, kết hợp với phương pháp nhị phân hóa thích ứng Adaptive Thresholding để xử lý tốt hơn các vùng chói hoặc tối cục bộ. Quy trình xác định vị trí ký tự dựa trên thuật toán tìm đường viền Find Contours phối hợp với bộ lọc Heuristic dựa trên tỷ lệ khung hình Aspect Ratio và diện tích để lọc nhiễu chính xác. Đặc biệt, để giải quyết vấn đề biến dạng ký tự, kỹ thuật Padding thêm viền đen đã được sử dụng thay vì resize trực tiếp, giúp đưa ảnh về khung vuông 64x64 mà vẫn giữ trọn vẹn tỷ lệ hình học thực tế của con chữ, kết hợp cùng EasyOCR để hỗ trợ phân loại sơ bộ trước khi rà soát thủ công.

3 Quy trình thực hiện: Quá trình bắt đầu từ việc tiếp nhận ảnh biển số, sau đó chuyển sang hệ màu xám và khử nhiễu bằng bộ lọc Gaussian Blur trước khi tăng cường độ tương phản bằng CLAHE và nhị phân hóa ảnh. Giai đoạn quan trọng nhất là quét toàn bộ các đường viền để xác định vùng ứng viên, thực hiện lọc bỏ chi tiết thừa như ốc vít rồi sắp xếp thứ tự và cắt rời ký tự. Sau khi cắt, toàn bộ ảnh được áp dụng kỹ thuật Padding để đưa về kích thước cố định 64x64 pixel nhằm đảm bảo tính đồng nhất mà không làm méo hình. Các ký tự sau đó được phân loại vào thư mục nhãn tương ứng và chọn lọc 3% ngẫu nhiên để thực hiện Augmentation bao gồm các thao tác xoay nghiêng có kết hợp thu nhỏ Scale để không bị mất góc ảnh, thêm mờ và nhiễu, cuối cùng là bước kiểm soát chất lượng nghiêm ngặt để loại bỏ hoàn toàn các ảnh lỗi trước khi xuất bản dataset.

4 Kết quả đạt được: Dự án đã xây dựng thành công bộ dữ liệu ký tự biển số xe sạch với toàn bộ ảnh đầu ra có kích thước 64x64 pixel rõ nét và giữ đúng tỷ lệ thực tế, không bị mập hay bóp méo hình học. Dữ liệu được phân loại chính xác tuyệt đối vào các thư mục nhãn từ 0-9 và A-Z với cấu trúc khoa học, sẵn sàng để tích hợp trực tiếp vào quy trình huấn luyện mạng CNN mà không cần bất kỳ bước xử lý trung gian nào khác.

5 Khó khăn gặp phải: Thách thức lớn nhất nằm ở việc xử lý các ảnh biển số có ánh sáng phức tạp hoặc mờ nhòe do chuyển động làm thuật toán khó tách biệt ký tự, cũng như việc phân biệt các cặp ký tự dễ nhầm lẫn như 8 với B hay 0 với D đòi hỏi phải tinh chỉnh tham số bộ lọc nhiều lần. Tuy nhiên, việc áp dụng kỹ thuật Padding và Scale khi xoay đã giải quyết triệt để các vấn đề về biến dạng và mất thông tin góc ảnh gặp phải trong giai đoạn đầu của dự án.
