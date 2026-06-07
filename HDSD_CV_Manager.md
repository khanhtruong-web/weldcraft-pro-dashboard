# 📖 HƯỚNG DẪN SỬ DỤNG - HR CVs MANAGEMENT DASHBOARD

**Dành cho Tuyển dụng & Quản lý nhân sự các dự án Dầu khí (Oil & Gas), Offshore, Điện gió.**

---

## Phần 1: Hướng Dẫn Tải Về & Chạy Ứng Dụng (Dành cho người không rành IT)

Hệ thống được thiết kế dưới dạng Single Page Application (Web-App) siêu nhẹ và bảo mật. Nó không yêu cầu bạn phải cài đặt bất cứ máy chủ phức tạp nào.

1. **Chuẩn bị file:** Đảm bảo bạn đã có file `HR_CVs_App.html` và file `Run_HR_App.bat` lưu trong cùng một thư mục (ví dụ: `D:\AI App\`).
2. **Khởi động ứng dụng:** 
   - Rất đơn giản, bạn chỉ cần **click đúp chuột (nhấp đúp)** vào file `Run_HR_App.bat`.
   - Một màn hình đen (Terminal) sẽ chớp nhanh, và sau đó trình duyệt Chrome/Edge của bạn sẽ tự động mở lên tại địa chỉ `http://127.0.0.1:8080/HR_CVs_App.html`.
3. **Lưu ý:** Không nên mở trực tiếp file `html` bằng cách nhấp đúp vào nó, vì một số tính năng bảo mật của Google (như đăng nhập OAuth) sẽ yêu cầu bạn chạy qua giao thức `http` (local server) thay vì `file://`. Đó là lý do bạn nên dùng file `.bat` để khởi chạy.

---

## Phần 2: Hướng Dẫn Tính Năng Chi Tiết (Sử Dụng App)

### 1. Đăng nhập & Cơ chế phân quyền (Role-based Access)

*Giao diện Đăng nhập Google an toàn, tích hợp trực tiếp với Workspace của bạn.*

- Bấm vào nút **"Sign in with Google"**. Hệ thống sẽ yêu cầu bạn chọn tài khoản Google (Gmail hoặc email công ty).
- **Phân quyền tự động:** 
  - 👑 **Admin**: Toàn quyền cài đặt hệ thống, xóa dữ liệu, cấu hình API, và toàn quyền quản lý CV.
  - 📝 **Editor / Recruiter** (Tuyển dụng): Có thể Upload CV, sử dụng AI trích xuất dữ liệu, chỉnh sửa và xuất file, nhưng không được can thiệp vào Settings hay Xóa toàn bộ dữ liệu.
  - 👁️ **Viewer** (Xem báo cáo): Chỉ xem được bảng điều khiển (Dashboard), tìm kiếm nhân sự và xem biểu đồ báo cáo.

### 2. Cài đặt Hệ thống (Settings Tab)
*(Chỉ dành cho Admin)*

Mục này để thiết lập "bộ não" cho ứng dụng.
- **Disciplines (Ngành nghề/Chuyên môn):** Bạn có thể bấm nút **+ Add** để thêm các chuyên môn đặc thù (VD: `Welding`, `Subsea`, `Piping Inspector`). Hệ thống sẽ tự động đồng bộ danh sách này vào Cloud.
- **API Keys Setup:**
  - **Gemini API Key:** (Bắt buộc) Lấy từ Google AI Studio, để trí tuệ nhân tạo có thể đọc và hiểu CV.
  - **Google Sheet ID:** Nhập ID của Sheet để hệ thống lưu file log (App_Logs) và lưu dữ liệu.
- **Connect Google Drive & Sync:**
  - Nhập **Client ID** của bạn và bấm **Connect**.
  - Nó giúp đồng bộ toàn bộ cơ sở dữ liệu `cv_extractor_backup.json` lên đám mây. Bạn đăng nhập máy khác cũng sẽ tự động tải lại dữ liệu cũ về. Không lo mất mát.

### 3. CV Extraction (Trích xuất CV tự động bằng AI)
*Đây là bước đầu tiên và quan trọng nhất.*

- **Upload:** Kéo thả hàng chục file CV (.pdf, .docx) vào khung đứt đoạn.
- Bấm **Extract Data**: AI sẽ đọc từng CV, bóc tách các trường: *Họ tên, Số năm kinh nghiệm, Học vấn (Education), Lĩnh vực hoạt động, Chuyên môn hẹp, và tự động gán Discipline*.
- **Review (Kiểm tra đối chiếu trực tiếp):**
  - Trong bảng kết quả, bạn sẽ thấy cột Action có nút hình **Cái Bút (Review & Edit)**.
  - Nhấp vào đó, một cửa sổ lớn sẽ hiện ra. Bên trái là **Giao diện đọc PDF/WORD** trực tiếp cực rõ nét. Bên phải là thông tin AI vừa bóc tách.
  - Bạn có thể so sánh chéo bằng mắt, chỉnh sửa nếu AI làm sai, và ấn nút **Save**.
- **Cảnh báo trùng lặp:** Nếu bạn lỡ tải lên 1 CV đã có trong hệ thống, hộp thoại sẽ hiện lên hỏi bạn có muốn cập nhật (overwrite) hay bỏ qua.

### 4. Smart Search (Tìm kiếm thông minh)

Dành cho lúc bạn cần gấp một kỹ sư có 10 năm kinh nghiệm về Piping.
- Chọn tab **Smart Search**.
- Bạn gõ "Piping" vào ô tìm kiếm, chọn *Min Exp = 10*, chọn Discipline = NDT/Inspection.
- Hệ thống sẽ lọc ra ngay lập tức lập danh sách kỹ sư đạt yêu cầu.

### 5. Company Templates (Định dạng lại CV theo chuẩn Công ty)

- Ứng dụng cung cấp các Template mặc định hoặc cho phép bạn upload mẫu file `.docx` theo thương hiệu công ty bạn (Upload Company CV Template).
- Bạn chọn 1 ứng viên, chọn mẫu Template và bấm **Export to Word**. Toàn bộ dữ liệu của ứng viên sẽ được AI "trám" vào file Word một cách đẹp mắt, chuyên nghiệp để gửi ngay cho đối tác/khách hàng.

### 6. Dashboard & Reports (Bảng điều khiển & Báo cáo)

- **Dashboard:** Hiển thị tổng quan bao nhiêu CV mới trong tháng, biểu đồ phân bố ngành nghề, biểu đồ kinh nghiệm.
- Có tính năng theo dõi Log (Nhật ký hoạt động): Ai vừa đăng nhập, ai vừa tải lên bao nhiêu CV.
- Toàn bộ hành động đều được **Data Log** tự động gửi về Google Sheet để kiểm toán và truy vết.

---
**Chúc bạn có trải nghiệm tuyệt vời và tăng tốc quy trình tuyển dụng lên gấp nhiều lần!**
