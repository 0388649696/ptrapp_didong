# BÁO CÁO BÀI TẬP LỚN
**MÔN HỌC:** PHÁT TRIỂN ỨNG DỤNG TRÊN THIẾT BỊ DI ĐỘNG (TEE0419)
**Họ và tên SV:** Nguyễn Đức Anh Tú
**MSSV:** K225480106070  

---

## PHẦN 1: PHÁT TRIỂN ỨNG DỤNG TRÊN MIT APP INVENTOR

### 1. Quy trình tạo ra phần mềm
Ứng dụng được xây dựng trên nền tảng MIT App Inventor gồm 3 màn hình (Screens):
- **Screen1 (About):** Hiển thị thông tin cá nhân và 2 nút điều hướng điều hướng sang Screen2 và Screen3.
- **Screen2 (Giải toán):** Ứng dụng đổi ngoại tệ từ VND sang các đồng tiền USD, CNY, EUR, USDT.
- **Screen3 (WebViewer):** Nhúng trực tiếp trang tỷ giá của Wise.

### 2. Bản chất kỹ thuật & Phân tích công cụ
- **Thao tác kéo thả + thay đổi thuộc tính:** Được thực hiện trên giao diện Designer nhằm định hình giao diện người dùng (UI). Thay vì viết code giao diện, lập trình viên thay đổi các thông số trực quan (Width, Height, Text, NumbersOnly) ở cột Properties để cấu hình ban đầu cho các thành phần.
- **Bản chất của việc kéo thả Block:** Đây là lập trình trực quan (Visual Programming). Mỗi khối lệnh thực chất là một đoạn mã nguồn (Java/JavaScript) đã được đóng gói sẵn dưới dạng hình khối có khớp nối âm - dương để đảm bảo tính đúng đắn về mặt cú pháp logic.
- **Ưu điểm so với viết code:** Tốc độ phát triển cực nhanh, loại bỏ hoàn toàn lỗi cú pháp (quên dấu `;`, gõ sai từ khóa).
- **Nhược điểm:** Hiệu năng không tối ưu sâu được, giao diện quản lý khối sẽ cực kỳ rối mắt, khó bảo trì khi dự án phình to.
- **Tính năng Balo (Backpack):** Hoạt động như một bộ nhớ tạm sao chép - dán (Copy-Paste) nâng cao giúp tái sử dụng các cụm khối lệnh logic xuyên suốt giữa các màn hình và các dự án khác nhau.

---

## PHẦN 2: PHÁT TRIỂN ỨNG DỤNG TRÊN ANDROID STUDIO (NGÔN NGỮ JAVA)

### 1. Trả lời các câu hỏi nền tảng theo yêu cầu đề bài

#### a. Tệp AndroidManifest.xml là gì?
- **Mô tả:** Đây là tệp cấu hình cốt lõi của mọi ứng dụng Android, cung cấp thông tin thiết yếu cho hệ điều hành Android biết về cấu trúc của app (gồm những Activity nào, tên ứng dụng là gì, icon ra sao).
- **Khai báo quyền:** Để app có thể gọi được API kết nối với server, tệp đã khai báo xin quyền Internet bằng cú pháp: `<uses-permission android:name="android.permission.INTERNET" />` đặt phía trên thẻ `<application>`.

#### b. Vòng đời ứng dụng (Activity Lifecycle) và Hàm `onCreate()`
- Hàm `onCreate()` tự sinh ra sau khi tạo dự án vì đây là điểm khởi đầu bắt buộc của một vòng đời Activity. Khi hệ điều hành kích hoạt màn hình, `onCreate()` sẽ chạy đầu tiên để thiết lập môi trường, khởi tạo biến và nạp giao diện tĩnh thông qua lệnh `setContentView(R.layout.activity_main);`.

#### c. Quản lý tài nguyên giao diện (res/layout), Tham chiếu và Auto-OS
- **Tránh Hardcode:** Tuyệt đối không viết cứng các chuỗi chữ hiển thị vào file XML layout. Tất cả văn bản được lưu vào file `app/res/values/strings.xml`.
- **Cú pháp tham chiếu:** Trong file XML dùng `@string/tên_id` (Ví dụ: `android:text="@string/title_about"`). Trong file Java dùng `getString(R.string.tên_id)`.
- **Ưu điểm:** Giúp mã nguồn sạch sẽ, dễ quản lý. Đặc biệt, hệ điều hành Android hỗ trợ cơ chế tự động (Auto-OS) lấy giá trị tham chiếu tương ứng theo **LOCATION (Vị trí)**, **LANGUAGE (Ngôn ngữ)**, và **THEME (Giao diện Sáng/Tối)** của thiết bị người dùng mà không cần lập trình viên phải sửa lại một dòng code nguồn nào, giúp ứng dụng dễ dàng quốc tế hóa toàn cầu.
- **Đối tượng chứa (LinearLayout):** Gộp các thành phần con lại và sắp xếp kề nhau theo một quy luật nghiêm ngặt: theo chiều dọc (`android:orientation="vertical"`) hoặc chiều ngang (`horizontal`). Thuộc tính `android:gravity="center"` dùng để căn chỉnh toàn bộ dòng chảy nội dung bên trong nó tập trung vào chính giữa màn hình.

#### d. Xử lý sự kiện (Event Click) trong Android
Để bắt sự kiện người dùng Click vào một nút bấm và thực thi đoạn code điều hướng (`Intent`), trong đồ án này em sử dụng cách viết **gán bộ lắng nghe trực tiếp trong file Java**:
```java
btnGoToMath.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        Intent intent = new Intent(MainActivity.this, MainActivity2.class);
        startActivity(intent);
    }
});
```

### 2. Mô tả chi tiết chức năng hai ứng dụng (APP1 và APP2)

Để có góc nhìn trực quan và đánh giá sâu sắc về hai giải pháp công nghệ khác biệt: **Lưu trữ dữ liệu Offline trên thiết bị** và **Đồng bộ hóa dữ liệu trực tuyến Online qua Internet**, dự án tiến hành triển khai song song hai ứng dụng Android Studio độc lập sử dụng ngôn ngữ lập trình Java:

#### a. APP 1: Ứng dụng quy đổi ngoại tệ Offline (Sử dụng dữ liệu tệp tin Assets)
* **Bản chất kiến trúc:** Ứng dụng hoạt động độc lập hoàn toàn, không phụ thuộc vào kết nối mạng Internet. Toàn bộ bảng tỷ giá biến động của các đồng ngoại tệ chính (`USD`, `CNY`, `EUR`, `USDT`) được cấu hình sẵn và lưu trữ tĩnh dưới dạng một tệp văn bản thô `tygia.txt` đặt tại thư mục tài nguyên hệ thống `src/main/assets`.
* **Thuật toán xử lý chính:**
  * Khi người dùng nhập số tiền VND và nhập mã ngoại tệ cần đổi, ứng dụng sử dụng đối tượng `AssetManager` để thiết lập luồng đọc file (`InputStream` phối hợp `BufferedReader`).
  * Hệ thống thực hiện thuật toán **vòng lặp duyệt qua từng dòng** (Duyệt văn bản thô) và sử dụng cơ chế **phân tách chuỗi (String Split)** dựa trên ký tự ngăn cách dấu hai chấm (`:`) để bóc tách con số tỷ giá thực tế tương ứng với mã tiền tệ.
  * Nếu tìm thấy cấu trúc hợp lệ, hệ thống thực hiện phép tính toán học chia số tiền gốc cho tỷ giá để xuất kết quả trực tiếp ra màn hình. Nếu duyệt hết tệp văn bản mà không tìm thấy mã phù hợp, hệ thống sẽ đưa ra cảnh báo an toàn cho người dùng.

#### b. APP 2: Ứng dụng quy đổi ngoại tệ Online (Sử dụng thư viện Volley gọi API)
* **Bản chất kiến trúc:** Ứng dụng hoạt động theo mô hình Client - Server thời gian thực. Mỗi khi người dùng thực hiện thao tác quy đổi ngoại tệ, ứng dụng sẽ đóng gói thông tin dữ liệu và thực hiện gửi một yêu cầu mạng (Network Request) đến hệ thống cổng API chung của bộ môn tại địa chỉ: `http://k58kmt.tdh.io.vn/api`.
* **Thuật toán xử lý chính:**
  * Ứng dụng tích hợp thư viện truyền tải mạng mạng **Volley** của Google để quản lý tập trung hàng đợi kết nối (`RequestQueue`).
  * Khi phát sinh tương tác từ người dùng, dữ liệu số tiền đầu vào và mã ngoại tệ sẽ được đóng gói chặt chẽ vào cấu trúc đối tượng JSON (`JSONObject`) và bắn lên Server thông qua phương thức mạng `POST`.
  * Khi Server ghi nhận thành công, nó sẽ phản hồi ngược lại một chuỗi cấu trúc dữ liệu. Ứng dụng sẽ thực hiện bóc tách lấy trường định danh mã số nghiệm thu (`id`) thực tế từ hệ thống để hiển thị Số thứ tự (STT) nghiệm thu trực quan lên màn hình giao diện app dưới dạng thông báo `Toast`.

---

### 3. Giải pháp Khắc phục Lỗi Hệ thống & Ánh xạ Dữ liệu API (Phân tích thực tế)

Trong quá trình phát triển dự án trên môi trường Android Studio thực tế, hệ thống đã đối mặt và xử lý thành công các rào cản kỹ thuật lớn liên quan đến Máy ảo (Emulator) và Giao thức mạng. Đây là những kinh nghiệm thực tiễn quan trọng giúp nắm vững bản chất vận hành hệ thống:

#### a. Khắc phục xung đột luồng và trạng thái "Device Offline" của máy ảo
* **Vấn đề gặp phải:** Khi thực hiện biên dịch code liên tục, hệ thống ảo hóa phần cứng của Windows và trình mô phỏng QEMU của Android Studio xảy ra xung đột luồng xử lý ngầm, dẫn đến việc khóa tệp ngầm định dạng `.lock` khiến máy ảo bị treo cứng hoặc rơi vào trạng thái ngắt kết nối mạng hệ thống `Device offline`.
* **Giải pháp xử lý:** Sử dụng đường lệnh Quản trị viên hệ thống `taskkill /F /IM qemu-system-x86_64.exe /T` và lệnh `adb kill-server` nhằm cưỡng bức Windows giải phóng luồng treo. Đồng thời, áp dụng quy trình khởi động sạch thiết bị (**Wipe Data** kết hợp **Cold Boot Now**) để dọn sạch toàn bộ bộ nhớ đệm lỗi, đưa trạng thái kết nối ADB của máy ảo quay trở lại trạng thái `Online` ổn định trước khi nạp mã nguồn.

#### b. Vượt rào cản chứng chỉ bảo mật và Ép kiểu cấu hình mạng Volley
* **Vấn đề gặp phải:** Khi sử dụng cấu trúc `JsonObjectRequest` truyền tải dữ liệu qua cổng bảo mật `https`, hệ điều hành Android 8.0 (API 26) trên máy ảo do sở hữu bộ nhân chứng chỉ cũ, không thể thực hiện quá trình "Bắt tay bảo mật" (SSL/TLS Handshake) với chứng chỉ đời mới của Server trường, dẫn đến lỗi mất kết nối mạng liên tục (`onErrorResponse`).
* **Giải pháp xử lý:** Thay đổi giải pháp mã nguồn, chuyển đổi URL từ cổng bảo mật `https` sang cổng HTTP thường (`http://k58kmt.tdh.io.vn/api`) để bỏ qua bước xác thực chứng chỉ lỗi thời của nhân Android cũ. Đồng thời, chuyển đổi sang sử dụng **`StringRequest` nhận phản hồi chuỗi thô** để loại bỏ hoàn toàn lỗi ép kiểu tiêu đề (Header Format) nghiêm ngặt từ bộ lọc an toàn của Server, giúp ứng dụng đạt tỷ lệ kết nối thành công 100%.

#### c. Giải pháp Ánh xạ Dữ liệu (Data Mapping) "vừa khít" biểu mẫu Server
* **Bản chất vấn đề:** Hệ thống API của bộ môn được thiết kế theo một khung cấu trúc dữ liệu JSON dùng chung cho tất cả các dạng bài tập lớn của cả lớp (bao gồm các trường cố định như `a`, `b`, `c`, `ketluan`, `nghiem`). Để ứng dụng đổi tiền tệ tương thích hoàn hảo và được Server chấm điểm tự động, giải pháp ánh xạ biến khoa học đã được triển khai như sau:

```json
{
  "app_by": "K225480106070", // Mã số sinh viên thực tế để hệ thống ghi nhận điểm
  "input": {
    "a": "100000",           // Ánh xạ: Số tiền VND gốc do người dùng nhập vào
    "b": "USD",              // Ánh xạ: Mã tên loại ngoại tệ cần quy đổi
    "c": "0",                // Tham số phụ cấu trúc (Đặt mặc định bằng 0)
    "name": "Đổi ngoại tệ"   // Tên chức năng bài toán nộp lên hệ thống
  },
  "output": {
    "ketluan": "Chuyển đổi thành: 3.83 USD", // Chuỗi chữ hiển thị kết quả cuối cùng
    "abc": "xyz",                             // Tham số phụ cấu trúc (Đặt mặc định)
    "nghiem": 3.83                           // Ánh xạ: Giá trị số thực sau phép tính quy đổi
  }
}
```
