# Exam Bank — Quản lý đề thi trắc nghiệm

Đồ án môn Công nghệ XML (WinForms, C# / .NET Framework 4.8).
Nhóm 3 người: Tài, Thiết, Vinh.

## Công nghệ
XML, XSD, XSLT, LINQ to XML, XPath, SHA-256.

## Cấu trúc thư mục
```text
Final_XML.sln
Final_XML/
├── Data/       các file .xml (MonHoc, CauHoi, DeThi, NguoiDung)
├── Schemas/    các file .xsd
├── Styles/     DeThi.xsl, DeThi_Print.xsl
├── Models/     lớp dữ liệu
├── DAL/        truy cập dữ liệu XML
├── Helpers/    XmlHelper, XslHelper, ForeignKeyChecker, Session...
├── Forms/      các form WinForms
Docs/           tài liệu, sơ đồ, wireframe, test case
```

## Tài khoản thử
| Tên đăng nhập | Mật khẩu | Quyền |
| :--- | :--- | :--- |
| admin | 123 | Admin |
| gv01 | 123 | Giáo viên |
| gv02 | 123 | Giáo viên |
| gv03 | 123 | Giáo viên |

Mật khẩu trong `Data/NguoiDung.xml` được lưu dạng SHA-256 (hex thường, 64 ký tự).

## Tài liệu
- [ProjectBackground.md](Docs/ProjectBackground.md): mô tả dự án
- [TaskAssignment.md](Docs/TaskAssignment.md): phân công công việc

## Quy ước Git
- Nhánh chính: `main`; nhánh cá nhân: `feature/ten-task`
- Commit message ghi mã task, ví dụ: `[T-A06] Viết XmlHelper.cs`
