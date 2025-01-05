### Lab3: Identify design elements
#### 1. Subsystem context diagrams

PrintService
Mô tả: PrintService được sử dụng để in các tài liệu cần thiết, chẳng hạn như phiếu lương của nhân viên hoặc hóa đơn giao dịch. Hệ thống này kết nối với Payroll System để lấy thông tin về các tài liệu cần in, sau đó gửi tài liệu tới máy in.
Các thành phần và đối tượng liên quan:
Payroll System: Gửi thông tin tài liệu cần in và nhận phản hồi về quá trình in.
Printer (Máy in): Thiết bị được sử dụng để in các tài liệu mà hệ thống PrintService gửi tới.
![Diagram](https://www.planttext.com/api/plantuml/png/j59B2eCm5Dpd50zN5cfejo8Yj1jtGa-GQeI09f94QMXxiYvwf5wXyPDIjTjca_UPoGn3NezdeZIHkgqhb5T4ASY8aQAg3eBh_gOIhWY68ri-BVqDkYF4kAQo93c5D9EsEL7PCTivVDCFZo9lQygrNqm5X4x2hROZqYhPrLYbl1Io9fe9FaXDrhvLeaYrPsMKfhNbYuk9utyeMnJJPadyZ5SaXDO1UZkCznu4GRn8AXpreHafu9mgw1X1S-pqI7J3U1R40jQBBCt-GAnz9vGN_Izu0m00__y30000)




 Project Management Database
 Mô tả: ProjectManagementDatabase là hệ thống cơ sở dữ liệu lưu trữ thông tin về các dự án, bao gồm mã số dự án, chi tiết thanh toán và thông tin liên quan khác. Payroll System kết nối với hệ thống này để lấy thông tin về dự án, phục vụ cho các quy trình thanh toán hoặc kiểm tra chi phí.
Các thành phần và đối tượng liên quan:
Payroll System: Lấy thông tin dự án từ ProjectManagementDatabase khi cần tính lương hoặc chi phí liên quan.
Project Management Database: Cơ sở dữ liệu chứa thông tin về các dự án của công ty.



![Diagram](https://www.planttext.com/api/plantuml/png/j59B2i8m4Dtd58Ch1IswBQK8kd4Xz0fZEqgaJJIPYaKzcGkFv1LiQskBOd5ZDfdCvxqtZzoljwbbD9mciGXZj1O2p8oEuvbMNDnau2IWF8ROI3fGOFIMGfuZOtyWBa98nMJM618igjeI5Mue8LLshT3I2sL3t0ROFUF575m8wdW8TLgjTQkGlqo2BBKgUIl1NoazpwOhcrccf00yPhx_3navfUIi6NjFDEr2VBhR6plEf0UZaT_bdfkxlq_9SYq9ehm41ucYOwh2ziwEyzscBe12LRFNZusjVQUaek9hFG000F__0m00)



**2. Analysis class to design element map**



![image](https://github.com/user-attachments/assets/fadaff50-054c-4004-b1dd-188ae589244d)




**3. Design Element to Owning Package Map**

![image](https://github.com/user-attachments/assets/c1a86372-2b41-4ab9-8de1-5a25e7323634)




**4. Architectural layers and their dependencies**

![Diagram](https://www.planttext.com/api/plantuml/png/R99DJiCm48NtSmgh6rQz0kfFG49gH6a56zI5cmxH26Scibsg2d4o5Xo9Av3QQOZJxkoPUS-Zx_dt-sVYlBP-Nnc0MXVlkaGrMbfqo5vx4bOBVKGxKf-WrElpWvfBLGitNRTHfzAzsAezlX0Ut0Q-UaxJkZPKN1hDXRqLOz2ssZNQ3ogmlIKoAQb8NMTxHupE9PPtxCdJsI6JIXEhN7PesbAdMkqD3lPSDekGyyW59gOhhCMH5_jlF7qSQ3FjzLQxL9WVrq-Bg5YAywN5xfuBbvBDWicDol2DcBXKEwoHTyq6pLDgY_w0oCgSB1qCmO_7job3EESGEXrCQ3E9vIjK8KqYZ7KWePTAwAHGuOfXd1kIXbuuOI312iEmubk1CmmI2At85k98BFKONvUScSEaWHn--ny0003__mC0)
