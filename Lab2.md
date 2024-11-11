# Lab2: Thực hành phân tích các ca sử dụng của hệ thống Payroll System
### 1. Phân tích ca sử dụng Create Administrative Report
#### 1.1. Xác định các lớp phân tích
- Payroll Administrator: Người dùng yêu cầu báo cáo hành chính.
- System: Xử lý yêu cầu và tạo báo cáo dựa trên các tiêu chí đã nhập.
- Report: Đối tượng đại diện cho báo cáo được tạo ra.
#### 1.2. Biểu đồ tuần tự

![Diagram](https://www.planttext.com/api/plantuml/png/T95DJiCm48NtFiKiGIeNo08rWWDOz0GZUmeZ-GzxqYfdOy6Hk09E3MaIodRcU_Fydhy-FlT5CClWdK8ZCOF6CKVdUkivS96Cqn0Bw5wb2hBXX47WC1OXlngzK8fPbD8zF3p-05sTlWzK1F9b2oOJ2iUWsduYTT-1pj4dWMFrca4Moenm9sEY7LWKAZi8wAdSRpog-iIMjjA5HtjR1q-J_GoUMTwW939yPB9NNQFNAMJ80LufK6saikt29iKpb-Hm_5t-quH4A7YYsoSMHLmW5qthwtRYDVCtx-5g12YBhBDcJy5El_yD003__mC0)

#### 1.3. Nhiệm vụ của từng lớp
- Payroll Administrator: Yêu cầu hệ thống tạo và lưu báo cáo.
- System: Xử lý yêu cầu tạo báo cáo, thu thập tiêu chí, và lưu báo cáo.
- Report: Đại diện báo cáo được tạo ra, bao gồm các thông tin như tổng số giờ làm.
#### 1.4. Biểu đồ lớp phân tích

![Diagram](https://www.planttext.com/api/plantuml/png/R57BRSCm3Brh2XsJGnRG8N21350qxG2iJ1W2P2ebwG96qSbww4XT8N8ifRLh7GJmYTJxyEVhkn45rg6FnaSGiOymSehneUq31L46JMm_Z9rEQ9qzAmVgvfgWnoMIHzS8lWqe-eINnBhRpw30EzwHJrEepwCezfNC3yn8-YB8RbDL-Kf11rboUaRGIk0vA7A0sl9VGamUD2JwxRXBcZkg9BvLp-DbvV4Lkq2dJEdiTCyWKhk6V2BDbfR37H9cF_Wtcsr9cwiv78urE5V35bEGwR5OS2KLCKrMDktx2W00__y30000)

### 2. Phân tích ca sử dụng Create Employee Report
#### 2.1. Xác định các lớp phân tích
- Employee: Người dùng yêu cầu tạo báo cáo cá nhân.
- System: Xử lý yêu cầu và tạo báo cáo cá nhân theo tiêu chí.
- Report: Đại diện cho báo cáo cá nhân.
#### 2.2. BIểu đồ tuần tự

![Diagram](https://www.planttext.com/api/plantuml/png/Z951Ri9034NtEOKlm0Mog5Y0kaNb15R6K4kJ6NViW7AsBdeahi24OO2eLTIj_Rw__Ntv_bchORAXzmrs5XDiU_5n96eabxbZmM2m7zMedvK-I6AofgayhDxkM9jxNmEfWL3I6D13Ad3fJsHLjR1BiHU3GxOk5DWe11WSE3JIFmsowCIEgiAH8NjzcL-sQ-6T0gKyff9djazGeOuFJEuXBFZy11jIWEDTxvPEsB2Anx4YYv5O1CKJ_JEH6-fZXyOnB2On9ty7iN-QJZiyo3K5Dpt_2W00__y30000)

#### 2.3. Nhiệm vụ từng lớp
- Employee: Yêu cầu tạo và lưu báo cáo cá nhân.
- System: Xử lý yêu cầu, thu thập tiêu chí, tạo và lưu báo cáo.
- Report: Đại diện cho báo cáo cá nhân bao gồm thông tin giờ làm, dự án, ngày nghỉ và lương.
#### 2.4. Biểu đồ lớp phân tích

![Diagram](https://www.planttext.com/api/plantuml/png/R5713S8m3FndYZpXqGNoG7t00XG62AbLHKgJOhj85M8o7ep42hGqARIGHoHVphdp-Nb_vCGQkQsTC4uJoLtTkD01oAkGmx6baWMZzTLOUrt37C7WbWYSMo3UGnEGL-iH97s12Rc9A5Tqn50dCTCYWkSZ0Qh9IMndpItDTGo2vlIfGSk0LYVAhwmBHhCD_iEOR8oCP0FVrQ5h5dETeB9-sqigETmZ2BvSGYPuxiUODrVW0NlATnx_BKqhoB9D2aYbK4b4P7YCjbLCWaJUknbs-G800F__0m00)

### 3. Phân tích ca sử dụng Login
#### 3.1. Xác định các lớp phân tích
- User: Người dùng yêu cầu đăng nhập.
- System: Xác thực thông tin đăng nhập của người dùng.
#### 3.2. BIểu đồ tuần tự

![Diagram](https://www.planttext.com/api/plantuml/png/T4-n3G8n3EmzXHTWWI_G5z3H8UYjnBmY9VueTa0_6mKZiGA9GE8fS67fpkSxtVF-6DMeM4qHoDbSyAHS83Sgk91938-B6YU0Vi3DzeC7t8ireZPMA36IUCoaUfkBXxTchJvJ39wCqHNsB1OeAb2qDSPh5m6s-Hhqs04FynG4jJh7gfSQWQF-U66G_z-xe3dIWbnAQvYQ1KqCB1x6jdht5m000F__0m00)

#### 3.3. Nhiệm vụ từng lớp
- User: Nhập thông tin đăng nhập.
- System: Xác thực và thông báo kết quả đăng nhập.
#### 3.4. Biểu đồ lớp phân tích

![Diagram](https://www.planttext.com/api/plantuml/png/P8_13S8m34NlcIB78j45Sa2L6A5Y02kngaX9Ycm7X12JSM0aLY19wQ7Wa_Lj__VzVhu65Y39CIWRW5cV64dVbQwLIvyWej6Za4_JefxBsdKcjrN3FFdKxTH3VOt66ml6rQfG9FFsn6OYJ5A9fd4N-GB1En0y4heozX2u-qso_qlHo2rytnzMkD4-2H9OOJLWSlND3m000F__0m00)

### 4. Phân tích ca sử dụng Maintain Employee Information
#### 4.1. Xác định các lớp phân tích
- PayrollAdministrator: Đại diện cho người quản trị thực hiện các tác vụ quản lý thông tin nhân viên.
- System: Xử lý các yêu cầu từ quản trị viên để thêm, cập nhật hoặc xóa thông tin nhân viên.
- Employee: Đối tượng nhân viên với các thông tin như tên, loại hình làm việc, địa chỉ và các thông tin liên quan khác.
#### 4.2. BIểu đồ tuần tự

![Diagram](https://www.planttext.com/api/plantuml/png/r5HBJiCm4Dtx5BC4gLmW2zIeOS4kQiK1h7WgBFd7UD8gPsF1aRW2Jc88AKdLBP6InVWzlu-jVBv_R2DBujOQ8Hls1BNio1jJAgkTZaoo7ye8TIb20kf61-aO3brajBFHamt6TuX2r2KyF6P80NjyQp4oi0ShjUFq0cOiQ7VqP2LhxyH8wAbrMK1DtWQ6j0m-80qGu2uWt9LARU0bACcuWGeDCjvVY1xIjE4BfX3IC2Jsv1NIiwhhy3mvLPYScpWmvbg9ST8Abw7Jvj-Q1Um8a_NvzcVDhol4tbMbOp2octEUAu4cOgxYnb2_sJTaoQYb67jaqdZ2vTDSpz2qH9Wkp2fjsL8xf5HNH2PhkP4_9pBKDTwO_rENTqUTOH06PmjETYCg9KtXhbMJq_-O86myAO5EYMtwz7-2Bm000F__0m00)

#### 4.3. Nhiệm vụ từng lớp
- PayrollAdministrator: Chọn loại thao tác (thêm, cập nhật, xóa), cung cấp thông tin nhân viên cần thiết, và xác nhận thao tác.
- System: Xử lý các yêu cầu, lấy thông tin đầu vào, tạo, cập nhật hoặc xóa thông tin nhân viên trong hệ thống.
- Employee: Lưu trữ thông tin của nhân viên, thực hiện các thay đổi hoặc xoá dữ liệu khi được yêu cầu.
#### 4.4. Biểu đồ lớp phân tích

![Diagram](https://www.planttext.com/api/plantuml/png/T99DJiGm38NtEKMM7OcvG1TeGCE27MBW0AQnHX7vavq8HOYJiU18N86KDgNjb2o_vyJFp_d-_3fm18h96j4PO9OFaCaRSwEiTfeZGVGatuNi3_Jm_jZAKoJjpWDqO759olqL0QNkR30-8pQx0QMW8EAQAZIue1zYz7NA7D5M9yLqJBniqYKYTF6PaThDCOQoGBv3vgc73rXKxLrzxKhYgFsDEZDIBrOhbyN_vVBcwVKfXyjigFXPGWO3b5jvzEd5u3YVjrOp5wUF9RcLHbXOep22DjDRktPoEmzze-pMbvs1co-XcU4o_EQ_sE-lws9QQS716LcCeDUch7vL7P8fxLaSqAd-n_q0003__mC0)

### 5. Phân tích ca sử dụng Maintain Purchase Order
#### 5.1. Xác định các lớp phân tích
- CommissionedEmployee: Đại diện cho nhân viên nhận hoa hồng, người tạo, sửa hoặc xóa đơn hàng mua.
- System: Xử lý các yêu cầu tạo, sửa hoặc xóa đơn hàng mua từ nhân viên.
- PurchaseOrder: Đối tượng đơn hàng với các thông tin như khách hàng, sản phẩm, và giá trị đơn hàng.
#### 5.2. BIểu đồ tuần tự

![Diagram](https://www.planttext.com/api/plantuml/png/n9DDJeH048NtVOfQQZ9UO1Pc3B1m1Pc91-ZGDR6J_flkOWndS-6Hl8B5ZsDW47Kb2IHqtglwwb6ylxxj4ib8ZJL2rkGZPDvQdPBs3bLXW_4j8iW4MI422tMjWtG4XpOHsibHrSJwMIOieyBOMQfIYAo0k_jHlOKzdXfC1EJ1Iks8RmYZ3Npd4uEqCsN55gheRI0uCfWF62Kn5r0R46uUbDh0Kr2IS0Cv6YIydRKxy6bDCwSGqX2m-m8CFR40lhxjFgK4XSnkKk-PzcJFMQibtLVjgjn25f79mU7BF85hZbodO6GxXtZC1Hf-6qBuqpYN0ZyDC4gcx7kagF6CQwaiJr0tCIBlog3NZbbi_sbMG9f-FBMIvHZ0TT4-dc4t_YEUNwVYtL6Fp11wZ8NEsQ3YUZpFPsJJpkEeiuL2fyIE7zrF_W400F__0m00)

#### 5.3. Nhiệm vụ từng lớp
- CommissionedEmployee: Chọn loại thao tác (thêm, cập nhật, xóa), cung cấp thông tin đơn hàng cần thiết, và xác nhận thao tác.
- System: Xử lý các yêu cầu thêm, sửa hoặc xóa đơn hàng mua.
- PurchaseOrder: Lưu trữ thông tin của đơn hàng, thực hiện các thay đổi hoặc xoá dữ liệu khi được yêu cầu.
#### 5.4. Biểu đồ lớp phân tích

![Diagram](https://www.planttext.com/api/plantuml/png/R99DJiCm48NtEOMNgKGla0Mge2nOKL71VeX7nPB_D3DUL8YJiU18N06dIOeTaaMKlFSy-VpYdw_l7GkG96URtWApkW_E6MOJFEe75squ8wgFHWqNJk-F-quTXOm_ZRe7XxNINwSyWsHl7zARnT43hG-9-dTWV2ADr6v6FKMTiwkMHel_hSzcOZwUMT3Db7b3adZ1auZGomiZTQjR76EHGe_CzOT2H0B9wNdaZGg3yTT2WL8jdOaMyHc99RY1frGpWKwzrE9b_IlOj6XIZztc-pIIC3-t6WMClJQmwMggiksLx5q85i6NnRU5d7UwUaIsszlvFtJAWOSJSZC9WrSNSucOc6ncu6Q7NWydy1S00F__0m00)

### 6. Phân tích ca sử dụng Run Payroll
#### 6.1. Xác định các lớp phân tích
- SystemClock: Đồng hồ hệ thống kích hoạt quy trình chạy bảng lương vào đúng thời điểm.
- System: Xử lý quy trình chạy bảng lương, bao gồm việc tính lương, trích xuất các thông tin thời gian làm việc và bán hàng.
- Payroll: Đối tượng đại diện cho bảng lương của nhân viên.
- Employee: Cung cấp thông tin về thời gian làm việc, tiền lương, và các khoản trừ lương (nếu có).
#### 6.2. BIểu đồ tuần tự

![Diagram](https://www.planttext.com/api/plantuml/png/R951JWCn34NtEOKlm0LcWIeg5YoGAk029Z6jLKyIsHxGd8q5H-8AP3gTqf6QJIBd_vVl-FVxPsEEwaCleRQT8rVC3g-ZEVLRAV48Q70wt12iIezzbJ8IhOex7BM8X32pxkxFpWxUbFTxKgYp0dJ8ORwRL0kiWnToPVea-2fwX4CPr01p0aCXWuIELxRpSnriKU8Ww7JXVnG5MYAYdABrr2A-Zv1OAJeagiNO0xJrptp0V5n2FsLsdgXh1xXYDepE9GSIesjuF53xl3NpadEdt5GjuwoYd6vryuojzQMHDe-g9P8PfR1fZcbuVm000F__0m00)

#### 6.3. Nhiệm vụ từng lớp
- SystemClock: Kích hoạt quy trình tính lương vào thời điểm quy định.
- System: Xử lý các bước tính toán lương và thực hiện các thao tác chuyển khoản hoặc in phiếu lương.
- Payroll: Đại diện bảng lương của nhân viên, bao gồm các phương thức để tính toán và lưu dữ liệu lương.
- Employee: Cung cấp thông tin cần thiết cho quá trình tính lương.
#### 6.4. Biểu đồ lớp phân tích

![Diagram](https://www.planttext.com/api/plantuml/png/R58nJiGm4Epz2fUXk0-uG0SS1Tr9XqHjx2L4iRsvNRk842-Zu4by0IUnoGLmPStEpinw_VNnkUUeAIRlX76QMPv6Zk3l79fUlWavdTXvKFAW8ppcsuAz49mJ13CgUOhKXRPGgMjReACU2PrhhiIxsEXMoMmQ4szxAOMrRqO6GWFC6VKGOWD-S3X2pd9VRXVwfRKQ37ey0dLeb-0Bs1BEQXd3zEmA6Y3-mIpOP6A7WRUuqSuabmN_2wDgY8NhDVKtV5nc0Dla-YsY0ntMrBMtngwg3uVjsxnY8dv2wi5k0x5sy2jZ2t5Yvh7rv5baikNbQdUxwxeILRV6XJ4NwtkgTMOM5Pm8Fz6LJ0miRVRBtmAzs4EmquVw1W00__y30000)
