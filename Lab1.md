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

Nhiệm vụ của từng lớp phân tích:
- Employee (Nhân viên):
  - Nhiệm vụ: Yêu cầu tính toán và xử lý thanh toán.
  - Thuộc tính:
    - name: Tên nhân viên.
    - salary: Mức lương của nhân viên.
    - commissionRate: Tỷ lệ hoa hồng (nếu có).
    - paymentMethod: Phương thức thanh toán đã chọn.
- PayrollProcessor (Bộ xử lý lương):
  - Nhiệm vụ: Xử lý tính toán lương dựa trên thông tin nhân viên và timecard. Sau đó, hệ thống thực hiện thanh toán dựa trên phương thức thanh toán đã chọn.
  - Phương thức:
    - calculatePayment(): Tính toán tổng số tiền lương cho nhân viên.
    - processPaymentMethod(): Xử lý thanh toán dựa trên phương thức được chọn.
- PaymentMethod (Phương thức thanh toán):
  - Nhiệm vụ: Xác định phương thức thanh toán (ví dụ: chuyển khoản, nhận qua bưu điện) và cung cấp chi tiết thanh toán.
  - Thuộc tính:
    - type: Loại phương thức thanh toán (Direct Deposit, Mail, Pick-Up).
    - details: Chi tiết liên quan đến phương thức (ví dụ: số tài khoản).
- BankSystem (Hệ thống ngân hàng):
  - Nhiệm vụ: Xử lý các giao dịch chuyển khoản trực tiếp nếu phương thức thanh toán là Direct Deposit.
  - Phương thức:
    - processDirectDeposit(): Xử lý giao dịch chuyển khoản trực tiếp.
- PayrollDatabase (Cơ sở dữ liệu lương):
  - Nhiệm vụ: Lưu trữ thông tin về nhân viên, timecard và kết quả thanh toán. Cung cấp dữ liệu cho bộ xử lý lương khi cần thiết.
  - Phương thức:
    - getEmployeeDetails(): Lấy thông tin của nhân viên.
    - getTimecards(): Lấy timecard của nhân viên.
    - storePaymentRecord(): Lưu trữ thông tin về giao dịch thanh toán.

Biểu đồ lớp phân tích cho ca sử dụng Payment:

![Diagram](https://www.planttext.com/api/plantuml/png/T59BJiD03DtFARo4HI-G1QfGM29LRI_WJgmoOZx1zYmYnCbOS2IkG3uJchImdFUUxUVd-VxyseeYQmxUM8yYy1HQdpeYU3S06uWOg8A3ield4H3qo5q5TSedJoDaKmXEnAMuHwKLrM8NAEepwKjgAjWjdxq0WEajasWXxkxDXob6UeYJzpjEbaGIZuO0B7gRVJ_dKZB0xIHR3IWKvrXwNRM_ACkoshNhPHjIT5uMsFMaPSj7ZA-7JfH2yLgajMEoMbERnFsrOesA9nGgLMVI-GZrDByiqXD75yWYDpCacdXEOaysSJFr_xtYPlDmawIvYNQXcityAreSS9tXm2yYg20BYJ5RYitmlNu0003__mC0)

Giải thích:
  - Employee: Đại diện cho nhân viên yêu cầu xử lý lương. Họ có thuộc tính liên quan đến tên, lương, và phương thức thanh toán.
  - PayrollProcessor: Lớp trung tâm, thực hiện tính toán lương và xử lý các bước thanh toán.
  - PaymentMethod: Lớp lưu trữ và xử lý các phương thức thanh toán.
  - BankSystem: Hệ thống bên ngoài xử lý các giao dịch ngân hàng, được sử dụng khi thanh toán qua chuyển khoản.
  - PayrollDatabase: Lưu trữ tất cả thông tin nhân viên và lịch sử thanh toán.

### 4. Phân tích ca sử dụng Maintain Timecard:

Trong ca sử dụng Maintain Timecard, hệ thống sẽ xử lý việc nhân viên nộp và cập nhật timecard (bảng giờ làm việc). Timecard lưu giữ thông tin về giờ làm việc và dự án mà nhân viên đã tham gia. Dưới đây là các lớp phân tích chính:
- Employee (Nhân viên): Nhân viên sẽ nộp timecard ghi lại số giờ đã làm việc và các dự án liên quan. Họ có thể tạo, chỉnh sửa hoặc nộp timecard thông qua giao diện người dùng.
- Timecard: Đại diện cho bảng ghi số giờ làm việc của nhân viên trong một khoảng thời gian nhất định, chứa thông tin như ngày, giờ làm và số dự án.
- PayrollProcessor (Bộ xử lý lương): Lớp này xử lý timecard, xác minh dữ liệu và ghi lại giờ làm việc cho các dự án. Nó cũng đảm bảo rằng timecard được tính chính xác khi xử lý lương.
- ProjectManagementDB (Cơ sở dữ liệu Quản lý Dự án): Chứa thông tin về các dự án và mã số dự án mà nhân viên làm việc. Lớp này chịu trách nhiệm xác minh mã số dự án trên timecard.
- PayrollDatabase (Cơ sở dữ liệu lương): Lưu trữ thông tin về timecard đã nộp và lịch sử các bảng ghi giờ của nhân viên.

Biểu đồ Sequence:

![Diagram](https://www.planttext.com/api/plantuml/png/X99DRi8m48NtFeMNPS45igWGfSiYf5Ri9yu3ZFmJZIUWd8r5ZzGhrAdgHPfGjfxtvdlpvA_Rvoe9iNJUAJ8IMR_wriKUK6r-jiQs54JlgEVet8wZGKgHHyCFws68cx63unb6tYZG4Hv1DkkvZHiIgYb1gSBLo-S9hjAfgxsLGdfQgB-ImLR6bJOC4cnnVU2OILdf2zWU-fSJyH7RpjVWDDYdKhsSpSgGZiEUd6r8R0pPF0yVLv2FpFrZchW8xk1C30VB_XzKjfLsAos_-zz_6XKCe1L2C_o0Rm000F__0m00)

Nhiệm vụ của từng lớp phân tích:
- Employee (Nhân viên):
  - Nhiệm vụ: Nhân viên tạo và nộp timecard, ghi lại giờ làm việc hàng tuần hoặc hàng tháng, và có thể chỉnh sửa timecard nếu cần thiết.
  - Thuộc tính:
    - name: Tên nhân viên.
    - employeeId: Mã số nhân viên.
- Timecard:
  - Nhiệm vụ: Lưu trữ thông tin về số giờ làm việc, ngày và mã số dự án liên quan. Đây là bảng ghi giờ làm việc của nhân viên.
  - Thuộc tính:
    - date: Ngày làm việc.
    - hoursWorked: Số giờ đã làm việc.
    - chargeNumber: Mã số dự án mà nhân viên đã làm việc.
- PayrollProcessor (Bộ xử lý lương):
  - Nhiệm vụ: Xử lý timecard nộp lên từ nhân viên, xác minh thông tin dự án, và lưu timecard vào cơ sở dữ liệu.
  - Phương thức:
    - processTimecard(): Xử lý và xác minh thông tin timecard.
    - submitTimecard(): Gửi timecard lên hệ thống.
- ProjectManagementDB (Cơ sở dữ liệu Quản lý Dự án):
  - Nhiệm vụ: Xác minh mã số dự án từ timecard của nhân viên để đảm bảo thông tin hợp lệ.
  - Phương thức:
    - verifyChargeNumbers(): Xác minh tính hợp lệ của mã số dự án.
- PayrollDatabase (Cơ sở dữ liệu lương):
  - Nhiệm vụ: Lưu trữ timecard đã được xác minh và lịch sử giờ làm việc của nhân viên để phục vụ tính toán lương sau này.
  - Phương thức:
    - storeTimecard(): Lưu trữ timecard vào cơ sở dữ liệu.
    - getTimecards(): Lấy timecard của nhân viên để xử lý lương.

Biểu đồ lớp phân tích cho ca sử dụng Maintain Timecard:

![Diagram](https://www.planttext.com/api/plantuml/png/T59BJiCm4Dtx5BEaYro01QeW8B6WgbIahYVEa1hygSQJeWXnCXOSYIlW1BTAIRgnD6zctiVspzVtCWgojCugRJ56k7Tx6peY-5001NXqT0qROUER0Q3SVwn7C41iAsVasJZIoFNLGdsgJ7Z4Cc6DaWZBT0xbBhGSju7VAF4zs80om7g7tD2gTHNncOvcIgihUXz9zNX39_6I18sDOmzhx3XOk-QWASR0WnU0_L_zZseIfGSFQ4rlVIvXedqbBK_eiI57NihRB70WDY_TtIZCdArq6LXXfBmK9J1TZfSPJkzK53UJV6eIk9ywCintPr9S63nthPRaw_x__0800F__0m00)

Giải thích:
  - Employee: Nhân viên tạo và nộp timecard. Họ cung cấp thông tin về giờ làm việc và mã số dự án.
  - Timecard: Chứa dữ liệu về ngày làm việc, số giờ làm và mã dự án. Đây là bảng ghi giờ làm việc của nhân viên.
  - PayrollProcessor: Xử lý timecard của nhân viên, xác minh tính hợp lệ và sau đó lưu vào cơ sở dữ liệu lương.
  - ProjectManagementDB: Xác minh mã dự án để đảm bảo rằng các dự án được ghi trong timecard là hợp lệ.
  - PayrollDatabase: Lưu trữ thông tin timecard và cung cấp dữ liệu để tính toán lương sau này.

### 5. Hợp nhất ca sử dụng:

Khi hợp nhất kết quả phân tích của hai ca sử dụng Payment và Maintain Timecard, chúng ta nhận thấy rằng cả hai đều liên quan đến việc quản lý dữ liệu nhân viên, xử lý timecard, và tính toán lương.

Kết quả phân tích được hợp nhất để tạo ra một hệ thống hoàn chỉnh:
- Tích hợp dữ liệu: Timecard và Payment đều dựa trên cùng một tập dữ liệu của nhân viên, nên cần có sự chia sẻ thông tin giữa hai quy trình này.
- Tích hợp xử lý: PayrollProcessor chịu trách nhiệm xử lý cả việc tính toán lương (Payment) và xử lý timecard (Maintain Timecard).
- Sử dụng chung cơ sở dữ liệu: PayrollDatabase lưu trữ thông tin về nhân viên, timecard và kết quả thanh toán, cho phép cả hai ca sử dụng truy cập và cập nhật dữ liệu.

Mô tả kết quả hợp nhất:
- Employee (Nhân viên): Là đối tượng trung tâm, chịu trách nhiệm nộp timecard và yêu cầu tính toán lương. Employee sẽ gửi thông tin về giờ làm việc qua timecard và yêu cầu nhận lương qua một phương thức thanh toán đã chọn.
- Timecard: Đây là bảng ghi lại thông tin về giờ làm việc và dự án của nhân viên. Timecard sẽ được xử lý bởi PayrollProcessor, xác minh tính hợp lệ với ProjectManagementDB, sau đó lưu trữ trong PayrollDatabase.
- PayrollProcessor (Bộ xử lý lương): Thành phần xử lý trung tâm đảm nhận vai trò tính toán lương dựa trên timecard của nhân viên và xử lý thanh toán. Nó liên kết hai quy trình lại với nhau bằng cách tính toán lương dựa trên thông tin giờ làm việc và đơn hàng đã được lưu trữ.
- PaymentMethod (Phương thức thanh toán): Lớp này lưu trữ và xác định cách thức nhân viên được thanh toán (chuyển khoản, nhận tiền mặt). Khi lương đã được tính toán xong, hệ thống sẽ thực hiện thanh toán dựa trên phương thức đã chọn.
- ProjectManagementDB: Hệ thống này xác minh các mã dự án từ timecard trước khi chúng được xử lý và lưu vào cơ sở dữ liệu lương.
- PayrollDatabase: Là nơi lưu trữ thông tin về nhân viên, timecard và lịch sử thanh toán. Cả hai ca sử dụng đều cần truy cập và cập nhật dữ liệu tại đây.
- BankSystem: Hệ thống này xử lý các giao dịch chuyển khoản trực tiếp nếu nhân viên chọn phương thức thanh toán qua ngân hàng.
