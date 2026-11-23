# Cozy Life Planner — Android APK

Đây là **dự án nguồn** Capacitor cho Android, bao gồm bản Cozy Life Planner PWA được cung cấp trước đó trong thư mục `www/`. ZIP này **không phải APK**. GitHub Actions sẽ biên dịch APK sau khi bạn tải dự án lên GitHub.

## Cách tạo APK trên GitHub (không cần Android Studio)

1. Tạo **repository GitHub mới** tên `cozy-life-planner-android` (không ghi đè repo website hiện tại).
2. Giải nén ZIP, tải **nội dung bên trong** lên thư mục gốc repository mới. Quan trọng: thư mục `.github/workflows` là thư mục ẩn, cần tải đúng cấu trúc. Dùng GitHub web có thể khó tải thư mục ẩn; dùng Git trên MacBook sẽ dễ hơn.
3. Nếu dùng Terminal trên Mac, trong thư mục đã giải nén:

   ```bash
   git init
   git branch -M main
   git add .
   git commit -m "Initial Android app"
   git remote add origin https://github.com/duyento5813-ctrl/cozy-life-planner-android.git
   git push -u origin main
   ```

   Nếu repo GitHub mới được tạo với README sẵn, cần xử lý lịch sử git trước khi push; tốt nhất tạo repo **trống**.
4. Trên GitHub, mở tab **Actions** → **Build Cozy Life Planner APK** → **Run workflow**. Workflow cũng chạy khi push vào `main`.
5. Đợi job hoàn tất (màu xanh), vào phần **Artifacts**, tải `cozy-life-planner-debug-apk` rồi giải nén để lấy `app-debug.apk`.
6. Chép APK sang điện thoại Android và mở để cài. Android có thể yêu cầu cho phép cài từ nguồn này.

## Lưu ý quan trọng

- APK là **debug build**, dành cho cài đặt thử nghiệm; chưa phải bản phát hành ký bằng khóa riêng để đưa lên Google Play.
- Đăng nhập Supabase qua email/password có thể hoạt động trong WebView, nhưng cần **kiểm thử trên điện thoại thực tế**. Liên kết xác nhận/khôi phục mật khẩu hiện chuyển về URL GitHub Pages của website, không tự quay về APK; có thể đặt lại mật khẩu trên website rồi đăng nhập APK.
- LocalStorage của APK và website là hai vùng lưu trữ **riêng**. Đăng nhập cùng tài khoản và kiểm tra đồng bộ Supabase; nếu có xung đột, **không ghi đè dữ liệu quan trọng**.
- Ứng dụng tải thư viện Supabase từ CDN nên cần Internet khi khởi động lần đầu. Chưa đảm bảo hoạt động offline hoàn chỉnh.
- Khi cập nhật mã website, cập nhật các file tương ứng trong `www/` của dự án Android rồi chạy workflow lại.
- `supabase-config.js` chứa **publishable key** cho trình duyệt, không phải secret key. Đảm bảo RLS trên Supabase.
- Để xuất bản rộng rãi, cần kiểm tra luồng auth, quyền riêng tư, icon Android, ký APK release và quản lý nâng cấp phiên bản.
