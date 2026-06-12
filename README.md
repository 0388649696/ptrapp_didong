# BÁO CÁO BÀI TẬP LỚN
**MÔN HỌC**: PHÁT TRIỂN ỨNG DỤNG TRÊN THIẾT BỊ DI ĐỘNG (TEE0419) **Họ và tên SV**: Nguyễn Đức Anh Tú **MSSV**: K225480106070

# BÀI TẬP 1: PHÁT TRIỂN ỨNG DỤNG TRÊN NỀN TẢNG TRỰC QUAN MIT APP INVENTOR

Thiết kế ứng dụng đa màn hình: Xây dựng hệ thống ứng dụng gồm 3 màn hình logic liên kết chặt chẽ với nhau, cấu hình nút bấm điều hướng mượt mà, không xảy ra xung đột luồng khi chuyển màn hình.

Xây dựng chức năng giải toán/quy đổi: Triển khai màn hình chức năng cho phép người dùng nhập liệu, sử dụng các khối logic toán học để tính toán quy đổi tiền tệ từ VND sang các đồng ngoại tệ (USD, CNY, EUR, USDT).

Tích hợp giao diện hiển thị web: Nhúng trực tiếp thành phần trình duyệt WebViewer vào app để truy cập thẳng vào đường link theo dõi biến động tỷ giá trực tuyến thời gian thực mà không cần thoát ứng dụng.

**BÀI LÀM**

**Đề tài:** Xây dựng ứng dụng quy đổi tiền tệ nhanh trên Mit App Inventor

Sau khi dự án khởi tạo xong, tại cây thư mục bên trái (chuyển chế độ xem sang

## 1.1. Thiết kế giao diện đồ họa trực quan

\- Mục tiêu: Xây dựng cấu trúc thẩm mỹ, bố cục và định hình toàn bộ giao diện người dùng (UI) cho hệ thống ứng dụng gồm 3 màn hình (Screen1, Screen2, Screen3).

**\-** Mô tả thanh công cụ cốt lõi: Giao diện Designer cung cấp hệ thống công cụ chia làm 4 cột quản lý chặt chẽ:

- Palette (Thanh thành phần): Chứa các linh kiện kéo thả như User Interface (Button, TextBox, Label, WebViewer) và Layout (HorizontalArrangement, VerticalArrangement để dàn hàng thành phần).
- Viewer (Màn hình mô phỏng): Không gian trực quan mô phỏng màn hình điện thoại để sắp xếp vị trí linh kiện.
- Components (Cây quản lý): Hiển thị cấu trúc phân cấp, danh sách các linh kiện đang có mặt trên màn hình để lập trình viên thực hiện đổi tên (Rename) tường minh theo chuẩn mã nguồn.
- Properties (Bảng thuộc tính): Nơi tùy chỉnh chi tiết thông số của từng linh kiện được chọn.
- Thao tác kéo thả và thay đổi thuộc tính:
- Giữ các thành phần từ thanh Palette thả vào màn hình Viewer, sau đó di chuyển sang cột Properties để cấu hình lại các thông số kỹ thuật.
- Để thiết lập trạng thái tĩnh ban đầu cho ứng dụng mà không cần viết code cấu hình giao diện. Ví dụ: Chỉnh thuộc tính Width = Match parent để nút bấm giãn vừa khít màn hình, tích chọn NumbersOnly cho TextBox nhập tiền để ép người dùng chỉ được nhập số, hoặc đổi Text hiển thị của nhãn thành "Ứng dụng đổi tiền offline".

## 1.2. Lập trình tư duy logic bằng khối lệnh

\- Mục tiêu: Định nghĩa hành vi, xây dựng thuật toán toán học và thiết lập luồng xử lý sự kiện tương tác giữa các màn hình.

\- Bản chất của việc kéo thả Block: Đây là phương thức lập trình trực quan (Visual Programming). Bản chất đằng sau mỗi khối hình màu sắc thực tế là những đoạn mã nguồn ngôn ngữ bậc cao (Java hoặc JavaScript) đã được nhà phát triển đóng gói sẵn.

- Các khối lệnh được thiết kế dưới dạng các hình khối có khớp nối âm - dương (khớp lồi và rãnh lõm) dựa trên lý thuyết ngôn ngữ nghiêm ngặt. Hệ thống chỉ cho phép các khối ghép nối vừa khít với nhau khi chúng hoàn toàn đồng nhất và đúng đắn về mặt cú pháp logic (Ví dụ: Không thể nhét một khối chữ String vào một khớp nối yêu cầu biến số Number).

\- Ưu điểm so với viết code truyền thống:

- Tốc độ phát triển sản phẩm cực nhanh (Fast Prototyping).
- Loại bỏ hoàn toàn 100% các lỗi cú pháp kinh điển của lập trình viên sơ cấp như: quên dấu chấm phẩy ;, thiếu dấu đóng mở ngoặc {}, hoặc gõ sai từ khóa hệ thống.

\- Nhược điểm:

- Hiệu năng phần cứng không được tối ưu sâu, ứng dụng chạy tốn tài nguyên hơn code thuần.
- Khi bài toán phình to hoặc xử lý thuật toán phức tạp, giao diện quản lý khối sẽ trở nên cực kỳ rối mắt, chồng chéo, gây khó khăn lớn cho việc bảo trì, đọc lại mã nguồn và mở rộng dự án.

## 1.3. Cơ chế tái sử dụng mã nguồn và điều hướng đa màn hình

\- Mục tiêu: Đồng bộ thuật toán và luồng dữ liệu mượt mà giữa các phân hệ màn hình của Bài tập lớn.

\- Cơ chế sao chép - dán khối lệnh nâng cao (Tính năng Balo - Backpack):

- Mô tả hành động: Tính năng Balo (Biểu tượng chiếc Balô ở góc trên bên phải màn hình Blocks) hoạt động như một bộ nhớ tạm Clipboard nâng cao của hệ thống. Khi muốn sao chép một cụm thuật toán lớn, lập trình viên chỉ cần dùng chuột gắp toàn bộ cụm khối lệnh đó thả vào biểu tượng chiếc Balo.
- Mục đích: Giúp tái sử dụng mã nguồn xuyên màn hình. Khi sang màn hình mới (Screen2 hoặc một dự án khác), lập trình viên chỉ cần click vào Balo và kéo cụm khối lệnh đó ra ngoài màn hình làm việc mà không cần mất công tìm kiếm và xây dựng lại từ đầu.

\- Logic điều hướng và nhúng tài nguyên:

- Ứng dụng triển khai khối lệnh open another screen with start value để truyền dữ liệu định danh từ Màn hình chính sang Màn hình chức năng.
- Tại Screen3, ứng dụng kéo thành phần WebViewer từ thanh công cụ, gọi hàm dữ liệu call WebViewer.GoToUrl và nạp vào đường link trang tỷ giá trực tuyến của Wise để nhúng thẳng giao diện web theo dõi tỷ giá trực ca vào ứng dụng theo đúng yêu cầu đề bài.

## 1.4. Thực hiện bài toán

- Tại trang chủ MIT App Inventor, chọn menu Projects -> chọn Start new project -> đặt tên dự án là BaiTapLon_AppInventor và bấm OK.
- Tại giao diện thiết kế màn hình chính (Screen1), kéo linh kiện Label vào để điền thông tin cá nhân và thêm 2 thành phần Button, đổi thuộc tính Text hiển thị tương ứng.
