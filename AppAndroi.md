2. Viết app sử dụng Android Studio
   + Android manifest.xml  => mô tả gì? app cần quyền để do-st: khai báo ntn? để làm gì?
   + vòng đời của 1 ứng dụng android.
     code tự sinh sau khi tạo 1 project: có sẵn hàm onCreate: tại sao???
   + Code: java language. 
     app cần check xem có quyền để do-st? : code ntn? ý nghĩa?
     giao diện: (res/layout) mô tả bằng file XML + UI Design review
        + thuộc tính text, hoặc các thuộc tính khác: giá trị hardcode => lưu vào nới khác, tham chiếu tới nó:
          cú pháp của việc tham chiếu là gì?
          ưu điểm của việc tham chiếu này?
          OS hỗ trợ auto việc lấy giá trị tham chiếu theo LOCATION, LANGUAGE, THEME
          việc hỗ trợ auto này giúp app làm được điều gì?	
        + đối tượng chứa: gộp các đối tượng con lại: cùng 1 quy luật sắp xếp để hiển thị 
          các đối tượng con nằm kề nhau theo chiều dọc | hoặc ngang, gravity
     code tương tác với layout: vd hiển thị text
          mong muốn text hiển thị phù hợp với thiết lập LOCATION, LANGUAGE, THEME của người dùng
          thì làm ntn? (tránh hardcode)
     event (sự kiện) người dùng tác động vào app: CLICK vào button, click vào text,...
          với 1 sự kiện nào đó, muốn chạy 1 đoạn code để do-st
          thì LAYTOUT cần làm gì?
              CODE viết như nào (2 cách)
APP2 (android studio):  tạo app tương đương với Mit App inventor
  app có 3 activity
  + activity1: about: about+nút gọi sang 2 activity còn lại
  + activity2: giải toán đơn giản (tuỳ ý). mỗi khi giải xong bài toán: gọi api tại https://k58kmt.tdh.io.vn/api
    để gửi bài toán lên đó
    {app_by:mã số sv, input: {a:1,b:2,c:3,name:"hello tắc kè"},output:{ketluan:"vô nghiệm", abc:"xyz", nghiem:3.14}}
    nhận lại json: {ok:1, stt:1234}
  + activity3: 
    dùng web-view để truy cập từ 
    1 trang web https://k58kmt.tdh.io.vn?masv=mã sv của bạn

#
# Trả lời câu hỏi lý thuyết: 
1. Android Manifest.xml
+ Mô tả gì?: Đây là "bản thiết kế" hoặc "chứng minh thư" của ứng dụng. Nó mô tả các thành phần cơ bản (Activity, Service, Receiver), thông tin gói (Package name), phiên bản, và các cấu hình hệ thống (Theme, Icon).
+ Khai báo quyền (Permissions):
Cú pháp: <uses-permission android:name="android.permission.NAME" /> (đặt trước thẻ <application>).
Để làm gì?: Để bảo vệ quyền riêng tư và bảo mật. Ứng dụng phải xin phép hệ điều hành để truy cập các tài nguyên nhạy cảm như Internet, Camera, Vị trí... Nếu không khai báo, hệ thống sẽ chặn các hành động này để bảo vệ người dùng.
#
3. Vòng đời ứng dụng (Activity Lifecycle)
Tại sao có sẵn onCreate?: Đây là hàm quan trọng nhất và là điểm khởi đầu (Entry point) của một Activity.
Khi bạn mở app, hệ thống gọi onCreate để: Thiết lập giao diện (setContentView/setContent), khởi tạo các biến, và chuẩn bị dữ liệu. Nếu không có nó, Activity sẽ không biết phải hiển thị gì lên màn hình.
#
4. Code & Giao diện (Java/Kotlin)
+ Kiểm tra quyền trong code:
   + Cú pháp: ContextCompat.checkSelfPermission(context, PermissionName).
   + Ý nghĩa: Với các quyền nhạy cảm (Dangerous Permissions), khai báo trong Manifest là chưa đủ, code phải kiểm tra xem người dùng thực tế đã nhấn "Cho phép"      (Allow) lúc chạy app hay chưa để tránh app bị văng (Crash).
+ Tham chiếu tài nguyên (Resources):
Cú pháp:
   +  Trong XML: @string/tên_biến (Ví dụ: @string/app_name).
   + Trong Code: R.string.tên_biến (Ví dụ: R.string.app_name).
   + Ưu điểm: Dễ quản lý, dễ bảo trì (chỉ cần sửa 1 nơi), và đặc biệt là hỗ trợ đa ngôn ngữ. Hỗ trợ tự động (Location, Language, Theme): Giúp app tự động thay đổi ngôn ngữ (Tiếng Anh/Việt) hoặc giao diện (Sáng/Tối) dựa trên cài đặt máy của người dùng mà không cần viết thêm logic code phức tạp.
#
5. Đối tượng chứa (Layout Containers)
Quy luật: Các đối tượng con được sắp xếp theo:
LinearLayout: Xếp kề nhau theo chiều dọc (vertical) hoặc ngang (horizontal).
Gravity: Điều chỉnh vị trí của nội dung bên trong đối tượng (căn trái, căn giữa, căn phải).
#
6. Tương tác Layout & Tránh Hardcode
Cách làm: Thay vì viết textView.setText("Chào bạn"), ta dùng textView.setText(R.string.welcome).
Hệ thống sẽ tự tra cứu trong file strings.xml tương ứng với ngôn ngữ của máy để hiển thị nội dung phù hợp.
#
7. Sự kiện (Events - Click)
Để chạy code khi Click, Layout cần làm gì?: Layout cần xác định rõ đối tượng đó có ID (ví dụ: android:id="@+id/btn_solve") để code có thể tìm thấy và gắn sự kiện.
2 cách viết code sự kiện:
+ Cách 1 (Trong XML): Dùng thuộc tính android:onClick="tên_hàm". Sau đó viết hàm tương ứng trong Activity. (Cách này đơn giản nhưng hiện nay ít dùng hơn).
+ Cách 2 (Trong Code - Phổ biến): Sử dụng hàm lắng nghe sự kiện:
   + button.setOnClickListener { ... } (Kotlin).
   + button.setOnClickListener(new View.OnClickListener() { ... }) (Java).
#
# Thiết Kết Phần mềm: 

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/52c9ec30-a5a8-4828-ac53-ee223dab192f" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/87eaf85a-b144-4a95-8a01-49db93f3e320" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cd1ba74b-5ec8-42b9-a2f7-cfeb0ba2c6a8" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1ffb55d0-253a-4276-aeaf-03bc98c138ca" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0c092717-daf4-4fee-865e-0c68cdbc8196" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/9dd2f66b-f467-4bb4-abea-02f9e2115542" />

# Kết quả của phần mềm khi chạy trên thiết bị Redminote 11: 

<img width="460" height="1024" alt="image" src="https://github.com/user-attachments/assets/f5d792c8-b92a-481b-94c4-7bcad15570c9" />
<img width="460" height="1024" alt="image" src="https://github.com/user-attachments/assets/926a29ec-22b2-479a-8e55-96194c675feb" />
<img width="460" height="1024" alt="image" src="https://github.com/user-attachments/assets/48434ae2-8caf-4626-9227-f163bc68f1b8" />
