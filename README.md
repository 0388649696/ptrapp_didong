# BÁO CÁO BÀI TẬP LỚN
**MÔN HỌC**: PHÁT TRIỂN ỨNG DỤNG TRÊN THIẾT BỊ DI ĐỘNG (TEE0419) **Họ và tên SV**: Nguyễn Đức Anh Tú **MSSV**: K225480106070
1.  Tên đề tài: Bài tập phát triển ứng dụng trên thiết bị di động
2.  Nội dung thực hiện:

- Phần 1: Phát triển ứng dụng trên nền tảng trực quan MIT App Inventor. Xây dựng ứng dụng, tìm hiểu bản chất kỹ thuật của lập trình kéo thả khối Block và cơ chế tái sử dụng mã nguồn bằng tính năng Balo (Backpack).
- Phần 2: Xây dựng ứng dụng Online kết nối Volley API trên Android Studio (Java)
- Phần 3: Xây dựng ứng dụng Offline đọc file Assets trên Android Studio

Ngày giao nhiệm vụ: 25/05/2026 | 
Ngày hoàn thành nhiệm vụ: 12/06/2026

Báo cáo: **PDF + readme**

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

## 1.2. Lập trình tư duy logic bằng khối lệnh:

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

## 1.4. Thực hiện bài toán:

- Tại trang chủ MIT App Inventor, chọn menu Projects -> chọn Start new project -> đặt tên dự án là BaiTapLon_AppInventor và bấm OK.
- Tại giao diện thiết kế màn hình chính (Screen1), kéo linh kiện Label vào để điền thông tin cá nhân và thêm 2 thành phần Button, đổi thuộc tính Text hiển thị tương ứng.

- Bấm nút Add Screen... trên thanh công cụ để tạo thêm 2 màn hình phụ: nhập tên màn hình thứ hai là Screen2 (màn hình giải toán quy đổi) và màn hình thứ ba là Screen3 (màn hình nhúng web tỷ giá).

- Tại màn hình Screen2, kéo thả 1 TextBox làm ô nhập tiền VND (tích chọn thuộc tính NumbersOnly), tạo nút bấm Button đại diện cho các đồng ngoại tệ (USD, CNY, EUR, USDT) và đặt 1 Label ở dưới cùng để chuẩn bị làm vùng hiển thị chuỗi kết quả đầu ra.

- Chuyển sang giao diện Blocks của Screen2, kéo ghép cụm khối lệnh logic: khi người dùng click vào một nút ngoại tệ bất kỳ, hệ thống tự động lấy số dữ liệu từ TextBox chia cho hằng số tỷ giá định sẵn, thực hiện nối chuỗi kết quả và gán hiển thị lên Label.

- Tại màn hình Screen3, kéo thành phần WebViewer từ danh mục linh kiện thả vào màn hình mô phỏng, sau đó chuyển sang giao diện Blocks chọn khối sự kiện khởi tạo when Screen3.Initialize rồi gắn khối hành động call WebViewer.GoToUrl chứa đường dẫn liên kết theo dõi tỷ giá trực tuyến của Wise.

- Giao diện hoàn thành sẽ trông như sau:

# BÀI TẬP 2: XÂY DỰNG ỨNG DỤNG ONLINE KẾT NỐI VOLLEY API TRÊN ANDROID STUDIO

**2.1. Kiến thức nền tảng và Cấu trúc hệ thống Android:**

Tệp AndroidManifest.xml: Là tệp cấu hình cốt lõi bắt buộc, mô tả toàn bộ thông tin cơ bản của ứng dụng cho hệ điều hành Android (tên ứng dụng, icon, các Activity thành phần). Do ứng dụng cần kết nối mạng để truyền dữ liệu lên Server, tệp cấu hình phải khai báo xin quyền truy cập Internet bằng cú pháp:

&lt;uses-permission android:name="android.permission.INTERNET" /&gt;

Mục đích nhằm thông báo cho hệ điều hành cấp phép mở luồng truyền tải dữ liệu qua không gian mạng cho ứng dụng.

Ngoài ra để định vị các file quan trọng theo yêu cầu đề bài:

- app / manifests / AndroidManifest.xml: File cấu hình hệ thống của ứng dụng (nơi khai báo các Activity, xin quyền Internet, quyền đọc file...).
- app / java / \[com.sv.k225480106070\] / MainActivity.java: File xử lý logic bằng code Java,
- app / res / layout / activity_main.xml: File thiết kế giao diện bằng mã XML hoặc kéo thả trực.
- app / res / values / strings.xml: Nơi lưu trữ tất cả các văn bản chuỗi trong app để tránh lỗi Hardcode theo yêu cầu của đề bài.

**2.2. Quản lý tài nguyên giao diện:**

Quản lý Layout và tránh Hardcode: Toàn bộ giao diện được định nghĩa bằng các tệp tin cấu trúc XML trong thư mục res/layout. Tuyệt đối không viết cứng (hardcode) các chuỗi chữ hiển thị trực tiếp vào file XML hoặc file code Java. Tất cả dữ liệu chữ được lưu tập trung tại tệp res/values/strings.xml.

- Cú pháp tham chiếu: Trong file XML layout sử dụng @string/tên_id (Ví dụ: android:text="@string/app_name"). Trong file code Java sử dụng lệnh getString(R.string.tên_id) hoặc tham chiếu trực tiếp qua định danh R.string.tên_id.
- Ưu điểm: Giúp mã nguồn sạch sẽ, dễ bảo trì, quản lý tập trung toàn bộ văn bản của ứng dụng tại một nơi duy nhất.
- Cơ chế Auto-OS: Hệ điều hành Android hỗ trợ tự động nhận diện và lấy giá trị cấu hình tương ứng theo LOCATION (Vị trí), LANGUAGE (Ngôn ngữ), và THEME (Giao diện Sáng/Tối) của thiết bị người dùng.

Đối tượng chứa (LinearLayout): Sử dụng cấu trúc LinearLayout để gộp các đối tượng con (Button, EditText, TextView) lại và sắp xếp hiển thị theo một quy luật nghiêm ngặt kề nhau theo chiều dọc (android:orientation="vertical") hoặc chiều ngang (horizontal). Thuộc tính android:gravity được áp dụng để căn chỉnh dòng chảy của toàn bộ nội dung con tập trung vào chính giữa hoặc các góc màn hình theo thiết kế UI.

**2.3. Cơ chế xử lý sự kiện tương tác**

Khi người dùng tác động vào ứng dụng (Click vào Button, TextView...), hệ thống cần bắt sự kiện để chạy một đoạn code xử lý.

- Yêu cầu tại Layout (XML): Linh kiện nút bấm hoặc chữ bắt buộc phải được định danh một mã ID duy nhất thông qua thuộc tính android:id="@+id/tên_id" để file Java có thể tìm thấy và liên kết.
- 2 cách viết code xử lý sự kiện trong Java:
- Cách 1 (Khai báo trực tiếp trong XML): Thêm thuộc tính android:onClick="tên_hàm" tại thẻ linh kiện trong file XML, sau đó viết hàm tương ứng có tham số (View v) trong file Java.
- Cách 2 (Sử dụng Bộ lắng nghe ẩn danh - Anonymous Listener): Ánh xạ linh kiện trong Java và gán bộ lắng nghe trực tiếp.
- Vấn đề: Hệ thống API của bộ môn được thiết kế theo một khung cấu trúc dữ liệu JSON dùng chung cho tất cả các dạng bài tập lớn của cả lớp (bao gồm các trường cố định như a, b, c, ketluan, nghiem). Để ứng dụng đổi tiền tệ tương thích hoàn hảo và được Server chấm điểm tự động, giải pháp ánh xạ biến khoa học đã được triển khai như sau:

{

"app_by": "K225480106070",

"input": {

"a": "100000", // Ánh xạ: Số tiền VND gốc do người dùng nhập vào

"b": "USD", // Ánh xạ: Mã tên loại ngoại tệ cần quy đổi

"c": "0", // Tham số phụ cấu trúc (Đặt mặc định bằng 0)

"name": "Đổi ngoại tệ"

},

"output": {

"ketluan": "Chuyển đổi thành: 3.83 USD",

"abc": "xyz", // Tham số phụ cấu trúc (mặc định)

"nghiem": 3.83 // Ánh xạ: Giá trị số thực sau tính quy đổi

}

}

**2.5. Thực hiện bài toán APP 2:**

Ứng dụng được xây dựng tương đương với logic trên MIT App Inventor bao gồm 3 Activity độc lập:

- Activity 1 (About): Hiển thị thông tin sinh viên và cấu hình 2 nút bấm để gọi kích hoạt chuyển sang 2 Activity chức năng còn lại.
- Activity 2 (Đổi ngoại tệ & Gửi API): Màn hình thực hiện chức năng nhập số tiền VND và quy đổi ngoại tệ. Mỗi khi người dùng bấm nút tính toán, ứng dụng sử dụng thư viện mạng Volley phát một yêu cầu mạng POST gửi dữ liệu lên Server tại địa chỉ http://k58kmt.tdh.io.vn/api.
- Dữ liệu truyền đi được đóng gói dưới dạng đối tượng JSON (JSONObject) chứa mã số sinh viên, số tiền nhập và loại ngoại tệ. Hệ thống tiếp nhận phản hồi dạng JSON từ Server, thực hiện bóc tách lấy trường dữ liệu định danh mã số nghiệm thu (id) và hiển thị Số thứ tự nghiệm thu trực quan lên màn hình thông qua dòng chữ kết quả và thông báo.

- Activity 3: Tích hợp đối tượng WebView trên toàn màn hình.

Khi Activity được khởi tạo, ứng dụng cấu hình mã lệnh webView.loadUrl("https://k58kmt.tdh.io.vn?masv=k225480106070"); để truy cập trực tiếp vào trang thông tin cá nhân và tỷ giá nội bộ của Server trường ngay bên trong ứng dụng.

# BÀI TẬP 3: TRIỂN KHAI CƠ CHẾ DỮ LIỆU OFFLINE QUA THƯ MỤC ASSETS

**3.1. Bản chất kỹ thuật và Quản lý tài nguyên trong thư mục Assets**

- Đặc tính của thư mục đặc biệt Assets: Thư mục assets trong cấu trúc dự án Android là một kho lưu trữ tài nguyên thô (Raw Assets). Khi sử dụng File Explorer (Windows) để sao chép trực tiếp các tệp tin hoặc thư mục vào đây, quá trình biên dịch (Compiler) sẽ đóng gói nguyên vẹn toàn bộ các tệp tin này đi theo bộ cài đặt ứng dụng (.apk).
- Cú pháp truy cập dữ liệu trong Java: Hệ thống không quản lý các tệp trong assets bằng mã ID thông qua file R. Để truy cập, ứng dụng bắt buộc phải gọi đối tượng AssetManager và thiết lập luồng đọc dữ liệu thông qua cú pháp:

AssetManager assetManager = getAssets();

InputStream inputStream = assetManager.open("tên_file.txt");

## 3.2. Đặt vấn đề:

**a. Cấu trúc dữ liệu đề xuất:**

Dữ liệu bảng giá quy đổi được lưu trữ dưới dạng tệp văn bản thô tĩnh mang tên tygia.txt đặt trong thư mục assets. Cấu trúc dữ liệu trong tệp được định dạng nghiêm ngặt theo quy tắc Chuỗi văn bản phân tách:

\[Mã_Ngoại_Tệ\]:\[Giá_Trị_Tỷ_Giá_VND\]

- Ví dụ nội dung file cấu hình:

USD:26098

CNY:3787

EUR:29551

USDT:26323

**b. Thuật toán xử lý**

Để trích xuất được con số tỷ giá chính xác phục vụ phép toán chia, ứng dụng triển khai thuật toán tiền xử lý chuỗi tuần tự:

- Bước 1: Khởi tạo BufferedReader kết hợp InputStreamReader để mở luồng quét bộ nhớ dữ liệu text.
- Bước 2: Sử dụng thuật toán vòng lặp while duyệt qua từng dòng văn bản thô của tệp tin.
- Bước 3: Sử dụng hàm kiểm tra điều kiện đầu chuỗi .startsWith(maTienCanTim + ":") để định vị chính xác dòng dữ liệu ngoại tệ người dùng yêu cầu.
- Bước 4: Áp dụng thuật toán Phân tách chuỗi (String Split) dựa trên ký tự phân tách dấu hai chấm (:) để rã dòng thành một mảng gồm 2 phần tử độc lập.
- Bước 5: Lấy phần tử chỉ số \[1\] (chuỗi chứa con số tỷ giá), thực hiện ép kiểu dữ liệu từ chuỗi ký tự sang số thực Double.parseDouble() để làm toán tử chia cho số tiền VND đầu vào.

**c. Đối tượng hiển thị**

- Công cụ hiển thị dữ liệu: Ứng dụng sử dụng linh kiện EditText (với thuộc tính nhập số) để nhận tiền gốc, 1 EditText nhận mã chữ đầu vào, và 1 TextView lớn đặt ở vùng trung tâm để xuất chuỗi kết quả tính toán cuối cùng ra màn hình.
- Kết quả kiểm thử thực tế trên máy ảo: Ứng dụng chạy cắm song song, độc lập hoàn toàn với APP 2. Khi ngắt toàn bộ kết nối Internet của thiết bị, người dùng nhập số tiền 261000 VND, nhập mã ngoại tệ USD và kích hoạt nút tính toán, ứng dụng lập tức bóc tách file văn bản hệ thống, thực hiện phép chia và kết xuất chuỗi hoàn hảo: "Chuyển đổi thành: 10.00 USD" ra màn hình giao diện.

- Kết quả chương trình:

# KẾT LUẬN

Qua quá trình thực hiện bài tập lớn môn Phát triển ứng dụng trên thiết bị di động, em đã hoàn thành toàn diện các mục tiêu đề bài đặt ra, bao gồm việc xây dựng ứng dụng đa màn hình trên nền tảng trực quan MIT App Inventor và triển khai song song hai giải pháp công nghệ độc lập (Offline đọc file Assets và Online kết nối qua Volley API) trên môi trường chuyên nghiệp Android Studio bằng ngôn ngữ Java.

Thông qua bài tập lớn này, em đã rèn luyện được tư duy lập trình hệ thống bài bản, hiểu rõ cơ chế vận hành Client - Server và cách xử lý bóc tách cấu trúc dữ liệu JSON thời gian thực. Đặc biệt, việc tự đối mặt và xử lý thành công các xung đột luồng của máy ảo phần cứng cũng như lỗi bất đồng chứng chỉ mạng giúp em hình thành kỹ năng phân tích nguyên nhân gốc rễ và giải quyết các bài toán kỹ thuật phát sinh trong thực tế một cách độc lập, hiệu quả. Đây là những kiến thức và nền tảng kinh nghiệm thực tiễn vô cùng giá trị để em tiếp tục phát triển chuyên sâu trong lĩnh vực lập trình di động nói riêng và công nghệ phần mềm nói chung.

Em xin chân thành cảm ơn thầy Đỗ Duy Cốp, người đã tận tình hướng dẫn, định hướng và hỗ trợ em trong suốt quá trình thực hiện bài tập lớn. Những kiến thức và sự chỉ bảo của thầy đã giúp em vượt qua nhiều khó khăn, hiểu sâu hơn về nội dung học phần và hoàn thành bài báo cáo một cách hiệu quả hơn.

 

# MÃ QR GITHUB

**BÁO CÁO**
