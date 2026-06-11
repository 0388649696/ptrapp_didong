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
