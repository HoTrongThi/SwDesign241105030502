# Lab1: Phân tích kiến trúc, cơ chế, ca sử dụng

### 1. Phân tích kiến trúc: 

Hệ thống Payroll sẽ áp dụng kiến trúc Client-Server, với các thành phần chính bao gồm:
- Lớp giao diện người dùng (UI): Đây là giao diện Windows desktop cho phép nhân viên nhập thông tin về thời gian làm việc (timecards), chọn phương thức thanh toán, và tạo các báo cáo.
- Lớp logic nghiệp vụ (Business Logic Layer): Đây là lớp trung tâm thực hiện tất cả các quy tắc xử lý lương, bao gồm tính toán giờ làm việc, tiền lương, và xử lý các đơn hàng của nhân viên hoa hồng.
- Lớp truy cập dữ liệu (Data Access Layer): Lớp này tương tác với cơ sở dữ liệu Payroll và cơ sở dữ liệu quản lý dự án (DB2) kế thừa, giúp lấy dữ liệu cần thiết cho hệ thống mà không làm thay đổi hệ thống hiện có.
- Giao diện hệ thống ngân hàng (Bank System Interface): Giao diện này xử lý các giao dịch chuyển khoản trực tiếp đến hệ thống ngân hàng.

Lý do lựa chọn:
- Modular và dễ bảo trì: Tách biệt từng thành phần giúp hệ thống dễ bảo trì và mở rộng trong tương lai.
- Tính bảo mật: Giao diện với hệ thống ngân hàng và cơ sở dữ liệu quản lý dự án được tách biệt nhằm tăng cường tính bảo mật và giảm thiểu rủi ro trong xử lý dữ liệu nhạy cảm.
- Tương thích với hệ thống kế thừa: Hệ thống Payroll mới sẽ kết nối với cơ sở dữ liệu DB2 hiện có mà không cần thay đổi cấu trúc hệ thống cũ.
- Tính linh hoạt: Nhân viên có thể chọn phương thức thanh toán tùy chỉnh, từ nhận tiền mặt, qua đường bưu điện, hoặc chuyển khoản trực tiếp.

Biểu đồ Package:

![Diagram](https://www.planttext.com/api/plantuml/png/X9HDRi8m48NtEON5gbrmWIugIiEY4bH8j0SOp2Yu-2SQJwH65IVheaVg5MgJH2Gnq5baaVUI-Tvuaj_ldvbd8AwCpagG1oXGJDPGazDQR6hFQ2RYAnEXpZAXHyl0obcnX1gfiyII6hmN2rDgLoE-l_IaM5DXmU3eLWcr2MzS8U_TRg09uL6Zv7NVSNS_zbHRe_XD6PH0VVcODTTXW7dbbSL0kNI5ajSYj5DOavF1woW98a7BIWDZ2pV22h6QHozmDKMLRPiCa5EES_G4WkiI7yI6ITbY9EsGGMcVg9U7aWE3U9BoD9UR4udEBNXCMB0zz6WOHIsGkvN86woRaSbzX4DVWGreCNm-JvgLZUToh-SzK86lbTaY_RiEYqz6ij3jkq-3py4U6d648ReppXL562oTLtojO--Zc4uVamKxUPAjwpcxmTymfeExRZwdoexP3Eqk_WJ-0000__y30000)

Ý nghĩa từng thành phần:
- EmployeeUI: Thành phần giao diện người dùng cho phép nhân viên tương tác với hệ thống, chọn phương thức thanh toán và nộp timecard.
- PayrollProcessor: Lớp này thực hiện các tính toán và quy tắc nghiệp vụ liên quan đến việc xử lý lương và timecard của nhân viên.
- PaymentMethod: Lưu trữ phương thức thanh toán mà nhân viên chọn, có thể là chuyển khoản, nhận trực tiếp hoặc qua bưu điện.
- PayrollDatabase: Cơ sở dữ liệu lưu trữ thông tin về nhân viên và lịch sử thanh toán, dùng để truy vấn thông tin khi cần thiết.
- ProjectManagementDB: Cơ sở dữ liệu quản lý dự án kế thừa, lưu trữ các số liệu về dự án mà nhân viên làm việc.
- BankSystem: Xử lý các giao dịch ngân hàng liên quan đến chuyển khoản trực tiếp cho nhân viên khi chọn phương thức này.

### 2. Cơ chế phân tích:

Các cơ chế cần giải quyết trong bài toán:

| Cơ chế| Giải thích|
|---|----------------|
|Persistency (Lưu trữ) | Hệ thống cần một cơ chế lưu trữ dữ liệu trong cơ sở dữ liệu quan hệ (RDBMS) để đảm bảo tính bền vững của thông tin nhân viên và lịch sử thanh toán.|
|Security (Bảo mật) | Đảm bảo rằng chỉ nhân viên có thể truy cập và chỉnh sửa thông tin của họ, và chỉ quản trị viên lương có quyền thay đổi thông tin chi tiết của nhân viên.|
|Concurrency Control (Kiểm soát truy cập đồng thời) | Hệ thống phải hỗ trợ nhiều nhân viên truy cập cùng lúc mà không gây xung đột hoặc làm hỏng dữ liệu.|
|Transaction Management (Quản lý giao dịch) | Đảm bảo rằng tất cả các quy trình xử lý lương được thực hiện trong các giao dịch, để đảm bảo tính toàn vẹn và khôi phục dữ liệu nếu xảy ra lỗi.|
|Audit Logging (Ghi nhật ký kiểm tra) | Ghi lại mọi thay đổi về timecard và đơn hàng, cũng như mọi hoạt động truy cập để đảm bảo tính bảo mật và tuân thủ các quy định pháp luật.|
|Batch Processing (Xử lý theo lô) | Lương được tính tự động vào thứ Sáu hàng tuần và ngày làm việc cuối cùng của tháng, vì vậy cần có cơ chế xử lý tự động, không cần can thiệp thủ công.|
|Integration with Legacy Systems (Tích hợp với hệ thống kế thừa) | Hệ thống cần kết nối với cơ sở dữ liệu DB2 hiện tại để truy xuất thông tin dự án mà không thay đổi hệ thống cũ.|
|Reporting (Báo cáo) | Cần cơ chế tạo các báo cáo cho cả nhân viên (tổng số giờ làm việc, tổng lương, nghỉ phép còn lại) và quản trị viên lương (giờ làm việc tổng cộng, lương năm tới nay).|
|Data Validation (Xác minh dữ liệu) | Cần xác minh dữ liệu đầu vào từ timecard và đơn hàng để tránh lỗi và đảm bảo rằng tất cả thông tin được nhập đều hợp lệ.|

Lý do lựa chọn:
- Persistency: Đảm bảo rằng mọi thông tin quan trọng đều được lưu trữ an toàn, và có thể khôi phục lại khi cần thiết.
- Security: Bảo mật thông tin lương của nhân viên là ưu tiên hàng đầu, với các chính sách phân quyền nghiêm ngặt.
- Concurrency Control: Hệ thống phải có khả năng phục vụ nhiều nhân viên cùng lúc mà không làm gián đoạn quy trình làm việc.
- Transaction Management: Bảo vệ tính toàn vẹn của dữ liệu khi có các thay đổi lớn (như tính lương hàng loạt) hoặc khi có lỗi phát sinh trong quá trình xử lý.
- Audit Logging: Theo dõi và ghi lại các hoạt động quan trọng để đảm bảo tính minh bạch và giúp kiểm tra nếu cần.
- Batch Processing: Cần xử lý hàng loạt lương và các giao dịch vào những khoảng thời gian định kỳ mà không cần sự can thiệp thủ công.
- Legacy System Integration: Tích hợp dễ dàng với hệ thống DB2 hiện có mà không làm thay đổi hoặc gây rủi ro cho hệ thống cũ.
- Reporting: Giúp nhân viên và quản trị viên lương dễ dàng xem các thông tin cần thiết về lương và giờ làm việc.
- Data Validation: Đảm bảo tính chính xác và hợp lệ của dữ liệu trước khi lưu trữ hoặc xử lý.

### 3. Phân tích ca sử dụng Payment:

Trong ca sử dụng Payment, hệ thống xử lý yêu cầu tính lương và phát lương cho nhân viên. Dưới đây là các lớp phân tích được xác định:
- Employee (Nhân viên): Đại diện cho nhân viên trong hệ thống. Nhân viên có các thuộc tính như tên, lương, hoa hồng, phương thức thanh toán. Nhân viên yêu cầu hệ thống tính toán và xử lý thanh toán dựa trên thông tin timecard và đơn hàng của họ.
- PayrollProcessor (Bộ xử lý lương): Lớp này chịu trách nhiệm thực hiện toàn bộ quy trình tính toán tiền lương, xử lý đơn hàng cho nhân viên hoa hồng và đảm bảo thanh toán chính xác.
- PaymentMethod (Phương thức thanh toán): Đại diện cho cách thức thanh toán của nhân viên (ví dụ: chuyển khoản, nhận qua bưu điện). Lớp này chứa thông tin về loại thanh toán và chi tiết thanh toán cụ thể (ví dụ: số tài khoản ngân hàng).
- BankSystem (Hệ thống ngân hàng): Đối với những nhân viên chọn phương thức chuyển khoản, hệ thống ngân hàng sẽ xử lý giao dịch để chuyển tiền trực tiếp vào tài khoản của nhân viên.
- PayrollDatabase (Cơ sở dữ liệu lương): Lưu trữ thông tin nhân viên, timecard, và lịch sử thanh toán. Cơ sở dữ liệu này cung cấp thông tin cho PayrollProcessor để tính toán lương và lưu trữ kết quả sau khi xử lý.

Biểu đồ Sequence:

![Diagram](https://www.planttext.com/api/plantuml/png/b9DDJiGm38NtEOMNi9WBT856K9P88-029ZKGaRznt4NFne8ZSGLIjIMTQOk6xcg_p-yrJhy_l_P9aALrLg6Mm73leWqTaOgvRBI9w0KEs76mzi11Kqg1rver2hvWMe2El3oGl8Vcf7EB_kEfIq9EgSaJTZSBgmgOZYqb6KTTNQjpoGoRGbJmHZADhKdGs5J8IGMx3KDfsI_fYusVZIEDtFpNSivjcPNZh20ElPFgO5dU_pGSbRDFH7ksD309QiEa1MgA8HbHa9-rT6Mblz46SWJp_1ujieriElXNmwvGv9iB3p_bAqnZ_aVIWPlL-vBHQRqvwY2_2xb2GZsnpuxzB_43003__mC0)

