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

## 2. Blink Led PC13

<details>
<summary> Details </summary>

![BlinkLedPC13](https://github.com/Fakerrrrrrrrrrr/Embedded_in_Automotive/blob/main/Images/BlinkLedPC13.png)

Trên con vi điều khiển STM32 có các chân A0, A1, A2,... đó là các chân GPIO tổ chức thành các bộ như GPIOA, GPIOB, GPIOC,... mỗi bộ gồm 16 chân là từ chân 0 đến chân 15, các chân có nhiều chức năng, chức năng cơ bản là xuất và nhận điện áp. Ví dụ này xuất ra được điện áp để điều kiển con Led PC13.<br>

Để GPIO hoạt động được cần phải cấp xung clock để GPIO hoạt động. Con vi điều khiển sẽ hoạt động dựa trên giao động được tạo ra bởi thạch anh hay được tạo ra bởi bộ giao động nội.

PC13 có nghĩa là Port ở GPIOC thuộc chân số 13.

Hiện nay thời đại phát triển, mọi con vi điều khiển hầu hết đều có thư viện nên ít khi gặp trường hợp phải code trực tiếp trên thanh ghi. Code bằng thanh ghi chủ yếu để hiểu cách ngoại vi được cấu hình.

- APB2 được cấu hình bởi thanh ghi APB2 peripheral clock enable register (RCC_APB2ENR.)
- Bit IOPCEN điều khiển xung cấp cho GPIOC

![APB2ENR](https://github.com/Fakerrrrrrrrrrr/Embedded_in_Automotive/blob/main/Images/APB2.png)

Các bit từ 0 đến 15 sẽ chịu trách nhiệm cấu hình xung clock cho ngoại vi, bit số 4 là bit IOPCEN để cấu hình cho cái xung clock của GPIOC. Ghi IOPCEN lên 1 là đã cấp xung.

- **Cấu hình chế độ chân GPIO**

Port configuration register low (GPIOx_CRL): cấu hình cho các chân từ 0-7 trong Portx

![GPIOx_CRL](https://github.com/Fakerrrrrrrrrrr/Embedded_in_Automotive/blob/main/Images/GPIOx_CRL.png)

Port configuration register low (GPIOx_CRH): cấu hình cho các chân từ 8-15 trong Portx

![GPIOx_CRH](https://github.com/Fakerrrrrrrrrrr/Embedded_in_Automotive/blob/main/Images/GPIOx_CRH.png)

Mỗi GPIO có 16 chân, mỗi chân được quyết định bởi 4 bit, nên để đủ 16 chân thì cần 64 bit, cấu trúc vi điều khiển chỉ cần 32 bit nên phải chia đôi ra thành 2 thanh ghi CRH và CRL, GPIOx_CRL sẽ cấu hình cho chân từ 0-7, GPIOx_CRH sẽ cấu hình cho chân từ 8-15 (Thay x bằng A,B,C,...).

Ở đây dùng PC13 nên sẽ quan tâm tới CNF13 và MODE13, mỗi phần chứa 2 bit và tùy thuộc giá trị ghi vào 4 bit rw (read write).

![8-15](https://github.com/Fakerrrrrrrrrrr/Embedded_in_Automotive/blob/main/Images/8_15_leg.png)

Code điều khiển PC13 với Mode_11 và CNF_00:
```c
int main(){
  RCC->APB2ENR |= RCC_APB2ENR_IOPCEN| RCC_APB2ENR_IOPAEN;

  GPIOC->CRH |= GPIO_CRH_MODE13_0;  //MODE[1:0] = 11: Output mode, max speed 50 MHz.
  GPIOC->CRH |= GPIO_CRH_MODE13_1;
  GPIOC->CRH &= ~GPIO_CRH_CNF13_0;  //CNF13[1:0] = 00: General purpose output push-pull.
  GPIOC->CRH &= ~GPIO_CRH_CNF13_1;
  while(1){
  
  }
  return 0;
}
```

Port output data register (GPIOx_ODR).
- Gồm 16 bits (ODR0->ODR15) ứng với giá trị logic trên chân tương ứng trong Portx.

```c
int main(){
  RCC->APB2ENR |= RCC_APB2ENR_IOPCEN| RCC_APB2ENR_IOPAEN;

  GPIOC->CRH |= GPIO_CRH_MODE13_0;  //MODE[1:0] = 11: Output mode, max speed 50 MHz.
  GPIOC->CRH |= GPIO_CRH_MODE13_1;
  GPIOC->CRH &= ~GPIO_CRH_CNF13_0;  //CNF13[1:0] = 00: General purpose output push-pull.
  GPIOC->CRH &= ~GPIO_CRH_CNF13_1;
  while(1){
    GPIOC->ODR |= 1<<13;
    delay(10000000);
    GPIOC->ODR &= ~(1<<13);
    delay(10000000);
  }
  return 0;
}
```

Delay();<br>
Hàm delay được tạo bằng cách cho MCU không làm gì trong 1 khoảng thời gian bằng các vòng lặp.
```c
void delay(__IO uint32_t timedelay){
  for(int i = 0; i<timedelay; i++){}
}
```

</details>

## 3. Tổng kết & mở rộng

<details>
<summary> Details </summary>

- Việc code trên thanh ghi  giúp hiểu rõ cách hoạt động chi tiết của từng ngoại vi.
- Hiện nay các hãng sản xuất đều cung cấp bộ thư viện chuẩn cho từng MCU, trong đó các API được phát triển để người dùng dễ tiếp cận hơn.<br>
->> Nên sử dụng thư viện chuẩn để code dễ dàng hơn.

</details>

## 4. Đọc trạng thái nút nhấn để điều khiển Led.

<details>
<summary> Details </summary>

- Pin được chọn là PA0 (ODR: Output Data Register)

![Button_PA0](https://github.com/Fakerrrrrrrrrrr/Embedded_in_Automotive/blob/main/Images/Button_PA0.png)

- Lắp nút nhấn theo kiểu Pull-Up Resistor
- Cấu hình ban đầu trạng thái chân PA0 sẽ là mức 1. PA0 kiểu Input Push Pull.
- Set GPIOA_ODR lên 1. 

```c
RCC->APB2ENR |= RCC_APB2ENR_IOPAEN; //Kich hoat xung clock cap cho GPIOA
											
GPIOA->CRL &= ~GPIO_CRL_MODE0_0; 	//MODE = 00: Intput mode.
GPIOA->CRL &= ~GPIO_CRL_MODE0_1; 
GPIOA->CRL |= GPIO_CRL_CNF0_1;	 //CNF = 10: Input with pull-up / pull-down
GPIOA->CRL &= ~GPIO_CRL_CNF0_0;	       
GPIOA->ODR |= GPIO_ODR_ODR0;
```

Do cấu hình cho chân PA0 nên sẽ là CRL, MODE = 00, CNF = 10, ODR = 1 (pull-up). Thanh ghi ODR là để điều khiển xuất dữ liệu ra thanh ghi đó.

**Đọc trạng thái nhấn nút**

Thanh ghi Input Data Register (IDR):
- Nhận mức tín hiệu tại chân của Port.
- Giá trị nút nhấn tại PA0 = bit IDR0 của PortA.

```c
if( ( GPIOA->IDR & (1<<0) ) == 0 ){
     while((GPIOA->IDR & (1<<0)) == 0);
     // Do something.

     }
```

Đầu tiên nếu nhấn nút thì GPIOA->IDR sẽ bằng 0 sẽ chạy vào trong phần câu điều kiện, còn vòng lặp while để đến khi nào thả nút nhấn đó ra thì mới thực hiện câu lệnh mong muốn để tránh trường hợp thực hiện câu lệnh nhiều lần.

</details>

</details>


# Bài 2: GPIO

<details>
<summary> Details </summary>

## 1. Thư viện STM32F10x Standard Peripherals Firmware Library

<details>
<summary> Details </summary>

Thư viện STM32F10x là thư viện được phát triển cho dòng STM32. Đầy đủ driver cho tất cả các ngoại vi tiêu chuẩn. Thư viện này bao gồm các hàm, cấu trúc dữ liệu và marco được define từ trước để giúp việc cấu hình các ngoại vi đơn giản hơn mà không cần phải vào tới từng thanh ghi đọc các document để xem thanh ghi đó có chức năng gì.

Các bước cấu hình ngoại vi (GPIO)

**Cấp clock cho ngoại vi** (RCC) -> **Cấu hình ngoại vi** (CRH-CRL) -> **Sử dụng ngoại vi** (ODR-IDR)

Cấp xung clock cho GPIO: Sử dụng các API được cung cấp sẵn cho từng Bus. Các ngoại vi trên Bus được cấp xung thông qua việc truyền các tham số vào API. Vì sử dụng led PC13 nên cấp xung cho GPIOC qua Bus APB2.

**Cấp clock cho ngoại vi** :Để cấp xung cho ngoại vi ứng với Bus sẽ có 3 hàm:
```
void RCC_AHBPeriphClockCmd(uint32_t RCC_AHBPeriph, FunctionalState NewState);		//Cấp xung cho ngoại vi với Bus AHB
void RCC_APB2PeriphClockCmd(uint32_t RCC_APB2Periph, FunctionalState NewState);		//Cấp xung cho ngoại vi với Bus APB2
void RCC_APB1PeriphClockCmd(uint32_t RCC_APB1Periph, FunctionalState NewState);		//Cấp xung cho ngoại vi với Bus APB1
```

Cấu hình:
```
void RCC_Config(void){
     RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOC, ENABLE);	//Nếu muốn dùng ngoại vi, cấp clock cho các ngoại vi đó dùng toán tử | ví dụ "RCC_APB2Periph_GPIOC| RCC_APB2Periph_GPIOA"
     RCC_APB1PeriphClockCmd(RCC_APB1Periph_TIM2, ENABLE);
}
```

**Cấu hình ngoại vi**: Để cấu hình cho GPIO ta dùng Struct GPIO_InitTypeDef, cụm từ InitTypeDef sẽ dùng chung để cấu hình cho SPI,GPIO,... để cấu hình cho nó với struct có các biến thành viên khác nhau (cũng có thể hiểu là khởi tại kiểu mặc định).<br>
Ở đây GPIO_InitTypeDef sẽ chứa các biến thành viên như là GPIO_Pin (Chọn Pin), GPIO_Mode (Chọn Mode), GPIO_Speed (Tốc độ đáp ứng).
```
void GPIO_config(){
	GPIO_InitTypeDef GPIO_InitStruct;
	
	GPIO_InitStruct.GPIO_Pin = GPIO_Pin_13;			//Nếu muốn dùng nhiều chân thì sử dụng toán tử OR(|) để thiết lập nhiều chân ví dụ "GPIO_Pin_13| GPIO_Pin_14| GPIO_Pin_15" lưu ý nó phải cùng chế độ và trên GPIOC, nếu muốn dùng GPIOA thì ghi đè struct tạo ra.
	GPIO_InitStruct.GPIO_Mode = GPIO_Mode_Out_PP;
	GPIO_InitStruct.GPIO_Speed = GPIO_Speed_50MHz;
	
	GPIO_Init(GPIOC, &GPIO_InitStruct);

	//PA13
	GPIO_InitStruct.GPIO_Pin = GPIO_Pin_13;
	GPIO_InitStruct.GPIO_Mode = GPIO_Mode_IN_FLOATING;
	GPIO_InitStruct.GPIO_Speed = GPIO_Speed_10MHz;

	GPIO_Init(GPIOA, &GPIO_InitStruct);
}
```


</details>

</details>

# Bài 3: Interrupt - Timer

<details>
<summary> Details </summary>


</details>

# Bài 4: Các chuẩn giao tiếp cơ bản

<details>
<summary> Details </summary>


</details>

# Bài 5: SPI Software & Hardware

<details>
<summary> Details </summary>


</details>

# Bài 6: I2C Software & I2C Hardware

<details>
<summary> Details </summary>


</details>

# Bài 7: UART Software & Hardware

<details>
<summary> Details </summary>


</details>

# Bài 8: Interrupt

<details>
<summary> Details </summary>


</details>

# Bài 9: ADC

<details>
<summary> Details </summary>


</details>

# Bài 10: DMA

<details>
<summary> Details </summary>


</details>
