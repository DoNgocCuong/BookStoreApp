# 🪟 ĐỒ ÁN MÔN LẬP TRÌNH WINDOWS
## Ứng dụng quản lý bán hàng (Sales Management System)

---
## Mục lục
1. [Thông tin các thành viên](#0-thông-tin-các-thành-viên)  
2. [Chức năng ứng dụng](#1-chức-năng-ứng-dụng)  
3. [Giao diện (Prototype Figma)](#2-giao-diện-prototype-figma)  
4. [Làm việc nhóm & Chiến lược Git](#3-làm-việc-nhóm--chiến-lược-git)  
5. [Kiến trúc phần mềm](#4-kiến-trúc-phần-mềm)  
6. [Design Pattern áp dụng](#5-design-pattern-áp-dụng)  
7. [Đảm bảo chất lượng](#6-đảm-bảo-chất-lượng)  
8. [Các tính năng nâng cao](#7-các-tính-năng-nâng-cao)  
9. [Kế hoạch & Tiến độ thực hiện](#8-kế-hoạch--tiến-độ-thực-hiện)  

---

## 0. Thông tin các thành viên

| STT | Họ tên | MSSV | Vai trò | Ghi chú |
|-----|---------|-------|----------|----------|
| 1 | Lê Huy | 21120466 |  |  |
| 2 | Đạo Minh Chiến | 22120033 |  |  |
| 3 | Phan Công Châu | 22120036 |  |  |
| 4 | Đỗ Ngọc Cường | 22120042 |  |  |
| 5 | Quách Thành Kiệt | 22120175 |  |  |
| 6 | Nguyễn Thanh Phong | 22120265 |  |  |

---

## 1. Chức năng ứng dụng

### **Chức năng cơ bản**
- Đăng nhập / Đăng xuất (JWT + Salt)
- Dashboard tổng quan
- Quản lý sản phẩm
- Quản lý loại sản phẩm
- Báo cáo / thống kê
- Cấu hình chương trình: phân trang, lưu lại chức năng chính lần cuối mở.

---

## 2. Giao diện (Prototype Figma)

- File Figma: [ Xem Prototype tại đây](https://www.figma.com/file/xxxxx/SalesApp_UI_V1)
- Prototype mô phỏng các luồng chính:
- Đăng nhập → Dashboard → Quản lý sản phẩm → Tạo đơn hàng → In hóa đơn  
- UI sử dụng Fluent 2 Design System của Microsoft để tương thích với WinUI 3.

---

## 3. Làm việc nhóm

### **Công cụ và quy trình**
- Quản lý mã nguồn: **GitHub**
- Giao tiếp nhóm: **Zalo, Notion, Google meet**
- Thiết kế UI: **Figma**
- IDE: **Visual Studio 2022**, **PostgreSQL / Supabase**

### **Chiến lược làm việc với Git**
- Nhánh chính: `main`  
- Mỗi thành viên tạo branch riêng: `feature/<tên-chức-năng>`  
- Quy trình merge:  
  1. Commit → Push lên nhánh cá nhân  
  2. Pull Request → Review code → Merge vào `develop`  
  3. Khi ổn định → merge `develop` → `main`

---

## 4. Kiến trúc phần mềm
1.Frontend Phần giao diện được áp dụng mô hình MVVM (Model–View–ViewModel) để tách biệt giữa giao diện, dữ liệu và logic xử lý hiển thị:
  View: Chịu trách nhiệm hiển thị dữ liệu và nhận các thao tác từ người dùng.
  ViewModel: Xử lý logic hiển thị, ràng buộc dữ liệu (data binding) và giao tiếp với backend thông qua RESTful API.
  Model: Biểu diễn dữ liệu nhận từ server, như thông tin sản phẩm, đơn hàng, hay doanh thu. 
  Cách tổ chức này giúp mã nguồn frontend rõ ràng, dễ kiểm thử và dễ mở rộng khi thêm hoặc thay đổi tính năng giao diện.
2.Backend 
Phần backend được tổ chức theo mô hình 3-Layer Architecture, đảm bảo phân tách rõ ràng giữa các tầng:
  Controller: Tiếp nhận yêu cầu từ frontend, điều phối và trả kết quả phản hồi.
  Service: Chứa toàn bộ logic nghiệp vụ của hệ thống như tính doanh thu, quản lý đơn hàng, kiểm tra tồn kho.
  Repository: Làm việc trực tiếp với cơ sở dữ liệu, thực hiện các thao tác CRUD (Create, Read, Update, Delete).
Dữ liệu giữa frontend và backend được trao đổi thông qua RESTful API, đảm bảo tính độc lập và khả năng thay thế công nghệ giữa hai phần.
3.Clean Architecture trong dự án Ứng dụng được định hướng và triển khai theo Clean Architecture, đảm bảo nguyên tắc phụ thuộc hướng vào trong (Dependency Rule) – các tầng bên ngoài có thể phụ thuộc vào tầng trong, nhưng ngược lại thì không.
  Clean Architecture ở Frontend Ở phía client, Clean Architecture được thể hiện thông qua mô hình MVVM, tương ứng với các tầng sau:
    Presentation Layer: Gồm các View hiển thị giao diện và nhận thao tác người dùng.
    Application Layer: Gồm các ViewModel xử lý logic hiển thị, gọi dữ liệu từ API và cập nhật lại giao diện.
    Domain Layer: Chứa các lớp mô hình (Model) mô tả dữ liệu cốt lõi như Product, Order, Category, User.
    Infrastructure Layer: Bao gồm các service gọi REST API, lưu dữ liệu tạm thời hoặc thao tác với bộ nhớ cục bộ.
  Clean Architecture ở Backend Phía backend cũng tuân theo nguyên tắc của Clean Architecture, được triển khai thông qua mô hình 3-Layer:
    Presentation Layer: Là tầng Controller, tiếp nhận request từ frontend và trả response cho client.
    Application Layer: Là tầng Service, chịu trách nhiệm xử lý logic nghiệp vụ và điều phối dữ liệu giữa các tầng.
    Domain Layer: Định nghĩa các đối tượng cốt lõi của hệ thống như Product, Order, Category, User.
    Infrastructure Layer: Gồm Repository và các cấu hình truy cập cơ sở dữ liệu, giúp hệ thống kết nối và lưu trữ thông tin.

---

## 5. Design Pattern sử dụng
| STT | Design Pattern                    | Mục đích chính                                                                                                                                           |
| :-: | :-------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  1  | **Command**                       | Đóng gói **thao tác người dùng** (nhấn nút, menu) thành đối tượng để thực thi và quản lý.                                                                |
|  2  | **Observer**                      | **Cập nhật tự động** các phần UI (View) phức tạp khi trạng thái dữ liệu (Model/ViewModel) thay đổi, ngoài `INotifyPropertyChanged` cơ bản.               |
|  3  | **Repository**                    | Cung cấp lớp trung gian để **quản lý dữ liệu** và tách biệt **Tầng Logic Nghiệp vụ (ViewModel)** khỏi chi tiết truy cập dữ liệu (SQL, Web API).          |
|  4  | **Facade**                        | Cung cấp một **interface đơn giản** cho ViewModel truy cập vào một **hệ thống con phức tạp** (bao gồm DB, File Storage, Web Service).                    |
|  5  | **Factory Method** / **Mediator** | **Tạo các đối tượng** giao tiếp client-server (**Service Connector**) một cách **độc lập** với code Business Logic (ViewModel).                          |
|  6  | **Strategy**                      | Thay đổi **thuật toán xử lý** động.                                                                                                                      |

---

## 6. Đảm bảo chất lượng

---

## 7. Tính năng nâng cao

| Tên tính năng | Ghi chú |
|----------------|---------|
| Auto Save | +0.25 |
| Responsive Layout | +0.5 |
| Bổ sung khuyến mãi | +1.0 |
| Sử dụng kiến trúc MMVM | +0.5 |
| Sử dụng dependency injection | +0.5 |
| Quản lý khách hàng | +0.5 |
| In đơn hàng (PDF) | +0.5 |
| Hỗ trợ sắp xếp khi xem danh sách theo yêu cầu | +0.5 |
| Hỗ trợ tìm kiếm nâng cao | +1.0|

---

## 8. Kế hoạch & Tiến độ thực hiện

| Tuần | Nội dung công việc |
|------|--------------------|
| Tuần 1 | Khảo sát đề tài, phân tích yêu cầu, dựng prototyep figma
| Tuần 2 | Thiết kế UI (Figma), dựng kiến trúc MVVM, Hoàn thiện tầng dữ liệu + Repository
| Tuần 3 | Kết nối API, binding dữ liệu UI, Thêm chức năng CRUD + Dashboard
| Tuần 4 | Tích hợp nâng cao, backup/restore, khuyến mãi
| Tuần 5 | Test manual, unit test, hoàn thiện logic
| Tuần 6 | Hoàn thiện báo cáo, video demo, nộp đồ án
| Tuần 7 | Dự phòng

---

---

## Tác giả
> **Đồ án môn học: Lập trình Windows**
> GVHD: *Thầy Trần Duy Quang*  
> Năm học: 2025

---

