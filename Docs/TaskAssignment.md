# TaskAssignment.md — Phân công công việc chi tiết

* **Dự án:** Quản lý đề thi trắc nghiệm (Exam Bank) — Môn Công nghệ XML
* **Nhóm:** 3 người — Tài, Thiết, Vinh
* **Thời gian:** 7 tuần
* **Tài liệu gốc:** `ProjectBackground.md` **v2.2** (mọi tham chiếu "Phần 6.x" bên dưới theo bản v2.2)
* **Nguyên tắc:** Mỗi người có việc ở mọi giai đoạn. Task nào cũng có Definition of Done (DoD) rõ ràng.

> **THAY ĐỔI SO VỚI v1.0 (khối lượng và số task của từng người giữ nguyên: Tài 18 / Thiết 11 / Vinh 10 / chung 8):**
> 1. Đồng bộ với `ProjectBackground` v2.2: thẻ nested là `<CacCauHoi>`, XSD có `xs:key`/`xs:unique`, mật khẩu SHA-256, XSLT dùng `document()`, FK chéo "câu hỏi cùng môn với đề", quy tắc chặn xóa. Đánh số lại: XML = 6.1–6.4, XSD = 6.5–6.8, XSLT = 6.9.
> 2. **Sửa mâu thuẫn phụ thuộc:** form Đăng nhập (T-C02) cần `Login()` nên `NguoiDungDAL` (T-A11) được đưa lên **tuần 2**; `T-A05` (tạo solution) lùi lên cuối tuần 1 để nhường chỗ.
> 3. **Sửa mâu thuẫn phụ thuộc:** form Xem đề (T-B06, tuần 4) không còn phụ thuộc xuất PDF (T-A15, tuần 6); nút PDF được gắn sau khi T-A15 xong.
> 4. `T-A14` đổi cách làm: validation đặt trong lớp DAL (một chỗ) thay vì sửa lần lượt từng form.
> 5. **Chia nhỏ việc viết báo cáo** thành mốc nháp (tuần 4–5) và mốc hoàn chỉnh (tuần 7) cho T-A18, T-B11, T-C10, thay vì dồn hết vào tuần 7.
> 6. Bổ sung các phần còn thiếu trong task cũ: lớp `Session`, thư mục `Models/`, *Copy to Output Directory*, `xs:key`/`xs:unique`, XSLT `document()`, XPath, giới hạn mã 999, `Log.xsd`.

---

## 📑 MỤC LỤC

1. [Tổng quan phân công](#1-tổng-quan-phân-công)
2. [Task của Tài](#2-task-của-tài)
3. [Task của Thiết](#3-task-của-thiết)
4. [Task của Vinh](#4-task-của-vinh)
5. [Task chung (cả 3 người)](#5-task-chung-cả-3-người)
6. [Timeline & Deadline](#6-timeline--deadline)
7. [Quy ước làm việc nhóm](#7-quy-ước-làm-việc-nhóm)
8. [Checklist nghiệm thu cuối dự án](#8-checklist-nghiệm-thu-cuối-dự-án)

---

## 1. TỔNG QUAN PHÂN CÔNG

| Thành viên | Vai trò chính | Số task chính | Số task phụ | Khối lượng | Độ khó |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **Tài** | Data Layer + Logic + Integration + Báo cáo chính | 18 | 6 | ~45% | ⭐⭐⭐⭐⭐ |
| **Thiết** | XSLT + Hiển thị + Xuất file + Hỗ trợ báo cáo | 11 | 6 | ~30% | ⭐⭐⭐ |
| **Vinh** | UI/UX + CRUD Forms + Phân quyền + Test | 10 | 6 | ~25% | ⭐⭐⭐ |

### Nguyên tắc phân công
* **Tài** giữ các task "xương sống": XML, XSD, DAL, validation, tạo đề, tích hợp, báo cáo phần khó.
* **Thiết** giữ các task "hiển thị": XSLT, WebBrowser, xuất HTML, form xem đề, đổi mật khẩu, thống kê.
* **Vinh** giữ các task "giao diện": wireframe, form đăng nhập/main/CRUD, tìm kiếm, phân quyền UI, test case.
* **Task chung** (họp, test tích hợp, viết kết luận) chia đều.

### Quy tắc phối hợp (để tránh chờ nhau)
* Người làm **form** không cần đợi DAL xong mới bắt đầu: dựng giao diện trước bằng dữ liệu giả (hard-code `List<...>` tạm), rồi nối DAL khi Tài báo xong.
* Người làm **DAL/Helper** phải gửi vào group chat ngay khi merge, kèm 2–3 dòng ví dụ gọi hàm.
* Hợp đồng giữa các lớp (tên hàm, kiểu trả về) nằm trong mô tả task; muốn đổi chữ ký hàm phải báo trong group trước.

---

## 2. TASK CỦA TÀI

### 🔴 T-A01: Rà soát và chốt tài liệu ProjectBackground.md v2.2
* **Mô tả:** Bản v2.2 đã được cập nhật (ngày chốt 20/11/2026, thẻ `<CacCauHoi>`, `xs:key`/`xs:unique`, SHA-256, XSLT `document()`, 3 thành viên). Việc cần làm: đọc kỹ toàn bộ, đối chiếu với `TaskAssignment.md`, ghi lại các điểm còn mâu thuẫn (nếu có) rồi chốt. Commit vào repo (`Docs/ProjectBackground.md`) làm nguồn tham chiếu duy nhất.
* **Input:** `ProjectBackground.md` v2.2.
* **Output:** File đã chốt trong repo; danh sách điểm cần sửa (nếu có) gửi cả nhóm.
* **DoD:** Không còn chỗ nào mâu thuẫn giữa hai file về tên thẻ, đánh số mục, số thành viên; cả nhóm đã đọc.
* **Deadline:** Ngày 1 tuần 1.
* **Phụ thuộc:** Không.

### 🔴 T-A02: Tạo repo Git + cấu trúc thư mục dự án
* **Mô tả:** Tạo repo GitHub/GitLab private, mời Thiết + Vinh làm collaborator. Tạo cấu trúc thư mục theo Phần 7 của `ProjectBackground`:
  ```text
  ExamBank/
  ├── Data/
  ├── Schemas/
  ├── Styles/
  ├── Models/
  ├── DAL/
  ├── Helpers/
  ├── Forms/
  ├── Docs/
  ├── Program.cs
  ├── ExamBank.csproj
  └── .gitignore
  ```
* **Output:** Repo có `README.md` mô tả cấu trúc + `.gitignore` (loại `bin/`, `obj/`, `.vs/`, `*.user`).
* **DoD:** Cả 3 người clone được, push thử 1 file thành công.
* **Deadline:** Ngày 1 tuần 1.
* **Phụ thuộc:** Không.

### 🔴 T-A03: Tạo 4 file XML mẫu với dữ liệu thật
* **Mô tả:** Viết 4 file trong `Data/` theo mẫu Phần 6.1–6.4:
  * `MonHoc.xml`: $\ge 5$ môn (Lập trình Web, Lập trình C#, Cơ sở dữ liệu, Mạng máy tính, Hệ điều hành).
  * `CauHoi.xml`: $\ge 30$ câu trải đều 5 môn, mỗi môn $\ge 5$ câu, đủ 3 độ khó (1, 2, 3); mỗi môn đủ câu cho tạo đề thử (VD 5 dễ + 3 TB + 2 khó).
  * `DeThi.xml`: $\ge 3$ đề mẫu, dùng thẻ **`<CacCauHoi>`** nested; `NguoiTao` hợp lệ; **mọi câu trong đề cùng `MaMonHoc` với đề**.
  * `NguoiDung.xml`: $\ge 4$ user (1 admin, 3 giáo viên). `MatKhau` là **SHA-256 hex thường 64 ký tự** (mật khẩu thử nghiệm `123` $\rightarrow$ `a665a459…7ae3`). Ghi mật khẩu gốc của các tài khoản thử vào `README.md`.
* **Output:** 4 file XML đúng cấu trúc, dữ liệu tiếng Việt có dấu, UTF-8.
* **DoD:** Mở bằng trình duyệt không lỗi; parse bằng `XDocument.Load()` thành công.
* **Deadline:** Ngày 2 tuần 1.
* **Phụ thuộc:** T-A01.

### 🔴 T-A04: Viết 4 file XSD + test validate
* **Mô tả:** Viết 4 file trong `Schemas/`: `CauHoi.xsd`, `DeThi.xsd`, `MonHoc.xsd`, `NguoiDung.xsd` — dùng nguyên mẫu Phần 6.5–6.8 (đã có `xs:key`, `xs:unique`, kiểu mật khẩu băm); có thể siết thêm ràng buộc nếu cần.
* **Test:** Dùng VS "Validate XML" hoặc script nhỏ. 4 file XML ở T-A03 phải pass 100%. Thử các trường hợp sai, **mỗi trường hợp phải bị từ chối**:
  1. `DoKho = 4`
  2. Hai câu hỏi trùng `MaCauHoi`
  3. Cùng một đề có `MaCauHoi` lặp 2 lần
  4. `MatKhau` là mật khẩu thô (`123`) thay vì mã băm
* **Output:** 4 file XSD + ảnh chụp màn hình validate thành công và 4 ca lỗi, lưu `Docs/validate-screenshots/`.
* **DoD:** 4/4 file XML pass; 4/4 ca sai bị báo lỗi đúng.
* **Deadline:** Ngày 3 tuần 1.
* **Phụ thuộc:** T-A03.

### 🔴 T-A05: Tạo solution WinForms + Program.cs
* **Mô tả:** Tạo solution `ExamBank.sln` (WinForms, .NET Framework 4.8). Cấu hình `Program.cs` mở form `DangNhap` đầu tiên. Set Startup Object = `ExamBank.Program`. Thêm các file `Data/*.xml`, `Schemas/*.xsd`, `Styles/*.xsl` vào project và đặt **Copy to Output Directory = Copy if newer**.
* **Output:** Solution build thành công, chạy ra form trống; thư mục `bin\Debug` có đủ `Data\`, `Schemas\`, `Styles\`.
* **DoD:** `Ctrl + F5` chạy được, không warning nghiêm trọng; đường dẫn `Application.StartupPath + "\\Data\\CauHoi.xml"` mở được file.
* **Deadline:** Ngày 4 tuần 1. *(lùi lên từ tuần 2 để T-A06, T-A11 kịp tuần 2)*
* **Phụ thuộc:** T-A02.

### 🔴 T-A06: Viết Helpers/XmlHelper.cs — BLOCKER của nhóm
> ⚠️ **Cảnh báo:** Thiết và Vinh không nối DAL/form được nếu class này chưa xong.

* **Mô tả:** Viết class static `XmlHelper` trong `Helpers/` gồm các hàm:
  ```csharp
  public static class XmlHelper
  {
      public static string DataPath(string fileName);          // Application.StartupPath + "\\Data\\" + fileName
      public static string SchemaPath(string fileName);        // Application.StartupPath + "\\Schemas\\" + fileName
      public static XDocument LoadXml(string fileName);        // Load có try-catch, thông báo lỗi thân thiện
      public static void SaveXml(XDocument doc, string fileName); // Ghi an toàn (ghi file tạm rồi thay thế) + backup đơn giản
      public static bool ValidateXml(string xmlFile, string xsdFile, out List<string> errors);
      public static void BackupFile(string fileName);          // Copy sang Data/Backup/
  }
  ```
  *(Kiểm tra khóa ngoại KHÔNG nằm ở đây mà ở `ForeignKeyChecker`, T-A13.)*
* **Output:** Class hoàn chỉnh + test nhỏ trong `Docs/XmlHelper-TestCases.md` (5 case).
* **DoD:** Thiết và Vinh gọi được `XmlHelper.LoadXml("CauHoi.xml")` từ form của họ mà không lỗi; `ValidateXml` trả `false` + danh sách lỗi khi file sai.
* **Deadline:** Ngày 2 tuần 2.
* **Phụ thuộc:** T-A04, T-A05.

### 🔴 T-A11: Viết DAL/NguoiDungDAL.cs + Session + phân quyền *(đưa lên tuần 2)*
> Phải xong trước khi Vinh nộp form Đăng nhập (T-C02).

* **Mô tả:**
  ```csharp
  // Models/NguoiDung.cs, Helpers/Session.cs, Helpers/SecurityHelper.cs
  public static class Session { public static NguoiDung CurrentUser { get; set; } }
  public static string SecurityHelper.Sha256Hex(string plain);   // hex thường, 64 ký tự

  // DAL/NguoiDungDAL.cs
  public static NguoiDung Login(string username, string password);  // băm password rồi so với MatKhau
  public static List<NguoiDung> GetAll();
  public static void Insert(NguoiDung nd, string plainPassword);    // lưu mã băm
  public static void Update(NguoiDung nd);
  public static void Delete(string username);                       // chặn: user đã tạo đề; không tự xóa chính mình
  public static void ChangePassword(string username, string oldPw, string newPw);

  // Phân quyền (theo ma trận mục 2.3 của ProjectBackground)
  public static bool CanDelete(NguoiDung user);        // Admin = true
  public static bool CanManageUsers(NguoiDung user);   // Admin = true
  public static bool CanDeleteMonHoc(NguoiDung user);  // Admin = true
  ```
* **Output:** Class `NguoiDung` (POCO) + `NguoiDungDAL` + `Session` + `SecurityHelper`.
* **DoD:** `Login("admin","123")` trả về user; sai mật khẩu $\rightarrow$ `null`; `Sha256Hex("123")` = `a665a459…7ae3`; `CanDelete(GiaoVien)` = `false`, `CanDelete(Admin)` = `true`; sau `ChangePassword` file XML chứa mã băm mới và vẫn validate pass.
* **Deadline:** Ngày 4 tuần 2.
* **Phụ thuộc:** T-A06.

### 🔴 T-A07: Viết Helpers/XslHelper.cs
* **Mô tả:** Class static `XslHelper`:
  ```csharp
  public static string TransformToHtml(string xslFile, string maDeThi);
  public static void   TransformToFile(string xslFile, string maDeThi, string outputPath);
  ```
  Bên trong: `XslCompiledTransform.Load(xslPath, new XsltSettings(enableDocumentFunction: true, enableScript: false), new XmlUrlResolver())`; tạo `XsltArgumentList` với 3 tham số `maDeThi`, `cauHoiPath`, `monHocPath` (đường dẫn dạng `new Uri(...).AbsoluteUri`, lấy từ `XmlHelper.DataPath`); input là `DeThi.xml`. Mẫu code xem đầu mục 6.9 của `ProjectBackground`.
* **Output:** Class hoàn chỉnh.
* **DoD:** `TransformToHtml("DeThi.xsl", "DT001")` trả về chuỗi HTML có **nội dung câu hỏi và tên môn** (không chỉ mã), gán vào `WebBrowser.DocumentText` hiển thị đẹp; truyền mã đề không tồn tại không làm chương trình crash.
* **Deadline:** Ngày 5 tuần 2.
* **Phụ thuộc:** T-A05, T-A06. Phối hợp với Thiết (T-B03) để test cùng lúc.

### 🔴 T-A08: Viết DAL/MonHocDAL.cs
* **Mô tả:** CRUD môn học dùng LINQ to XML:
  ```csharp
  public static List<MonHoc> GetAll();
  public static MonHoc GetById(string maMonHoc);
  public static void Insert(MonHoc mh);   // Validate + Save
  public static void Update(MonHoc mh);
  public static void Delete(string maMonHoc); // Chặn khi còn câu hỏi hoặc đề thi thuộc môn đó (mục 6.10)
  public static bool Exists(string maMonHoc);
  ```
* **Output:** Class `MonHoc` (POCO, đặt trong `Models/`) + `MonHocDAL` hoàn chỉnh.
* **DoD:** `Insert` $\rightarrow$ `MonHoc.xml` có thêm mục; `Delete` môn đang có câu hỏi $\rightarrow$ throw exception có message rõ; mã trùng $\rightarrow$ báo lỗi, không ghi file.
* **Deadline:** Ngày 1 tuần 3.
* **Phụ thuộc:** T-A06.

### 🔴 T-A09: Viết DAL/CauHoiDAL.cs
* **Mô tả:** Tương tự T-A08 nhưng cho câu hỏi, thêm hàm. **Truy vấn theo môn / độ khó dùng XPath** (`XPathSelectElements`); **tìm từ khóa dùng LINQ** (không ghép từ khóa người dùng vào XPath):
  ```csharp
  public static List<CauHoi> GetByMonHoc(string maMonHoc);                 // XPath
  public static List<CauHoi> GetByDoKho(string maMonHoc, int doKho);       // XPath
  public static List<CauHoi> Search(string keyword, string maMonHoc = null); // LINQ, không phân biệt hoa thường
  public static int CountByMonHoc(string maMonHoc, int doKho);            // XPath count
  ```
  `Delete` chặn khi câu hỏi đang nằm trong một đề thi; `Update` chặn đổi `MaMonHoc` khi câu đang nằm trong đề.
* **Output:** Class `CauHoi` (POCO) + `CauHoiDAL` hoàn chỉnh.
* **DoD:** `GetByDoKho("MH001", 2)` đúng danh sách; `Search("css")` tìm được câu có `"CSS"`; từ khóa có dấu nháy (`it's`) không gây lỗi; xóa câu đang dùng trong đề $\rightarrow$ báo lỗi rõ.
* **Deadline:** Ngày 2 tuần 3.
* **Phụ thuộc:** T-A06, T-A08.

### 🔴 T-A10: Viết DAL/DeThiDAL.cs — TASK KHÓ NHẤT
> ⚠️ **Lưu ý:** Dành 2–3 ngày riêng cho task này. Đây là chức năng cốt lõi của đồ án.

* **Mô tả:** Class `DeThiDAL`:
  ```csharp
  public static List<DeThi> GetAll();
  public static DeThi GetById(string maDeThi);
  public static void Insert(DeThi dt);
  public static void Update(DeThi dt);
  public static void Delete(string maDeThi);

  // Hàm đặc biệt: tạo đề tự động
  public static DeThi TaoDeThi(
      string maMonHoc,
      string tenDeThi,
      int thoiGianLamBai,
      int soCauDe,
      int soCauTrungBinh,
      int soCauKho,
      string nguoiTao);
  ```
* **Logic `TaoDeThi`:**
  1. Kiểm tra môn tồn tại; tổng số câu yêu cầu $\ge 1$.
  2. Kiểm tra đủ câu mỗi độ khó (`CountByMonHoc` $\ge$ số yêu cầu) — nếu thiếu $\rightarrow$ throw exception `"Môn X chỉ có Y câu độ khó Z, cần W câu"`.
  3. Bốc ngẫu nhiên trong từng độ khó (`OrderBy(x => Guid.NewGuid()).Take(n)`); thứ tự trong đề: Dễ $\rightarrow$ Trung bình $\rightarrow$ Khó.
  4. Tạo mã đề mới (`DT001`, `DT002`… tự tăng); **nếu vượt `DT999` thì báo lỗi rõ ràng**.
  5. Gán `NguoiTao = nguoiTao` (lấy từ `Session.CurrentUser`, không cho nhập tay).
  6. Ghi nested `<CacCauHoi>` (mỗi câu một `<MaCauHoi>`; thứ tự xuất hiện = `ThuTu`) vào `DeThi.xml`.
  7. Validate XSD trước khi save $\rightarrow$ nếu fail thì rollback (không save).
* **Output:** Class `DeThi` (POCO) + `DeThiDAL` + 5 test case trong `Docs/TaoDeThi-TestCases.md`.
* **DoD:** Tạo đề 5 dễ + 3 TB + 2 khó $\rightarrow$ đúng 10 câu, đúng độ khó, cùng môn, không lặp câu, `NguoiTao` = user đang đăng nhập, `DeThi.xml` validate pass; yêu cầu thiếu câu $\rightarrow$ báo lỗi và file không đổi.
* **Deadline:** Ngày 5 tuần 3 (deadline mềm: cuối tuần 3).
* **Phụ thuộc:** T-A09, T-A11.

### 🔴 T-A12: Hoàn thiện ValidateXml() — trả về lỗi chi tiết
* **Mô tả:** Nâng cấp hàm từ T-A06: trả danh sách lỗi chi tiết (dòng, cột, message). Định dạng: `List<ValidationError>` với `LineNumber`, `LinePosition`, `Message`, `Severity`. Giữ lớp bao `ValidateXml(..., out List<string>)` để code cũ không vỡ.
* **Output:** Hàm `ValidateXml` phiên bản 2 + class `ValidationError`.
* **DoD:** Cố tình sửa `DoKho = 4` $\rightarrow$ lỗi `"Line X, Column Y: …DoKho…"`; trùng `MaCauHoi` $\rightarrow$ lỗi nêu đúng khóa `pkCauHoi` bị vi phạm.
* **Deadline:** Ngày 1 tuần 5.
* **Phụ thuộc:** T-A06.

### 🔴 T-A13: Viết Helpers/ForeignKeyChecker.cs
* **Mô tả:** Class kiểm tra FK giữa các file (5 quy tắc ở mục 6.10 của `ProjectBackground`):
  ```csharp
  public static List<string> CheckAll();
  // 1. CauHoi.MaMonHoc có trong MonHoc.xml?
  // 2. DeThi.MaMonHoc có trong MonHoc.xml?
  // 3. DeThi.NguoiTao có trong NguoiDung.xml?
  // 4. Mỗi DeThi/CacCauHoi/MaCauHoi có trong CauHoi.xml?
  // 5. Câu hỏi trong đề có cùng MaMonHoc với đề?
  ```
* **Output:** Class hoàn chỉnh; hàm trả list lỗi FK (rỗng nếu OK).
* **DoD:** Xóa 1 môn trong `MonHoc.xml` bằng tay $\rightarrow$ `CheckAll()` trả `"CauHoi CH001 tham chiếu MH999 không tồn tại"`; đưa 1 câu môn khác vào đề $\rightarrow$ báo lỗi quy tắc 5.
* **Deadline:** Ngày 2 tuần 5.
* **Phụ thuộc:** T-A04, T-A06.

### 🔴 T-A14: Tích hợp validation vào lớp DAL
* **Mô tả:** Đặt `ValidateXml` + `ForeignKeyChecker.CheckAll()` **trong lớp DAL** (một chỗ duy nhất) để mọi form được hưởng:
  1. Khi load dữ liệu: file XML lỗi $\rightarrow$ DAL ném exception có thông điệp rõ.
  2. Trước khi ghi: validate bản XML mới; fail $\rightarrow$ không ghi (rollback).
  Form chỉ cần bắt exception và hiện `MessageBox` — Tài hướng dẫn Thiết và Vinh đoạn `try-catch` mẫu (copy-paste), không sửa logic từng form.
* **Output:** Sửa `MonHocDAL`, `CauHoiDAL`, `DeThiDAL`, `NguoiDungDAL`; đoạn mã mẫu `try-catch` cho form.
* **DoD:** Cố tình làm hỏng `CauHoi.xml` $\rightarrow$ mở form QL Câu hỏi báo lỗi rõ, không crash, không ghi đè file hỏng.
* **Deadline:** Ngày 4 tuần 5.
* **Phụ thuộc:** T-A12, T-A13.

### 🔴 T-A15: Xuất PDF đề thi (tùy chọn)
* **Mô tả:** Dùng `iTextSharp` hoặc `PdfSharp` (NuGet) xuất đề thi ra PDF, 2 chế độ có/không đáp án. Sau khi xong, **gắn vào nút "Xuất PDF" (đang bị vô hiệu) trong `XemDeThi.cs`** cùng Thiết.
* **Output:** Hàm `PdfExporter.Export(DeThi dt, string outputPath, bool showAnswer)`.
* **DoD:** Bấm "Xuất PDF" trong form Xem đề $\rightarrow$ mở file PDF đúng nội dung, đúng tiếng Việt có dấu.
* **Deadline:** Ngày 3 tuần 6.
* **Phụ thuộc:** T-A10, T-B06.

### 🔴 T-A16: Audit log — ghi lại mọi thao tác CRUD (tùy chọn)
* **Mô tả:** Tạo `Data/Log.xml` + `Schemas/Log.xsd` (nhỏ) + class `AuditLogger`:
  ```csharp
  public static void Log(string action, string target, string detail); // username lấy từ Session.CurrentUser
  // VD: Log("CREATE", "CauHoi", "Thêm câu CH031")
  ```
  Gọi trong `Insert`/`Update`/`Delete` của DAL.
* **Output:** `Log.xml`, `Log.xsd`, `AuditLogger`.
* **DoD:** Thêm 1 câu hỏi $\rightarrow$ `Log.xml` có dòng mới với timestamp, user, action; `Log.xml` validate pass.
* **Deadline:** Ngày 4 tuần 6.
* **Phụ thuộc:** T-A08, T-A09, T-A10, T-A11.

### 🔴 T-A17: Backup tự động trước khi ghi (tùy chọn)
* **Mô tả:** Trong `XmlHelper.SaveXml`, trước khi ghi đè file gốc $\rightarrow$ copy bản cũ sang `Data/Backup/{filename}_{yyyyMMdd_HHmmss}.xml`. Giữ tối đa 20 bản gần nhất (xóa bản cũ khi vượt).
* **Output:** Sửa `XmlHelper.SaveXml`.
* **DoD:** Ghi file 3 lần $\rightarrow$ `Data/Backup/` có 3 file backup; ghi trên 20 lần $\rightarrow$ chỉ còn 20 bản mới nhất.
* **Deadline:** Ngày 5 tuần 6.
* **Phụ thuộc:** T-A06.

### 🔴 T-A18: Viết Chương 1 + Chương 2 (Khảo sát, Phân tích, Thiết kế CSDL XML) — chia 2 mốc
* **Mô tả:** Viết trong `BaoCao.docx`:
  * **Chương 1:** Giới thiệu (ích lợi XML, mục tiêu, phạm vi).
  * **Chương 2 phần 1:** Khảo sát nghiệp vụ (từ `ProjectBackground` Phần 2).
  * **Chương 2 phần 2:** Phân tích thiết kế (mô hình phân cấp, DFD, ERD, thực thể; giải thích `ChiTietDeThi` logic $\rightarrow$ nested).
  * **Chương 2 phần 3 (KHÓ NHẤT):** Thiết kế CSDL XML — 4 file XML mẫu, 4 file XSD, giải thích `xs:key`/`xs:unique`, giới hạn của XSD 1.0 và cách bù bằng `ForeignKeyChecker`; nêu hạn chế SHA-256 chưa có salt.
* **Mốc 1 — cuối tuần 4 (ngày 5):** bản nháp Chương 2 phần 1–3 (lúc XML/XSD vừa làm xong, còn nhớ rõ).
* **Mốc 2 — tuần 7 ngày 4:** hoàn chỉnh + viết Chương 1, thêm ảnh sơ đồ từ `Docs/`.
* **Output:** Phần Chương 1 + Chương 2 trong `BaoCao.docx` (khoảng 25–30 trang).
* **DoD:** Đọc mạch lạc, có ảnh sơ đồ, bảng thực thể, code XML/XSD trình bày đẹp.
* **Deadline:** Mốc 1: ngày 5 tuần 4. Mốc 2: ngày 4 tuần 7.
* **Phụ thuộc:** T-A04 (mốc 1); các task còn lại (mốc 2).

---

## 3. TASK CỦA THIẾT

### 🟡 T-B01: Render Mermaid + DBML thành ảnh
* **Mô tả:** Vào `mermaid.live` render code Phần 5.1 $\rightarrow$ `so-do-phan-cap.png`. Vào `dbdiagram.io` render code Phần 4.2 $\rightarrow$ `erd.png`. Lưu vào `Docs/`.
* **Output:** 2 file ảnh PNG chất lượng cao.
* **DoD:** Ảnh rõ nét, chữ đọc được, không bị cắt; ERD có đủ 5 bảng (kể cả `ChiTietDeThi`).
* **Deadline:** Ngày 2 tuần 1.
* **Phụ thuộc:** Không.

### 🟡 T-B02: Vẽ DFD mức khung cảnh + mức đỉnh
* **Mô tả:** Dùng `draw.io` vẽ:
  * **Context Diagram:** ExamBank $\leftrightarrow$ Giáo viên, Admin.
  * **Level 0:** 4 process (Quản lý môn, Quản lý câu hỏi, Quản lý đề, Xem đề) + 4 data store (`MonHoc.xml`, `CauHoi.xml`, `DeThi.xml`, `NguoiDung.xml`).
* **Output:** 2 file ảnh PNG trong `Docs/`.
* **DoD:** Đúng ký hiệu DFD (hình tròn = process, 2 gạch = data store, mũi tên = luồng).
* **Deadline:** Ngày 4 tuần 1.
* **Phụ thuộc:** Không.

### 🟡 T-B03: Viết Styles/DeThi.xsl — bản hiển thị
* **Mô tả:** Xuất phát từ mẫu Phần 6.9, hoàn thiện XSLT biến `DeThi.xml` $\rightarrow$ HTML đẹp:
  * **Header:** tên đề, **tên môn (lấy từ `MonHoc.xml` bằng `document()`)**, thời gian, số câu, người tạo, ngày tạo.
  * **Body:** đánh số câu $1..n$ theo thứ tự `<MaCauHoi>`, **nội dung câu hỏi và đáp án lấy từ `CauHoi.xml`**; có hiển thị đáp án đúng (cho giáo viên).
  * Có tham số `maDeThi`, `cauHoiPath`, `monHocPath`; mã câu không tồn tại thì hiện cảnh báo thay vì lỗi.
  * **CSS:** font Times New Roman, border, padding.
* **Output:** File `Styles/DeThi.xsl`.
* **DoD:** Chạy qua `XslHelper` (hoặc thử bằng `XslCompiledTransform` trong form tạm) $\rightarrow$ hiển thị đúng nội dung câu hỏi, không chỉ mã; nếu muốn xem bằng trình duyệt: mở qua Firefox hoặc trình duyệt cho phép `document()` với `file://`.
* **Deadline:** Ngày 3 tuần 2.
* **Phụ thuộc:** T-A03.

### 🟡 T-B04: Viết Styles/DeThi_Print.xsl — bản in
* **Mô tả:** Giống T-B03 nhưng:
  * Ẩn đáp án đúng.
  * Có dòng `"Họ tên thí sinh: ................ SBD: ..........."` ở đầu.
  * Có footer `"Trang X/Y"` (qua CSS in).
  * CSS tối ưu cho in A4 (`@media print`).
* **Output:** File `Styles/DeThi_Print.xsl`.
* **DoD:** In ra PDF từ trình duyệt $\rightarrow$ đúng 1 trang A4 cho đề 10 câu, không bị cắt, không lộ đáp án.
* **Deadline:** Ngày 4 tuần 2.
* **Phụ thuộc:** T-B03.

### 🟡 T-B05: Code form Forms/TaoDeThi.cs
* **Mô tả:** Form tạo đề thi:
  * `ComboBox` chọn môn (load từ `MonHocDAL.GetAll()`).
  * `TextBox` tên đề, `NumericUpDown` thời gian.
  * 3 `NumericUpDown`: số câu dễ / TB / khó; hiển thị số câu hiện có của mỗi độ khó khi chọn môn (`CauHoiDAL.CountByMonHoc`).
  * Nút "Tạo" $\rightarrow$ gọi `DeThiDAL.TaoDeThi(...)` với `nguoiTao = Session.CurrentUser.TenDangNhap`.
  * Hiển thị `MessageBox` kết quả / lỗi (bắt exception thiếu câu).
* **Cách làm:** Dựng giao diện từ tuần 3 bằng dữ liệu giả; nối `DeThiDAL` thật ngay khi T-A10 xong.
* **Output:** `Forms/TaoDeThi.cs` + `.Designer.cs`.
* **DoD:** Chọn môn + nhập số câu $\rightarrow$ bấm Tạo $\rightarrow$ `DeThi.xml` có đề mới đúng yêu cầu, `NguoiTao` đúng.
* **Deadline:** Ngày 2 tuần 4.
* **Phụ thuộc:** T-A10.

### 🟡 T-B06: Code form Forms/XemDeThi.cs
* **Mô tả:** Form xem đề:
  * `ListBox` bên trái: danh sách đề (`DeThiDAL.GetAll()`).
  * `WebBrowser` bên phải: hiển thị đề đã chọn qua `XslHelper.TransformToHtml("DeThi.xsl", maDeThi)`.
  * Nút "Xem bản in" (dùng `DeThi_Print.xsl`).
  * Nút "Xuất HTML" (gọi hàm `XuatHtml()` ở T-B08).
  * Nút "Xuất PDF": **để sẵn nhưng vô hiệu hóa (`Enabled = false`)**, T-A15 sẽ kích hoạt.
  * Nút "Xóa đề": chỉ Admin (Vinh gắn phân quyền ở T-C07).
* **Output:** `Forms/XemDeThi.cs` + `.Designer.cs`.
* **DoD:** Chọn đề $\rightarrow$ hiển thị đúng nội dung và đẹp; "Xem bản in" không có đáp án đúng.
* **Deadline:** Ngày 4 tuần 4.
* **Phụ thuộc:** T-A07, T-B03, T-B04.

### 🟡 T-B07: Nâng cấp XSLT — CSS đẹp + responsive
* **Mô tả:** Cải thiện `DeThi.xsl` + `DeThi_Print.xsl`:
  * Thêm logo trường (ảnh base64 hoặc URL).
  * Font đẹp (Google Fonts — kiểm tra hiển thị khi không có mạng, có font dự phòng).
  * Màu sắc hài hòa (xanh dương + trắng).
  * Responsive (`@media` cho mobile).
* **Output:** 2 file XSL cập nhật.
* **DoD:** Xuất HTML mở trên Chrome + Edge + giả lập mobile (F12) đều đẹp; vẫn hiển thị đúng trong `WebBrowser` của WinForms.
* **Deadline:** Ngày 3 tuần 5.
* **Phụ thuộc:** T-B03, T-B04.

### 🟡 T-B08: Viết hàm XuatHtml() trong XemDeThi.cs
* **Mô tả:** `SaveFileDialog` (filter `.html`) $\rightarrow$ gọi `XslHelper.TransformToFile()` $\rightarrow$ sau khi lưu, hỏi `"Mở file?"` $\rightarrow$ Yes thì `Process.Start(path)`. File HTML xuất ra phải **độc lập** (đã nhúng nội dung câu hỏi; không còn phụ thuộc `CauHoi.xml`).
* **Output:** Hàm hoàn chỉnh trong form.
* **DoD:** Bấm nút $\rightarrow$ chọn nơi lưu $\rightarrow$ file HTML mở bằng trình duyệt hiển thị đúng khi copy sang máy khác.
* **Deadline:** Ngày 4 tuần 5.
* **Phụ thuộc:** T-A07, T-B06.

### 🟡 T-B09: Code form Forms/DoiMatKhau.cs
* **Mô tả:** Form đổi mật khẩu:
  * `TextBox` mật khẩu cũ, mới, xác nhận (`UseSystemPasswordChar = true`).
  * Validate: mật khẩu cũ đúng, mật khẩu mới $\ge 3$ ký tự, xác nhận khớp.
  * Gọi `NguoiDungDAL.ChangePassword()` (DAL tự băm SHA-256).
* **Output:** `Forms/DoiMatKhau.cs` + `.Designer.cs`.
* **DoD:** Đổi thành công $\rightarrow$ đăng nhập lại bằng mật khẩu mới OK; sai mật khẩu cũ $\rightarrow$ báo lỗi; `NguoiDung.xml` vẫn validate pass.
* **Deadline:** Ngày 3 tuần 6.
* **Phụ thuộc:** T-A11.

### 🟡 T-B10: Code form Forms/ThongKe.cs
* **Mô tả:** Form thống kê:
  * `DataGridView 1`: số câu theo môn (LINQ `GroupBy`).
  * `DataGridView 2`: số câu theo độ khó từng môn.
  * `DataGridView 3`: số đề theo môn.
  * `Label` tổng: tổng số câu, tổng số đề, tổng số user.
* **Output:** `Forms/ThongKe.cs` + `.Designer.cs`.
* **DoD:** Số liệu khớp với file XML thực tế.
* **Deadline:** Ngày 4 tuần 6.
* **Phụ thuộc:** T-A08, T-A09, T-A10.

### 🟡 T-B11: Viết Chương 2 phần XSLT trong báo cáo — chia 2 mốc
* **Mô tả:** Viết mục "Thiết kế XSLT" trong `BaoCao.docx`:
  * Giải thích XSLT là gì, tại sao dùng.
  * Trình bày `DeThi.xsl` (rút gọn) + giải thích từng template; **nhấn mạnh `document()`, `xsl:key`, `xsl:param`** (vì `DeThi.xml` chỉ chứa mã, phải ghép từ `CauHoi.xml` và `MonHoc.xml`).
  * Ảnh chụp kết quả hiển thị (từ `WebBrowser` và từ file HTML đã xuất).
  * So sánh bản thường vs bản in.
* **Mốc 1 — cuối tuần 5 (ngày 5):** bản nháp (nội dung + code + ảnh bản thường).
* **Mốc 2 — tuần 7 ngày 3:** hoàn chỉnh (thêm bản in, ảnh cuối sau khi CSS xong).
* **Output:** Phần XSLT trong báo cáo (~8–10 trang).
* **DoD:** Có code + ảnh + giải thích mạch lạc.
* **Deadline:** Mốc 1: ngày 5 tuần 5. Mốc 2: ngày 3 tuần 7.
* **Phụ thuộc:** T-B03, T-B04 (mốc 1); T-B07 (mốc 2).

---

## 4. TASK CỦA VINH

### 🟢 T-C01: Vẽ wireframe 5 form
* **Mô tả:** Dùng Figma/draw.io/Balsamiq vẽ phác thảo 5 form:
  1. **Đăng nhập:** username, password, nút Đăng nhập, nút Thoát.
  2. **Main:** menu trái, header phải có tên user + quyền, vùng content.
  3. **QL Câu hỏi:** `DataGridView` + 4 `TextBox` + 2 `ComboBox` + 4 `RadioButton` + 4 nút CRUD.
  4. **Tạo đề thi:** `ComboBox` môn + 3 `NumericUpDown` + nút Tạo.
  5. **Xem đề thi:** `ListBox` trái + `WebBrowser` phải + các nút (bản in, xuất HTML, xuất PDF, xóa đề).
* **Output:** 5 file ảnh PNG trong `Docs/Wireframes/`.
* **DoD:** Mỗi form có chú thích control (label, textbox, button...).
* **Deadline:** Ngày 4 tuần 1.
* **Phụ thuộc:** Không.

### 🟢 T-C02: Code form Forms/DangNhap.cs
* **Mô tả:** Form đăng nhập:
  * 2 `TextBox` (username, password — `UseSystemPasswordChar = true`).
  * Nút Đăng nhập $\rightarrow$ gọi `NguoiDungDAL.Login()` $\rightarrow$ nếu OK gán `Session.CurrentUser`, mở `Main`, ẩn form đăng nhập.
  * Nếu sai $\rightarrow$ `MessageBox` lỗi.
  * Nút Thoát $\rightarrow$ `Application.Exit()`.
  * Dựng giao diện từ đầu tuần 2; nối `Login()` thật khi T-A11 báo xong (ngày 4).
* **Output:** `Forms/DangNhap.cs` + `.Designer.cs`.
* **DoD:** Đăng nhập đúng (`admin` / `123`) $\rightarrow$ mở `Main`; sai $\rightarrow$ báo lỗi; Enter ở ô mật khẩu $\rightarrow$ trigger nút Đăng nhập.
* **Deadline:** Ngày 5 tuần 2.
* **Phụ thuộc:** T-A05, T-A11.

### 🟢 T-C03: Code form Forms/Main.cs
* **Mô tả:** Form chính:
  * **Header:** `"Exam Bank — Xin chào, {HoTen} ({Quyen})"`.
  * **Menu trái:** 6 nút (QL Môn, QL Câu hỏi, Tạo đề, Xem đề, Thống kê, Đổi mật khẩu) + nút Đăng xuất. Các form chưa có thì mở form tạm báo "Đang phát triển".
  * **Vùng content:** `Panel` chứa form con (`TopLevel = false`).
  * **Phân quyền UI:** nút "QL Người dùng" (nếu có) chỉ hiện với Admin.
* **Output:** `Forms/Main.cs` + `.Designer.cs`.
* **DoD:** Click menu $\rightarrow$ form con hiển thị trong panel; đăng xuất $\rightarrow$ xóa `Session.CurrentUser` và quay về `DangNhap`.
* **Deadline:** Ngày 2 tuần 3.
* **Phụ thuộc:** T-C02.

### 🟢 T-C04: Code form Forms/QLMonHoc.cs
* **Mô tả:** Form CRUD môn học:
  * `DataGridView` load `MonHocDAL.GetAll()`.
  * 3 `TextBox` (Mã, Tên, Mô tả).
  * 4 nút: Thêm, Sửa, Xóa, Làm mới.
  * Click row $\rightarrow$ đổ dữ liệu lên `TextBox`.
  * Validate input trước khi gọi DAL (mã pattern `MH\d{3}`, tên không rỗng $\le$ 100 ký tự, mô tả $\le$ 255 ký tự).
  * Bắt exception từ DAL (mã trùng, xóa môn còn câu hỏi) và hiện `MessageBox`.
* **Output:** `Forms/QLMonHoc.cs` + `.Designer.cs`.
* **DoD:** Thêm môn mới $\rightarrow$ `DataGridView` cập nhật + `MonHoc.xml` có mục mới; xóa môn đang có câu hỏi $\rightarrow$ báo lỗi.
* **Deadline:** Ngày 4 tuần 3.
* **Phụ thuộc:** T-A08.

### 🟢 T-C05: Code form Forms/QLCauHoi.cs
* **Mô tả:** Form CRUD câu hỏi (phức tạp nhất của Vinh):
  * `DataGridView` load `CauHoiDAL.GetAll()`.
  * 9 control nhập: Mã, Nội dung (multiline), 4 đáp án, 4 `RadioButton` đáp án đúng, `ComboBox` độ khó, `ComboBox` môn.
  * 4 nút CRUD + nút Làm mới.
  * Click row $\rightarrow$ đổ dữ liệu + check `RadioButton` đúng.
  * Validate: đủ 4 đáp án (không rỗng, $\le$ 255 ký tự), nội dung $\le$ 500 ký tự, có 1 đáp án đúng, độ khó và môn đã chọn.
  * Bắt exception DAL (xóa/đổi môn câu hỏi đang nằm trong đề) và hiện `MessageBox`.
* **Output:** `Forms/QLCauHoi.cs` + `.Designer.cs`.
* **DoD:** Thêm câu hỏi $\rightarrow$ file XML có câu mới đúng cấu trúc, validate pass; sửa đáp án đúng $\rightarrow$ radio cập nhật đúng.
* **Deadline:** Ngày 5 tuần 3 (deadline mềm: ngày 2 tuần 4).
* **Phụ thuộc:** T-A09.

### 🟢 T-C06: Thêm tìm kiếm vào QLCauHoi.cs
* **Mô tả:** Thêm `TextBox` tìm kiếm + `ComboBox` lọc môn + nút Tìm:
  * Tìm theo nội dung (gọi `CauHoiDAL.Search`).
  * Lọc theo môn (gọi `CauHoiDAL.GetByMonHoc`).
  * Kết hợp cả 2.
* **Output:** Sửa `QLCauHoi.cs`.
* **DoD:** Gõ `"css"` $\rightarrow$ `DataGridView` chỉ hiện câu có `"CSS"`; chọn môn `"Lập trình Web"` $\rightarrow$ chỉ hiện câu môn đó; kết hợp cả hai đúng.
* **Deadline:** Ngày 3 tuần 5.
* **Phụ thuộc:** T-A09, T-C05.

### 🟢 T-C07: Phân quyền UI
* **Mô tả:** Áp dụng `NguoiDungDAL.CanDelete()` theo ma trận phân quyền (mục 2.3 `ProjectBackground`):
  * Form QL Môn: ẩn nút Xóa nếu không phải Admin.
  * Form QL Câu hỏi: ẩn nút Xóa nếu không phải Admin.
  * Form Xem đề: ẩn nút Xóa đề nếu không phải Admin.
  * *(Tùy chọn, làm nếu còn thời gian, không tính vào DoD)* Form QL Người dùng đơn giản (`DataGridView` + thêm/sửa/xóa qua `NguoiDungDAL`), chỉ Admin mở được.
* **Output:** Sửa 3 form (+ 1 form tùy chọn).
* **DoD:** Đăng nhập bằng `gv01` $\rightarrow$ không thấy nút Xóa ở 3 form; đăng nhập `admin` $\rightarrow$ thấy đầy đủ; gọi thẳng DAL với quyền Giáo viên cũng không xóa được (DAL kiểm tra lại quyền).
* **Deadline:** Ngày 4 tuần 5.
* **Phụ thuộc:** T-A11, T-B06.

### 🟢 T-C08: Polish UI toàn bộ
* **Mô tả:** Cải thiện giao diện:
  * Icon cho các nút (Font Awesome hoặc ảnh PNG).
  * Màu sắc hài hòa (xanh dương chủ đạo).
  * Tooltip cho các nút.
  * Căn lề, font Segoe UI 10pt.
  * (Tùy chọn) Guna UI nếu có license.
* **Output:** Sửa tất cả `.Designer.cs`.
* **DoD:** Nhìn chuyên nghiệp, không còn form "trắng bóc".
* **Deadline:** Ngày 4 tuần 6.
* **Phụ thuộc:** T-C02 $\rightarrow$ T-C07.

### 🟢 T-C09: Viết 20 test case
* **Mô tả:** Viết `Docs/TestCases.md` gồm 20 test case:
  * Đăng nhập đúng/sai.
  * Thêm/sửa/xóa môn (kể cả xóa môn đang có câu hỏi).
  * Thêm/sửa/xóa câu hỏi (kể cả thiếu đáp án, xóa câu đang nằm trong đề).
  * Tạo đề thiếu câu (VD: môn chỉ có 2 câu dễ nhưng yêu cầu 5).
  * Xem đề, xuất HTML, xuất PDF (nếu làm).
  * Validate XML hỏng (trùng mã, `DoKho = 4`) và FK hỏng (câu hỏi tham chiếu môn không tồn tại).
  * Phân quyền (Giáo viên không xóa được).
* **Output:** `Docs/TestCases.md` với format: `ID | Mô tả | Bước | Kết quả mong đợi | Kết quả thực tế | Pass/Fail`.
* **DoD:** Đủ 20 case, có ít nhất 5 case "âm" (mong đợi lỗi).
* **Deadline:** Ngày 5 tuần 6.
* **Phụ thuộc:** Tất cả task code.

### 🟢 T-C10: Viết Chương 3 (Cài đặt) trong báo cáo — chia 2 mốc
* **Mô tả:** Viết mục "Cài đặt chương trình" trong `BaoCao.docx`:
  * Ảnh chụp tất cả form (Đăng nhập, Main, QL Môn, QL Câu hỏi, Tạo đề, Xem đề, Thống kê, Đổi mật khẩu).
  * Mô tả chức năng từng form.
  * Mô tả luồng thao tác mẫu (VD: `"Để tạo đề: bước 1... bước 2..."`).
  * Ảnh chụp kết quả xuất HTML (+ PDF nếu làm).
* **Mốc 1 — cuối tuần 5 (ngày 5):** viết phần mô tả chức năng + luồng thao tác cho các form đã xong (Đăng nhập, Main, QL Môn, QL Câu hỏi, Tạo đề, Xem đề).
* **Mốc 2 — tuần 7 ngày 4:** chụp lại ảnh sau khi polish UI (T-C08), bổ sung Thống kê, Đổi mật khẩu, xuất file.
* **Output:** Phần Cài đặt trong báo cáo (~12–15 trang).
* **DoD:** Ảnh rõ nét, có chú thích từng control.
* **Deadline:** Mốc 1: ngày 5 tuần 5. Mốc 2: ngày 4 tuần 7.
* **Phụ thuộc:** T-C05 (mốc 1); tất cả task code (mốc 2).

---

## 5. TASK CHUNG (CẢ 3 NGƯỜI)

### 🔵 T-D01: Họp kickoff (tuần 1)
* **Mô tả:** Họp 1 buổi online/offline:
  * Review `ProjectBackground.md` v2.2.
  * Chốt phân công (file này).
  * Thống nhất quy ước code (mục 7).
  * Tạo group chat + kênh liên lạc.
* **Output:** Biên bản họp ngắn trong `Docs/MeetingNotes/`.
* **Deadline:** Ngày 1 tuần 1.

### 🔵 T-D02: Họp review cuối tuần 1
* **Mô tả:** Review sản phẩm tuần 1: 4 XML, 4 XSD (có ca test sai), solution, ảnh sơ đồ, DFD, 5 wireframe.
* **Output:** Feedback + danh sách việc cần sửa.
* **Deadline:** Cuối tuần 1.

### 🔵 T-D03: Test tích hợp cuối tuần 2
* **Mô tả:** Cả 3 ngồi cùng test:
  * Đăng nhập (`admin`/`123`) $\rightarrow$ mở `Main`.
  * Hiển thị đề mẫu qua `WebBrowser` bằng `XslHelper` (dùng form thử tạm của Thiết, vì `XemDeThi.cs` chính làm ở tuần 4): kiểm tra thấy nội dung câu hỏi và tên môn.
  * Validate XML (file đúng và file cố tình hỏng).
* **Output:** Danh sách bug + assign người fix.
* **Deadline:** Cuối tuần 2.

### 🔵 T-D04: Test CRUD end-to-end cuối tuần 4
* **Mô tả:** Test toàn bộ luồng: thêm môn $\rightarrow$ thêm câu $\rightarrow$ tạo đề $\rightarrow$ xem đề $\rightarrow$ sửa $\rightarrow$ xóa.
* **Output:** Danh sách bug + assign.
* **Deadline:** Cuối tuần 4.

### 🔵 T-D05: Test validation + phân quyền cuối tuần 5
* **Mô tả:** Test các case "âm": XML hỏng, thiếu FK, câu hỏi khác môn trong đề, Giáo viên xóa môn/câu hỏi/đề.
* **Output:** Danh sách bug + assign.
* **Deadline:** Cuối tuần 5.

### 🔵 T-D06: Fix bug + test trên máy khác cuối tuần 6
* **Mô tả:** Cả 3 fix bug còn lại. Sau đó copy thư mục dự án sang máy khác (hoặc máy ảo), giải nén, chạy thử $\rightarrow$ phải chạy được không lỗi (kiểm tra *Copy to Output Directory* cho `Data/`, `Schemas/`, `Styles/`).
* **Output:** Bản build final chạy được trên máy sạch.
* **Deadline:** Cuối tuần 6.

### 🔵 T-D07: Viết Kết luận + Hướng phát triển
* **Mô tả:** Mỗi người viết 1 đoạn (~$\frac{1}{2}$ trang):
  * **Tài:** tổng kết kỹ thuật (XML, XSD, LINQ to XML, XPath).
  * **Thiết:** tổng kết XSLT + hiển thị.
  * **Vinh:** tổng kết UI + trải nghiệm người dùng.
  * Tài gộp + viết phần "Hướng phát triển" (chấm điểm tự động, quản lý lớp học, mobile app, băm mật khẩu có salt, mở rộng mã vượt 999…).
* **Output:** Phần Kết luận trong `BaoCao.docx`.
* **Deadline:** Ngày 5 tuần 7.

### 🔵 T-D08: Review báo cáo + đóng gói + nộp
* **Mô tả:** Tài review toàn bộ `BaoCao.docx` (format, chính tả, ảnh). Cả 3 kiểm tra Checklist nghiệm thu (mục 8). Đóng gói `.zip` theo cấu trúc (các thư mục `Data/`, `Schemas/`, `Styles/` ở ngoài là bản sao để người chấm dễ xem; bản chạy được nằm trong `SourceCode/`):
  ```text
  Nhom_X_ExamBank.zip
  ├── SourceCode/        (toàn bộ solution, đã xóa bin/obj)
  ├── Data/             (4 file XML)
  ├── Schemas/          (4 file XSD)
  ├── Styles/           (2 file XSL)
  ├── Docs/             (sơ đồ, wireframe, test case)
  └── BaoCao.docx
  ```
* **Output:** File `.zip` hoàn chỉnh.
* **Deadline:** Cuối tuần 7.

---

## 6. TIMELINE & DEADLINE

| Tuần | Tài | Thiết | Vinh | Task chung |
| :---: | :--- | :--- | :--- | :--- |
| **1** | T-A01 $\rightarrow$ T-A05 | T-B01, T-B02 | T-C01 | T-D01, T-D02 |
| **2** | T-A06, T-A11, T-A07 | T-B03, T-B04 | T-C02 | T-D03 |
| **3** | T-A08 $\rightarrow$ T-A10 | T-B05 (dựng UI) | T-C03, T-C04, T-C05 | — |
| **4** | T-A18 (mốc 1: nháp Chương 2) | T-B05 (nối DAL), T-B06 | T-C05 (hoàn tất) | T-D04 |
| **5** | T-A12 $\rightarrow$ T-A14 | T-B07, T-B08, T-B11 (mốc 1) | T-C06, T-C07, T-C10 (mốc 1) | T-D05 |
| **6** | T-A15 $\rightarrow$ T-A17 | T-B09, T-B10 | T-C08, T-C09 | T-D06 |
| **7** | T-A18 (mốc 2) | T-B11 (mốc 2) | T-C10 (mốc 2) | T-D07, T-D08 |

### Deadline cứng (không được trễ)
* **Cuối tuần 1:** 4 XML + 4 XSD (có `xs:key`/`xs:unique`) phải xong (T-A03, T-A04) và solution tạo xong (T-A05) $\rightarrow$ nếu trễ, cả nhóm không code được.
* **Cuối tuần 2:** `XmlHelper` (T-A06), `NguoiDungDAL.Login` + `Session` (T-A11), `XslHelper` (T-A07) phải xong $\rightarrow$ blocker cho tuần 3 và cho form Đăng nhập.
* **Cuối tuần 3:** `TaoDeThi()` (T-A10) phải xong $\rightarrow$ blocker cho nối DAL ở form Tạo đề (T-B05) và Xem đề (T-B06).
* **Cuối tuần 5:** Validation + FK trong DAL (T-A14) xong; bản nháp báo cáo các phần Thiết kế CSDL XML, XSLT, Cài đặt đã có.
* **Cuối tuần 6:** Bản build phải chạy được trên máy khác (T-D06).
* **Cuối tuần 7:** Nộp bài (T-D08).

---

## 7. QUY ƯỚC LÀM VIỆC NHÓM

### 7.1. Git workflow
* **Branch chính:** `main` (luôn chạy được).
* **Branch cá nhân:** `feature/ten-task` (VD: `feature/tai-xmlhelper`).
* **Quy trình:** Tạo branch $\rightarrow$ code $\rightarrow$ commit $\rightarrow$ push $\rightarrow$ tạo Pull Request $\rightarrow$ 1 người khác review $\rightarrow$ merge.
* **Commit message:** `[T-A06] Viết XmlHelper.cs` (luôn ghi mã task).
* **Không commit file:** `bin/`, `obj/`, `.vs/`, `*.user`.

### 7.2. Code style
* **C#:** `PascalCase` cho class/method, `camelCase` cho biến local, `_camelCase` cho field private.
* **XML:** Thụt lề 2 space, encoding UTF-8, có `<?xml version="1.0" encoding="utf-8"?>`.
* **Comment:** Mỗi hàm public có `/// <summary>`.
* **Try-catch:** Mọi chỗ đọc/ghi file phải có, message lỗi thân thiện.
* **Đồng bộ dữ liệu:** Đổi tên/thêm/xóa thẻ XML phải sửa đồng thời XML mẫu, XSD, XSLT, `ForeignKeyChecker`, DAL và báo cả nhóm.

### 7.3. Liên lạc
* **Group chat:** Zalo/Messenger/Telegram (nhóm 3 người).
* **Họp online:** Google Meet (cuối tuần).
* **Báo cáo tiến độ:** Mỗi tối Chủ nhật, mỗi người gửi 1 tin nhắn: `"Tuần này xong gì, tuần sau làm gì, có blocker gì"`.

### 7.4. Xử lý blocker
* Nếu task bị block $> 1$ ngày $\rightarrow$ báo ngay trong group để cả nhóm hỗ trợ.
* Nếu Tài (người giữ nhiều blocker) bị kẹt $\rightarrow$ Thiết hoặc Vinh có thể nhảy vào giúp.

---

## 8. CHECKLIST NGHIỆM THU CUỐI DỰ ÁN

### 8.1. Sản phẩm kỹ thuật
* [ ] 4 file XML đúng cấu trúc, dữ liệu thật ($\ge 5$ môn, $\ge 30$ câu, $\ge 3$ đề, $\ge 4$ user); đề dùng thẻ `<CacCauHoi>`.
* [ ] 4 file XSD có `xs:key`/`xs:unique`; XML validate pass 100%; các ca sai (trùng mã, `DoKho = 4`, mật khẩu chưa băm, câu lặp trong đề) bị từ chối.
* [ ] Mật khẩu trong `NguoiDung.xml` là SHA-256; đăng nhập bằng mật khẩu gốc hoạt động.
* [ ] 2 file XSLT (`DeThi.xsl` + `DeThi_Print.xsl`) hiển thị đúng nội dung câu hỏi + tên môn (qua `document()`).
* [ ] Chức năng đăng nhập + phân quyền hoạt động (Giáo viên không xóa được môn/câu hỏi/đề).
* [ ] CRUD môn học, câu hỏi hoạt động, ghi được vào XML; các quy tắc chặn xóa (mục 6.10) hoạt động.
* [ ] Tạo đề tự động đúng độ khó, cùng môn, không lặp câu, gán `NguoiTao` đúng.
* [ ] Xem đề qua `WebBrowser` đẹp; bản in không lộ đáp án.
* [ ] Xuất HTML hoạt động (file độc lập).
* [ ] Thống kê, Đổi mật khẩu hoạt động.
* [ ] Validation XSD + FK checker hoạt động trong DAL; file hỏng không làm crash.
* [ ] Xuất PDF hoạt động (nếu làm).
* [ ] Audit log ghi lại thao tác (nếu làm).
* [ ] Backup tự động (nếu làm).
* [ ] Không hard-code đường dẫn tuyệt đối; `Data/`, `Schemas/`, `Styles/` được *Copy to Output Directory*.
* [ ] Try-catch ở mọi chỗ đọc/ghi file.
* [ ] Chạy được trên máy khác khi giải nén.

### 8.2. Báo cáo
* [ ] Chương 1: Giới thiệu đầy đủ.
* [ ] Chương 2: Khảo sát + Phân tích + Thiết kế CSDL XML + XSLT.
* [ ] Chương 3: Cài đặt (ảnh + mô tả).
* [ ] Kết luận + Hướng phát triển.
* [ ] Có đủ ảnh sơ đồ (phân cấp, DFD, ERD, wireframe).
* [ ] Có ảnh chụp tất cả form.
* [ ] Format thống nhất (font Times New Roman 13, line spacing 1.5, lề 3-2-2-2).

### 8.3. Đóng gói
* [ ] File `.zip` đúng cấu trúc (`SourceCode`, `Data`, `Schemas`, `Styles`, `Docs`, `BaoCao.docx`).
* [ ] File `.zip` $< 50\text{MB}$ (nếu nặng, xóa `bin`/`obj` trước khi nén).
* [ ] Test giải nén + chạy trên máy khác.

---

## 📌 GHI CHÚ CUỐI

* File này là "hợp đồng" giữa 3 người. Ai nhận task nào, deadline nào, DoD ra sao — đều ghi rõ. Nếu có thay đổi $\rightarrow$ cập nhật file này + báo cả nhóm.
* Task **T-A15 (PDF), T-A16 (Log), T-A17 (Backup)** và form QL Người dùng (trong T-C07) là phần tùy chọn, có thể bỏ nếu hết thời gian.
* Ưu tiên đúng thứ tự: Task nào là blocker (`T-A04`, `T-A06`, `T-A11`, `T-A07`, `T-A10`) phải xong trước — nếu trễ, cả nhóm trễ theo.
* Test sớm, test thường xuyên. Đừng đợi cuối tuần 6 mới test.
* Viết báo cáo theo mốc, đừng để dồn tuần 7.
* Hỏi giảng viên sớm nếu không chắc yêu cầu — đừng đoán.

---
*HẾT FILE — `TaskAssignment.md` v1.1 (20/11/2026), đồng bộ với `ProjectBackground.md` v2.2*
