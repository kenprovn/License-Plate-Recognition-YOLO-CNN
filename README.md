Form README
Tên github - Tên
1.Nhiệm vụ được giao
2.Cách tiếp cận nhiệm vụ & thuật toán (nếu có, trình bày logic xử lý là được)
3.Quy trình thực hiện (Các bước làm cụ thể)
4.Kết quả đạt được
5.Khó khăn gặp phải
Dựa vào form như này để viết nếu có thể chi tiết hơn thì có thể viết thêm nhưng cứ theo như này là được

Tên github: kenprovn - Minh Khanh
1 Nhiệm vụ được giao:
"1. Lấy ảnh biển số xe (chỉ biển số)
2. TIỀN XỬ LÝ ẢNH BIỂN SỐ (Chữ nổi rõ, Nền ít nhiễu, Dễ cắt ký tự
	2.1.Đọc ảnh
	2.2.Chuyển ảnh xám để dễ xử lý
	2.3.Khử nhiễu
	2.4.Nhị phân hóa (tức là đưa ảnh về chữ trắng nền đen)
3. CẮT KÝ TỰ
	3.1. Tìm vùng bao quanh vật thể (chữ, ốc, vết bẩn)
	3.2. Lọc vùng bao quanh vật thể bị sai
	3.3. Sắp xếp ký tự từ trái sang phải
	3.4. Cắt ký tự
4. Làm sạch ảnh
5. Gán nhãn
6. AUGMENTATION: Xoay, làm mờ, Nhiễu và thay đổi ánh sáng 1 vài ảnh để mô hình học (lưu ý chỉ thay đổi 1 vài ảnh khoảng 2-3% ảnh)
7. Kiểm tra dataset: Kiểm tra xem có gán nhầm ký tự ko (ví dụ nhầm B thành 8 nhầm 0 thành o,…)
Cuối cùng giao 1 folder chứa class nhãn, mỗi class sẽ chứa nhiều ảnh, ảnh sạch cùng size
Nhớ không cắt tay, không để ảnh bẩn, không gán nhãn sai"

2 Cách tiếp cận nhiệm vụ và Thuật toán
Phương pháp tiếp cận tập trung vào việc tự động hóa quy trình xử lý ảnh thông qua thư viện thị giác máy tính OpenCV thay vì thực hiện thủ công. Để giải quyết vấn đề ảnh đầu vào có chất lượng không đồng đều, thuật toán CLAHE (Contrast Limited Adaptive Histogram Equalization) được áp dụng nhằm cân bằng ánh sáng cục bộ, giúp ký tự nổi bật ngay cả trong điều kiện bóng râm hoặc chói sáng. Đối với việc tách ký tự khỏi nền, phương pháp Nhị phân hóa thích ứng (Adaptive Thresholding) được sử dụng để xử lý tốt hơn so với ngưỡng cố định.
Quy trình xác định vị trí ký tự dựa trên thuật toán tìm đường viền (Find Contours). Để phân biệt giữa ký tự và các vật thể nhiễu như đinh ốc hay vết bẩn, một bộ lọc Heuristic được xây dựng dựa trên tỷ lệ kích thước (Aspect Ratio) và diện tích vùng bao. Việc gán nhãn được hỗ trợ bởi thư viện EasyOCR để tự động phân loại sơ bộ, sau đó kết hợp với kiểm tra thủ công để đảm bảo độ chính xác tuyệt đối.

3. Quy trình thực hiện
Quá trình xử lý bắt đầu bằng việc tiếp nhận ảnh biển số xe đã được cắt sẵn. Tại giai đoạn tiền xử lý, ảnh được chuyển đổi sang hệ màu xám để giảm tải tính toán, sau đó đi qua bộ lọc Gaussian Blur để làm mịn và loại bỏ nhiễu hạt. Tiếp theo, ảnh được áp dụng thuật toán CLAHE để cân bằng sáng và đưa về dạng nhị phân (chữ trắng nền đen) thông qua Adaptive Threshold.
Giai đoạn quan trọng nhất là phân đoạn ký tự, hệ thống quét toàn bộ các đường viền trong ảnh nhị phân để xác định các vùng ứng viên. Các vùng này được lọc qua bộ lọc kích thước để loại bỏ các chi tiết thừa như ốc vít hoặc viền xe. Những vùng được xác định là ký tự sẽ được sắp xếp thứ tự từ trái sang phải, cắt rời khỏi ảnh gốc và chuẩn hóa về kích thước cố định 64x128 pixel để đảm bảo tính đồng nhất.
Sau khi cắt, các ảnh ký tự được phân loại vào các thư mục nhãn tương ứng (Folder-based Labeling). Để nâng cao khả năng học của mô hình, một lượng nhỏ dữ liệu (khoảng 3%) được chọn ngẫu nhiên để thực hiện Augmentation gồm các thao tác xoay nghiêng, làm mờ và thêm nhiễu. Cuối cùng, toàn bộ tập dữ liệu trải qua bước kiểm tra chất lượng nghiêm ngặt để loại bỏ các ảnh mờ nhòe hoặc gán nhãn sai trước khi bàn giao.

4. Kết quả đạt được
Dự án đã xây dựng thành công bộ dữ liệu ký tự biển số xe sạch và được chuẩn hóa đồng bộ. Toàn bộ ảnh đầu ra có kích thước 64x128 pixel, rõ nét, không lẫn tạp chất và được phân loại chính xác vào các thư mục nhãn (0-9, A-Z). Cấu trúc thư mục được tổ chức khoa học, thuận tiện cho việc tích hợp trực tiếp vào các quy trình huấn luyện mạng CNN mà không cần xử lý thêm.

5. Khó khăn gặp phải
Thách thức lớn nhất trong quá trình thực hiện nằm ở việc xử lý các ảnh biển số có điều kiện ánh sáng phức tạp hoặc bị mờ nhòe do chuyển động, khiến thuật toán khó tách biệt hoàn toàn ký tự khỏi nền. Bên cạnh đó, việc phân biệt giữa các ký tự có hình dáng tương đồng (như số 8 và chữ B, số 0 và chữ D) hoặc loại bỏ các đinh ốc có kích thước gần bằng ký tự cũng đòi hỏi phải tinh chỉnh tham số bộ lọc nhiều lần để đạt độ chính xác tối ưu.
