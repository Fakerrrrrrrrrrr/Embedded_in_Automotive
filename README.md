# Bài 1: Setup project đầu tiên trên keilC

<details>
<summary> Details </summary>

## 1.KeilC

<details>
<summary> Details </summary>

![KeilC](https://github.com/Fakerrrrrrrrrrr/Embedded_in_Automotive/blob/main/Images/KeilC.png)

KeilC (hay được gọi là Keil C hoặc Keil uVision) là một công cụ phát triển phần mềm tích hợp (IDE - Integrated Development Environment) được sử dụng để lập trình và phát triển phần mềm nhúng cho các vi điều khiển. KeilC được phát triển bởi công ty Keil, hiện thuộc sở hữu của ARM Holdings, và thường được sử dụng để lập trình các vi điều khiển dựa trên kiến trúc ARM, đặc biệt là các dòng vi điều khiển 8051 và ARM Cortex.

**Các thành phần chính của KeilC**:

- uVision IDE:<br>
Đây là môi trường phát triển tích hợp, cung cấp giao diện để viết mã, biên dịch chương trình, và gỡ lỗi các ứng dụng nhúng. Nó bao gồm trình biên tập mã nguồn và các công cụ khác giúp lập trình viên dễ dàng quản lý các dự án.
- C Compiler (Trình biên dịch C):<br>
KeilC cung cấp trình biên dịch ngôn ngữ lập trình C/C++, cho phép viết mã chương trình bằng ngôn ngữ C và biên dịch nó thành mã máy cho vi điều khiển.
- Assembler (Trình hợp dịch):<br>
Hỗ trợ viết mã Assembly và biên dịch mã Assembly thành mã máy. Đây là công cụ hữu ích cho các tình huống cần kiểm soát chi tiết phần cứng ở mức thấp.
- Debugger (Trình gỡ lỗi):<br>
KeilC tích hợp trình gỡ lỗi mạnh mẽ, giúp lập trình viên kiểm tra và sửa lỗi chương trình trên mô phỏng hoặc trên phần cứng thực. Trình gỡ lỗi có thể tương tác với các bo mạch thực tế để kiểm tra chương trình trên vi điều khiển.
- Simulator (Trình mô phỏng):<br>
Keil cung cấp công cụ mô phỏng, cho phép lập trình viên kiểm tra các chương trình của họ mà không cần phần cứng thực. Trình mô phỏng có thể mô phỏng các trạng thái và phản ứng của vi điều khiển.

**Các tính năng nổi bật của KeilC**:

- **Hỗ trợ nhiều vi điều khiển**: KeilC hỗ trợ nhiều dòng vi điều khiển, bao gồm các dòng 8051, ARM7, ARM Cortex-M, và các vi điều khiển khác dựa trên kiến trúc ARM.
- **Quản lý dự án**: Hỗ trợ quản lý dự án lớn, cho phép người dùng dễ dàng tổ chức mã nguồn và các tệp tin liên quan.
- **Tích hợp trình biên dịch và gỡ lỗi**: Giúp quá trình phát triển và thử nghiệm chương trình trở nên hiệu quả hơn.
- **Khả năng mô phỏng và gỡ lỗi trên phần cứng**: Đây là tính năng quan trọng giúp lập trình viên có thể kiểm tra chương trình trực tiếp trên vi điều khiển thực tế.

**Ứng dụng của KeilC**:

KeilC thường được sử dụng trong phát triển các ứng dụng nhúng, chẳng hạn như:

- Các hệ thống điều khiển thời gian thực (RTOS).
- Các ứng dụng IoT (Internet of Things) dựa trên vi điều khiển ARM.
- Các dự án phát triển phần mềm cho các thiết bị nhúng như điện thoại, máy tính bảng, hệ thống nhúng công nghiệp, thiết bị y tế, và nhiều hệ thống nhúng khác.

</details>

</details>
