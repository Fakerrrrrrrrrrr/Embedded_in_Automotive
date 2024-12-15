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
Ở đây GPIO_InitTypeDef sẽ chứa các biến thành viên như là GPIO_Pin (Chọn Pin), GPIO_Mode (Chọn Mode), GPIO_Speed (Tốc độ đáp ứng).<br>
Ngoài ra thì ta có thể ghi đè biến GPIO_InitStruct nếu có cấu hình các chân tương tự, những gì liên quan đến GPIO sẽ được đưa vào 1 hàm GPIO_config. Tương tự với các ngoại vi khác đều được code như bên dưới.
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

**Sử dụng GPIO**:Khi vào {}Function ở stm32f10x_gpio.c thì sẽ có các hàm để sử dụng ngoại vi.<br>
Sau đây là các hàm thông dụng:
```
//Đọc tín hiệu trên 1 chân trong GPIO được cấu hình là INPUT(ngỏ vào) tương ứng 1 bit: Tham số sẽ là GPIO với chân GPIO đó
uint8_t GPIO_ReadInputDataBit(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin);
//Đọc tín hiệu trên 16 chân trong GPIO được cấu hình là INPUT(ngỏ vào) tương ứng 16 bit: Tham số sẽ là GPIO
uint16_t GPIO_ReadInputData(GPIO_TypeDef* GPIOx);
//Đọc tín hiệu trên 1 chân trong GPIO được cấu hình là OUTPUT(ngỏ ra) tương ứng với 1 bit: Tham số sẽ là GPIO với chân GPIO đó
uint8_t GPIO_ReadOutputDataBit(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin);
//Đọc tín hiệu trên 16 chân trong GPIO được cấu hình là OUTPUT(ngỏ ra) tương ứng 16 bit: Tham số sẽ là GPIO
uint16_t GPIO_ReadOutputData(GPIO_TypeDef* GPIOx);
//Đặt 1 số chân trên GPIO về mức 1 có thể chọn nhiều chân bằng phép OR: Tham số sẽ là GPIO với chân GPIO đó
void GPIO_SetBits(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin);//0b0000….0010
//Đặt 1 số chân trên GPIO về mức 0 có thể chọn nhiều chân bằng phép OR: Tham số sẽ là GPIO với chân GPIO đó
void GPIO_ResetBits(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin);
//Hàm này cho phép ghi giá trị tùy ý lên 1 chân tương ứng 1 bit
void GPIO_WriteBit(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin, BitAction BitVal);
//Hàm này cho phép ghi giá trị tùy ý lên 16 chân tương ứng 16 bit
void GPIO_Write(GPIO_TypeDef* GPIOx, uint16_t PortVal);
```
Sử dụng hàm SetBits và ResetBits để tạo hàm blink led như bài trước.
```
while(1){
	GPIO_SetBits(GPIOC, GPIO_Pin_13); // Ghi 1 ra PC13
	delay(10000000);
	GPIO_ResetBits(GPIOC, GPIO_Pin_13);// Ghi 0 ra PC13
	delay(10000000);
}
```
Thêm 1 số ví dụ về nháy đuổi led, sẽ cấu hình cho chân 5 đến chân 8 của GPIOC. Nhìn thấy cùng chế độ với GPIO_Pin_13 nên ta có thể dùng phép OR cho tất cả các Pin.
```
GPIO_InitTypeDef GPIO_InitStructure;
GPIO_InitStructure.GPIO_Pin = GPIO_Pin_5|GPIO_Pin_6|GPIO_Pin_7|GPIO_Pin_8;
GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	
GPIO_Init(GPIOC, &GPIO_InitStructure);
```
Hàm nháy đuổi sử dụng hàm GPIO_Write ghi cùng lúc 16 chân, loop là số lần nháy đuổi, biến Ledval để điều khiển, mỗi lần nháy đuổi thì sẽ đặt giá trị là 1 tại vị trí GPIO4 và mỗi lần lặp thì sẽ dịch sang 1 bit GPIO5->GPIO6->GPIO7->GPIO8 mỗi lần led sẽ sáng 1 chân.
```
void chaseLed(uint8_t loop){
	uint16_t Ledval;
	for(int j=0; j<loop; j++ ){
		Ledval = 0x0010;
		for(int i =0; i<4; i++)
		{
			Ledval = Ledval<<1;
			GPIO_Write(GPIOC, Ledval);
			delay(10000000);
		}
	}
}
int main(){
	while(1){
		chaseLed(3);
		break;
	}
}
```
Nếu quá nhanh thì delay không đủ, phần sau học về Timer sẽ chuẩn hơn.<br>

**Đọc trạng thái nút nhấn**: Tương tự thì ta đọc trạng thái nút nhấn dựa trên các hàm. Cấu hình 1 phân GPIOA vì chân cần sử dụng ở đây là PA0 nhận tín hiệu đầu vào (INPUT).
```
GPIO_InitTypeDef GPIO_InitStructure;
GPIO_InitStructure.GPIO_Pin = GPIO_Pin_0;
GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;

GPIO_Init(GPIOA, &GPIO_InitStructure);
```
Kiểm tra xem PA0 có đang bằng không hay không bằng cách dùng GPIO_ReadInputDataBit so sánh với 0 hoặc Bit_RESET.
```
if(GPIO_ReadInputDataBit(GPIOA, GPIO_Pin_0)==0)
	{
		while(GPIO_ReadInputDataBit(GPIOA, GPIO_Pin_0)==0);
		//do something
		if(GPIO_ReadOutputDataBit(GPIOC, GPIO_Pin_13)){
			GPIO_ResetBits(GPIOC, GPIO_Pin_13);
		} else {
			GPIO_SetBits(GPIOC, GPIO_Pin_13);
	}
}

```

</details>

</details>

# Bài 3: Interrupt - Timer

<details>
<summary> Details </summary>

## 1. Ngắt:
Ngắt là 1 sự kiện khẩn cấp xảy ra trong hay ngoài vi điều khiển. Nó yêu cầu MCU phải dừng chương trình chính và thực thi chương trình ngắt.<br>
Trong hàm main sẽ có 1 vòng lặp while(1), khi không có gì xảy ra thì nó sẽ chạy ở trong while(1) nếu có sự kiện khẩn cấp xảy ra thì chương trình trong main sẽ lập tức dừng lại và chuyển tới thực hiện một chương trình ngắt sau khi xử lý xong nó sẽ quay lại chỗ được tạm dừng ở chương trình chính để thực hiện tiếp tục đoạn code. <br>
Ví dụ như trên chiếc xe hơi thì chương trình chính là chương trình khi xe hoạt động bình thường khi mình lái, nghe nhạc,... ví dụ trên đầu xe có cảm biến va chạm, mà xe sắp tông vào cột điện thì cảm biến va chạm nó sẽ báo cho con vi điều khiển biết xe sắp va chạm nên tạo ra 1 ngắt, thực hiện cho xe ngừng hoạt động hoặc phanh gấp or đảo lái, hoặc bung túi khí,... khi xe dừng hẳn mà cảm biến không báo nguy hiểm nữa thì xe lại chạy hoạt động lại bình thường. Hoặc khi chơi game chương trình chính window đang chạy mà nó nhận thấy nhiệt độ đang lên cao ngoài mức cho phép thì máy tính sẽ tự động tắt nguồn.<br>

Các loại ngắt thông dụng:<br>

Mỗi ngắt có 1 trình phục vụ ngắt, sẽ yêu cầu MCU thực thi lệnh tại trình phục vụ ngắt khi có ngắt xảy ra.(Thì nó là 1 hàm cố định bất cứ khi nào có ngắt tương ứng với hàm đó thì tự động gọi nó ra)<br>
Các ngắt có các địa chỉ cố định trong bộ nhớ để giữ các trình phục vụ. Các địa chỉ này gọi là vector ngắt.

|Ngắt|Cờ ngắt|Địa chỉ trình phục vụ ngắt| Độ ưu tiên ngắt|
|------|-------|--------------------------|----------------|
|Reset|-|000h|-|
|Ngắt ngoài|IE0|0003h|Lập trình được|
|Timer1|TF1|001Bh|Lập trình được|
|Ngắt truyền thông| | | |

Địa chỉ trình phục vụ ngắt (vector ngắt) chỉ là ví dụ, còn cờ ngắt đó là các bit ngắt, flag ngắt.

Ngắt reset xảy ra khi ta nhấn nút reset trên con vi điều khiển, hoặc rút nguồn điện sau đó cắm điện lại nó sẽ chạy chương trình lại từ đầu.<br>

![ProgramCounter](https://github.com/Fakerrrrrrrrrrr/Embedded_in_Automotive/blob/main/Images/Interrupt_PC.png)

Để nắm được cách hoạt động khi chương trình có ngắt thì phải biết tới Program Counter (Thanh ghi PC) thanh ghi này luôn chỉ đến lệnh tiếp theo trong chương trình. Khi chương trình nạp vào con stm32 thì từng cái lệnh hợp ngữ sẽ lưu vào từng ô nhớ vào bộ nhớ Flash của con stm32.<br>
Khi mà CPU đọc lệnh chạy thì thanh ghi PC nó sẽ trỏ vào vị trí đầu tiên (khi khởi động lên) 0xC1 rồi hàm main sẽ đi được bao nhiêu dòng code thì thanh ghi PC nó sẽ thực hiện các lệnh hợp ngữ tiếp theo ở trong vòng while(1) thì lặp lại vòng lặp mới 0xC1. Có các chương trình ngắt khác như là ngắt ngoài có vector ngắt địa chỉ sẽ được lưu tại 0xB5-B9 và 1 chương trình khác thì là 0xD3-0xD7.<br>
Ví dụ ở 0xC2 xảy ra ngắt thì CPU biết khi có ngắt xảy ra thì tạm dừng chương trình chính lại để chạy chương trình ngắt nhận diện được đây là ngắt và có vector 0xB5-B9 thì nó tạm thời đưa PC của nó tới 0xB5 sau khi chạy xong lệnh 0xC2 thì PC sẽ trỏ tới lệnh tiếp theo 0xB6 và thực hiện 0xB5 cứ thế chạy đến 0xB9 thì PC sẽ trỏ tới 0xC3 và chương trình lại tiếp tục ngay tại vị trí 0xC3 rồi chạy lại bình thường.<br>

### 1.1 Ngắt ngoài:

![ExternalInterrupt](https://github.com/Fakerrrrrrrrrrr/Embedded_in_Automotive/blob/main/Images/External_Interrupt.png)

Xảy ra khi có thay đổi điện áp trên các chân GPIO được cấu hình làm ngõ vào ngắt.<br>

Ví dụ trên thì cấu hình cho chân GPIO làm ngõ ngắt ngoài, lắp 1 nút nhấn khi nhấn nút điện áp sẽ thay đổi trên chân GPIO đó thì nó sẽ sinh ra 1 ngắt ngoài. Và có 4 kiểu ngắt ngoài. Các ngắt sẽ sinh ra khi ở các trạng thái khác nhau.

- LOW: kích hoạt ngắt liên tục khi chân ở mức thấp.
- HIGH: Kích hoạt liên tục khi chân ở mức cao.
- Rising: Kích hoạt khi trạng thái trên chân chuyển từ thấp lên cao.
- Falling: Kích hoạt khi trạng thái trên chân chuyển từ cao xuống thấp.

Thông thường chân sẽ có 2 giá trị là 1 và 0 tương ứng 3V3 và 0V

### 1.2 Ngắt Timer:

Ngắt Timer xảy ra khi trong thanh ghi đếm của timer tràn. Giá trị tràn được xác định bởi giá trị cụ thể trong thanh ghi đếm của timer. (Timer đơn giản là 1 bộ đếm, đếm lên hoặc đếm xuống sau khoảng thời gian nhất định ví dụ cấu hình sau mỗi 1ms thì nó sẽ đếm lên 1 thì thanh ghi đếm cứ sau 1ms sẽ tăng lên 1 đơn vị, thanh ghi đếm là thanh ghi đếm nhị phân, thanh ghi đếm tràn là khi giá trị nó đếm bằng với giá trị mình thiết lập cho nó (200 lần chẳng hạn) khi tràn thì sẽ tạo ra 1 ngắt Timer (Hàm ngắt cho Timer được gọi).

Vì đây là ngắt nội trong MCU(nội trong con vi điều khiển) không phụ thuộc tín hiệu bên ngoài, nên phải reset giá trị thanh ghi timer để có thể tạo được ngắt tiếp theo. Ở ví dụ uint8_t thì sẽ đếm từ 0-255 thì nó mới reset thay vì 200 nếu nó không phải là uint8_t mà là uint16_t hoặc uint32_t thì nó sẽ đếm thêm gấp mấy lần mới reset rồi mới đếm tới giá trị 200, nên để tránh xảy ra sai sót thì ta nên reset giá trị của thanh ghi đếm về 0 sau mỗi lần ngắt.

## 1.3 Ngắt truyền thông:

![Communication_Interrupt](https://github.com/Fakerrrrrrrrrrr/Embedded_in_Automotive/blob/main/Images/Communication_Interrupt.png)

Ngắt truyền thông xảy ra khi có sự kiện truyền/nhận dữ liệu giữa MCU với các thiết bị bên ngoài hay với MCU. Ngắt này sử dụng cho nhiều phương thức như Uart, SPI, I2C…v.v nhằm đảm bảo việc truyền nhận chính xác. Hầu như tất cả các giao thức hỗ trợ trên con stm32 đều có ngắt truyền thông, có nghĩa mỗi giao thức đều có ngắt riêng của nó.<Br>

Ở ví dụ trên mình sẽ có 2 con vi điều khiển nối với nhau qua 1 giao thức là UART. Thì trong vi điều khiển không phải lúc nào cũng là truyền và nhận dữ liệu (truyền qua UART) thì trong chương trình còn các công việc khác để nó làm nữa ví dụ func1, func2,... và các hàm sẽ mất thời gian để nó thực hiện. Ở MCUA và MCUB đều có func1 nhưng ở MCUA lại mất 2s để thực hiện thay vì 1s ở MCUB thì hàm nhận sẽ gọi trước hàm truyền và thực hiện xong rồi thì MCUA mới truyền dữ liệu thì dữ liệu sẽ bị mất khi MCU thực hiện nhiều công việc nếu cùng thời gian thì vô tình nó sẽ đúng. Hoặc là chỉ nhận 0.5s dữ liệu thì cũng bị mất 0.5s dữ liệu. Nên để đảm bảo khi con MCUA truyền thì con MCUB nhận thì dùng ngắt truyền thông.

Tạo ra 1 chương trình ngắt UART hoạt động khi MCUA truyền dữ liệu thì chương trình ở MCUB sẽ dừng và chuyển qua chương trình ngắt Timer, hành động này xảy ra rất là nhanh nên sẽ được coi là cùng lúc với lúc truyền dữ liệu bây giờ đơn giản ở hàm ngắt được gọi nó sẽ gọi hàm nhận.

## 1.4 Độ ưu tiên ngắt:

Độ ưu tiên ngắt là khác nhau ở các ngắt. Nó xác định ngắt nào được quyền thực thi khi nhiều ngắt xảy ra đồng thời.(Quyết định ngắt nào được thực hiện trước và ngắt nào được thực hiện sau)<br>
STM32 quy định ngắt nào có số ưu tiên càng thấp thì có quyền càng cao. Các ưu tiên ngắt có thể lập trình được.

Ví dụ trên xe ở vừa có cảm biến và chạm và vừa có cảm biến áp suất lốp. Xe đang chạy bị thủng lốp và trong lúc đó xe chuẩn bị đâm vào cột điện thì 2 cảm biến gửi cùng lúc 2 tín hiệu khẩn cấp, thì chiếc xe không biết thực hiện chương trình ngắt nào trước. Nên độ ưu tiên ngắt được sinh ra và được cài đật khác nhau ở các ngắt. Tùy thuộc vào độ khẩn cấp nào cao hơn thì sẽ cho nó độ ưu tiên cao hơn. Cái ngắt ưu tiên xử lý ngắt va chạm trước rồi mới thực hiện ngắt áp suất lốp, số ưu tiên thứ tự càng thấp thì quyền càng cao.<br>

Nên nhớ là ngắt không phải 1 cái function gọi chung nó là 1 trình phụ ngắt. ví dụ chương trình chạy từ 0x01 tới 0x03 và nó đang chạy lệnh 0x03 thì xảy ra ngắt lúc này PC đang trỏ tới 0x04 của chương trình chính thì sẽ thay đổi sang 0xD4 thì sau khi chạy xong tới 0xE2 chẳng hạn, để chương trình đang thực hiện biết được vị trí mà nó dời đi thì sẽ có 1 khái niệm gọi là Stack Pointer (cấu trúc dữ liệu Stack bình thường) thì nó sẽ được dùng để lưu các giá trị (PC) (địa chỉ) hiện tại khi chương trình nhảy sang chương trình ngắt khác và PC mới sẽ được cập nhật PC trỏ tới 0xD4 ví dụ ở tại dòng lệnh 0xD6 xảy ra ngắt PC trỏ tới 0xD7 thì nó sẽ tiếp tục lưu PC 0xD7 vào Stack Pointer và nhảy sang chương trình ngắt khác cũng như PC mới sẽ được cập nhật ở chương trình ngắt có độ ưu tiên cao hơn. Sau khi thực hiện xong chương trình ngắt tới dòng lệnh 0xB9 CPU nhận thấy chương trình ngắt sẽ kết thúc và thoát chương trình ngắt thì CPU sẽ vào Stack Pointer với cấu trúc LIFO thì 0xD7 sẽ được lấy ra cập nhật cho PC là 0xD7 và xóa phần tử đó sau đó trong Stack Pointer tiếp tục sau khi tới chương trình chính. Ở đây chỉ nói tới PC.

Trạng thái chương trình sẽ được lưu toàn bộ ở trong 1 stack riêng trong bộ nhớ stack, thực chất MCU chạy sẽ có 15 thanh ghi dùng để toán giá trị cho các biến, thì 15 thanh ghi đó chính là trạng thái chương trình khi 1 biến được dùng để tính toán sẽ thực hiện trên các thanh ghi đó, ví dụ đang tính toán lở dở ở biến a, thì toàn bộ quá trình tính toán lở dở sẽ được lưu hết vào trong bộ nhớ Stack khi chuyển đi sẽ có trạng thái hoàn toàn mới, khi nó khôi phục thì nó khôi phục lại toàn bộ trạng thái chương trình lúc đó luôn chứ không phải khôi phục PC không nên giá trị của biến đó hoàn toàn được bảo toàn (Tham khảo exception handing in stm32).

Nếu 1 ngắt có độ ưu tiên thấp hơn xảy ra trong quá trình thực hiện chương trình ngắt có độ ưu tiên cao hơn thì chương trình ngắt đó sẽ không thực hiện ngay mà nó sẽ vào trạng thái chờ (Pending) (Queue) để xử lý lần lượt hoặc nếu cài đặt cho MCU bỏ qua luôn thì nó sẽ bỏ qua luôn.

Trên là 3 ngắt chính còn về ngắt reset liên quan đến phần Boot của MCU chưa có học nên bỏ qua.

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

# Bài 11: Flash và Bootloader

<details>
<summary> Details </summary>

## 1. Bộ nhớ trong vi điều khiển

<details>
<summary> Details </summary>

### 1. Bộ nhớ RAM (Random Access Memory)

**Định nghĩa**: RAM là loại bộ nhớ tạm thời, cho phép truy cập ngẫu nhiên, tức là bất kỳ ô nhớ nào cũng có thể được truy cập trực tiếp mà không cần phải truy cập qua các ô khác.

**Đặc điểm**: 
- Tốc độ đọc/ghi nhanh.
- Dữ liệu bị mất khi ngưng cấp nguồn.

**Chức năng**: 
- Sử dụng để lưu trữ dữ liệu và chương trình mà CPU đang sử dụng tại thời điểm đó.

**Phân loại**:
- DRAM (Dynamic RAM): Cần phải được làm tươi (refresh) liên tục.
- SRAM (Static RAM): Nhanh hơn DRAM và không cần làm tươi, thường được sử dụng cho cache.

### 2. Bộ nhớ Flash

**Định nghĩa**: Flash là một loại bộ nhớ không bay hơi, cho phép ghi và xóa dữ liệu theo khối.

**Đặc điểm**: 
- Tốc độ ghi chậm.
- Tốc độ đọc nhanh.
- Dữ liệu không bị mất khi ngưng cấp điện.
- Giới hạn số lần xóa/ ghi.
- Chỉ có thể ghi theo khối 2/4 byte.

**Chức năng**: 
- Thường được sử dụng trong các thiết bị lưu trữ như USB flash drives, thẻ nhớ, và ổ SSD.

**Phân loại**:
- NAND Flash: Thường được sử dụng cho lưu trữ dữ liệu.
- NOR Flash: Thường được sử dụng cho firmware.

### 3. Bộ nhớ EPROM

**Định nghĩa**: EPROM là loại bộ nhớ không bay hơi, có thể được lập trình và xóa bằng tia cực tím.

**Đặc điểm**: 
- Tốc độ ghi chậm.
- Tốc độ đọc nhanh.(Nhanh hơn EPROM nhưng chậm hơn RAM.)
- Dữ liệu không bị mất khi ngưng cấp điện.
- Giới hạn số lần xóa/ ghi.
- Chỉ có thể đọc/ghi theo từng byte.

**Chức năng**: 
- Thường được sử dụng để lưu trữ firmware hoặc các chương trình không thay đổi thường xuyên.

**Phân loại**:
- EPROM: Có thể xóa bằng tia UV.
- EEPROM (Electrically Erasable Programmable Read-Only Memory): Có thể xóa bằng điện và cho phép sửa đổi dữ liệu từng byte.

</details>

## 2. FLASH

<details>
<summary> Details </summary>

**Tính chất**:
- Trên STM32F1 không có EPROM mà chỉ được cung cấp sẵn 128/64Kb Flash.
- Được chia nhỏ thành các Page. mỗi Page có kích thước 1Kb. Tương đương với (Page 0 đến Page 127)/(Page 0 đến Page 63).
- Flash có giới hạn về số lần xóa/ghi.
- Trước khi ghi phải xóa Flash trước. Ta sẽ đưa các dữ liệu về 0xFF. Khi xóa chỉ xóa 1 Page, không thể xóa 2 Byte hoặc 4 Byte sau đó ghi dữ liệu theo khối 2/4 Byte.
- Thường được dùng để lưu chương trình. Lưu cho firmware.
- Không mất dữ liệu khi mất nguồn, có cơ chế Lock bảo vệ dữ liệu an toàn khi mất nguồn.

**Vùng nhớ**:
- Vùng nhớ chứa chương trình hệ thống sẽ từ 0x0000 0000 -> 0x0800 0000. Vùng nhớ chứa chương trình người dùng nạp sẽ từ 0x0800 0000 -> 0x0800 0600. Và từ 0x0800 0600 -> 0x0801 FFFF sẽ là vùng nhớ trống.
- Vùng nhớ phía sau từ 0x0800 0000 sẽ là trống và người dùng có thể lưu trữ dữ liệu ở vùng này.
- Thư viện Std cung cấp hàm để giao tiếp với Flash trong Module Flash. File "stm32f10x_flash.h".

**Xóa Page**:
![FlashMemoryPageErase](https://github.com/Fakerrrrrrrrrrr/Embedded_in_Automotive/blob/main/Images/XoaPageFlash.png)

Mỗi lần ghi 2bytes hoặc 4bytes, tuy nhiên mỗi lần xóa phải xóa cả Page.
Sơ đồ xóa FLash như hình:
- Đầu tiên, kiểm tra cờ LOCK của Flash, nếu Cờ này đang được bật, Flash đang ở chế độ Lock và cần phải được Unlock trước khi sử dụng. (Cơ chế bảo mật để người dùng không thể truy cấp random vào khi Lock) (Perform unlock sequence: Thực hiện chuỗi mở khóa)
- Sau khi FLash đã Unlock, cờ CR_PER được set lên 1. (PER viết tắt của Page Erase) (Enable)
- Địa chỉ của Page cần xóa được ghi vào FAR. (Ở mỗi Page đều có địa chỉ riêng, chỉ cần truyền địa chỉ vào FAR để xóa. Ghi vào thanh ghi AR: Address Register địa chỉ cần phải xóa.)
- Set bit CR_STRT lên 1 để bắt đầu quá trình xóa.
- Kiểm tra cờ BSY đợi hoàn tất quá trình xóa. (Cờ busy được viết trên thanh ghi SR:Status Register)

</details>

</details>


# Bài 12: CAN

<details>
<summary> Details </summary>

## 1. Khái niệm

<details>
<summary> Details </summary>

Controller Area Network (CAN) là giao thức giao tiếp **nối tiếp** hỗ trợ mạnh cho những hệ thống điều khiển **thời gian thực phân bố** (distrubuted realtime control system).<br>
CAN đặc biệt được ứng dụng nhiều trong ngành công nghiệp Ô tô.

Ví dụ: Hệ thống túi khí thì độ trễ cho phép là 1ms, 2ms,... Thì hệ thống này đòi hỏi thời gian thực cao sẽ sử dụng CAN. 1 hệ thống va chạm nó sẽ gửi tín hiệu qua đường CAN BUS những phần liên quan thì nó sẽ xử lý.

</details>

## 2. Mạng CAN

<details>
<summary> Details </summary>
	
![Network](https://github.com/Fakerrrrrrrrrrr/Embedded_in_Automotive/blob/main/Images/CANNetwork.png)

CAN có đường dây dẫn đơn giản gồm 2 dây CAN_H và CAN_L, tạo thành 1 Bus, các thiết bị được nối chung trên 2 dây này và gọi là node trong mạng. Ở cuối mỗi đường dây sẽ có 2 con điện trở 120Ω<br>
Sự truyền dữ liệu thực hiện nhờ tính toán vi sai trên cặp dây truyền tín hiệu, có nghĩa là chúng đo sự chênh lệch điện áp giữa CAN_H và CAN_L.



</details>

</details>


# Bài 14: LIN

<details>
<summary> Details </summary>



</details>

# Bài 15: AUTOSAR Classic

<details>
<summary> Details </summary>

1. Định nghĩa

AUTOSAR Classic là Lập trình theo 1 frame, form nhất định, những hàm Init liên quan đến ngoại vi, config các phần RCC, GPIO, TIM, SPI, CAN, UART bằng những hàm riêng lẻ, truyền CAN hoặc gọi ra cảm biến sẽ được viết thành những hàm và những hàm đó sẽ được chạy bên trong 1 vòng lặp while ở trong hàm main.

```c
#include "stm32f10x.h"

void RCC_Config();	//
void GPIO_Config();	//
void TIM_Config();	//  Hàm Init
void SPI_Config();	//
void CAN_Config();	//
void UART_Config();	//
void CAN_Transmit(uint8_t *data, uint8_t length);
void Sensor_Init();
uint32_t Sensor_Read();
uint32_t Calculate_Data(uint32_t data);

void main(){
	while(1){
		//do something
	}
}
```
Code như trên không phù hợp vì nó rất dài, rất khó để chỉnh sửa hoặc mở rộng các tính năng vậy nên nó không phù hợp để tạo ra 1 ứng dụng nhất là đối với trong lập trình automotive, các hệ thống trong xe hơi.

ECU là đơn vị phần cứng



</details>






