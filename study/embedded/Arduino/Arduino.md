# Arduino：

[TOC]

## 简介：

Arduino是一款**便捷灵活、方便上手**的**开源**电子原型平台。包含**硬件和软件**（Arduino IDE）。由一个欧洲开发团队于2005年冬季开发。其成员包括 Massimo Banzi、David Cuartielles、Tom Igoe、Gianluca Martino、David Mellis 和 Nicholas Zambetti 等。

## 特点：

Arduino IDE可以在 **Windows、Mac OS、Linux** 三大主流操作系统上运行，而其他的大多数控制器只能在Windows上开发。对于初学者来说，它**极易掌控**，有**足够灵活性**，**不需要太多基础**就可以开发。我初次接触 Arduino 时，仅仅连 MCU 是什么也不知道，但还是开发出了不少东西。不够有一定基础也是**非常有必要**的，在开发复杂功能时可以少走弯路。（亲身经历）

## 主板：

目前 Arduino 的主板型号有很多，主要有：

> Arduino Uno
>
> Arduino Nano
>
> Arduino LilyPad
>
> Arduino Mega 2560
>
> Arduino Ethernet
>
> Arduino Due
>
> Arduino Leonardo
>
> ArduinoYún 

扩展版也有不少：

> Arduino GSM Shield
>
> Arduino Ethernet Shield
>
> Arduino WiFi Shield
>
> Arduino Wireless SD Shield
>
> Arduino USB Host Shield
>
> Arduino Motor Shield
>
> Arduino Wireless Proto Shield
>
> Arduino Proto Shield

------

使用资料：

[Arduino基础入门篇28—舵机控制 - 简书 (jianshu.com)](https://www.jianshu.com/p/f3fee0082519)

[Arduino基础入门篇26—步进电机 - 简书 (jianshu.com)](https://www.jianshu.com/p/877006ab4859)

------

## 实践：

刚开始时**最好先了解一下 C 语言**（其他也行），但如果0基础，需要**注意每一个语句的作用和写法**。这里只会讲解一些**核心函数**，语法不会详细讲解（如：while循环，for循环等）。

### 搭建环境：

这里使用 **Arduino IDE** 作为开发环境，**Arduino UNO** 作为开发板。

Arduino IDE 下载：[Arduino - Windows](https://www.arduino.cc/en/guide/windows)

Arduino UNO：

<img src="https://www.arduino-france.com/wp-content/uploads/2019/02/arduino-uno.jpg" style="zoom:15%;" />

软件下载完毕后，将开发板与电脑使用 **USB** 线连接，如果在**设备管理器**中未识别成功，考虑**安装驱动**，如果失败，则上网查找 **CH340** 驱动下载。

### 认识开发板：

<img src="https://www.yahboom.com/Public/ueditor/php/upload/image/20190918/1568801446487507.png" style="zoom:50%;" />

### Blink示例：

这里列举**点灯例程**（硬件世界的 Hello World）：



1.将1个**LED**灯**长引脚**（正极）连接**220Ω**电阻后连接 Arduino 板上的**数字脚0**。

2.将此LED灯**短引脚**（负极）连接 Arduino 板上的 **GND** 。

3.复制此代码，上传，观察效果。

注意" () ; , "等符号为**英文符号**。（如果硬件上不想接线，可以将代码中**0号引脚改为13号**，使用板载 LED ）

```c
void setup(){
  pinMode(0, OUTPUT); //将0号引脚设为输出。
}

void loop(){
  digitalWrite(0, HIGH); //0号引脚设为高电平。
  delay(1000); //延迟1秒。
  digitalWrite(0, LOW); //0号引脚设为低电平。
  delay(1000); //延迟1秒。
}
```

**可以看见 LED 以 1Hz 频率闪烁。**

程序解读：

其中“ void setup() ”函数在程序开始执行时**只调用一次**，使用它**初始化变量、初始化外设**等。

这里使用“ pinMode ”函数将0号引脚配置为**输出引脚**。

而“ void loop() ”函数会**不断重复执行**。

在这里，使用“ digitalWrite “函数将0号引脚设置为**高电平**（5V，HIGH），**一秒后**（delay 函数）设置为**低电平**（0V，LOW），**等待一秒后循环**。

------

### ADC、PWM示例：

##### -ADC ( <u>A</u>nalog to <u>D</u>igital <u>C</u>onverter ):

**模拟数字转换器**即 A/D 转换器，或简称 ADC ，通常是指一个将模拟信号转变为数字信号的电子元件。

##### -PWM ( <u>P</u>ulse <u>W</u>idth <u>M</u>odulation ):

**脉宽调制**是一种对**模拟信号电平进行数字编码**的方法。通过高分辨率计数器的使用，方波的**占空比**被调制用来对一个具体模拟信号的电平进行编码。PWM 信号仍然是**数字**的，因为在给定的任何时刻，满幅值的直流供电**要么完全有（ON），要么完全无（OFF）**。

<img src="http://yomaker.com/wp-content/uploads/2016/11/pwm-arduino.jpg" style="zoom:67%;" />



以下是 Arduino **读取 A3 引脚模拟信号并以 PWM 形式对 LED 调光**的例程：



1.将1个**LED**灯**长引脚**（正极）连接**220Ω**电阻后连接 Arduino 板上的引脚**9**。

2.将此LED灯**短引脚**（负极）连接 Arduino 板上的 **GND** 。

3.将一个电位器**阻值不固定的两端**分别接 **A3** 和 **GND** 。

4.复制此代码，上传，旋转电位器，观察效果。

```c
int ledPin = 9; //将LED连接至9号引脚
int AnalogPin = A3; //A3引脚作为模拟输入

int val = 0; //将读取到的模拟值赋给变量val

void setup(){
  pinMode(AnalogPin, INPUT); //将AnalogPin(A3)设置为输入引脚
  pinMode(ledPin, OUTPUT); //将ledPin(9)设置为输出引脚
}

void loop(){
  val = analogRead(AnalogPin); //读取并赋值
    
  analogWrite(ledPin, val/4); //输出PWM到LED
}//模拟值读出后是一个0-1024的值，但每字节的大小为0-255，所以这里将值除以4再输出
```

**可以看见随着电位器旋转， LED 亮度不断变化。如果有示波器，可以发现 PWM 波频率固定在 430Hz。**

程序解读：

analogRead() 和 analogWrite() 为核心函数。

------

### 串行通讯：

所有 Arduino 控制器都有至少一个串行端口（也称为**UART或者USART**）。个人电脑可以通过 USB 端口与Arduino的**引脚0(RX)和引脚1(TX)** 进行通信。你可以通过 Arduino 开发环境软件中的**串口监视器**来与 Arduino 控制器进行串口通信。

这里展示最基本示例：

```c
void setup(){
  Serial.begin(9600); //波特率为9600
}

void loop(){
  Serial.print("Hello World!");
  Serial.println("换行输出");
  Serial.println(millis()); //获取Arduino开机后运行的时间长度
  delayMicroseconds(1000000); //等待1000000微秒
}
```

**可以在串口监视器里看见打印的数据。**

程序解读：

Serial.print() , Serial.println() 用于打印数据，millis() 用于获取 Arduino 开机后运行的时间长度。

delayMicroseconds() 与 delay() 函数都可用于**暂停程序运行**。不同的是，delayMicroseconds() 的参数单位是**微秒**。

------

### 使用库：

通过**库**的使用可以**拓展 Arduino 开发板的功能**。因为有了库，我们可以**很轻松**的实现 Arduino 与外部硬件的协作或进行数据通讯。

Arduino IDE **预装有**一系列标准库文件，同时您也可以自己将**第三方库**（如：网上下载的开源库）安装导入Arduino IDE ，甚至**您自己也可以**建立库并导入 Arduino IDE 。

#### Arduino标准库有：

- EEPROM – 读写开发板内置EEPROM，“永久”保存数据。
- Servo – 控制舵机（伺服电机）
- Stepper – 控制步进电机
- SD – 读写SD卡
- Wire– 通过TWI/I2C实现多台开发板或传感器的相互通讯
- LiquidCrystal – 控制显示液晶屏(LCD)
- SPI – 用串行外设接口（SPI）进行通讯

**接下来我将依次给出教程：**

#### EEPROM：

EEPROM：**<u>E</u>lectrically <u>E</u>rasable, <u>P</u>rogrammable <u>R</u>ead-<u>O</u>nly <u>M</u>emory** 。电可擦除可编程只读存储器。

简单来说 EEPROM 就像是一个硬盘，所以即使掉电，存放在 EEPROM 中的数据也可以保存下来，方便再次上电的时候进行读取操作。

ATmega328 内部具有 **1kB** 的 EEPROM 。

注意：EEPROM的 写入/擦除 寿命为**100000**次左右。

示例：



1.硬件上无需连线。

2.上传代码。

```c
//写入：
#include <EEPROM.h> //导入库

int addr = 0; // 从地址0开始写

void setup(){

}

void loop(){
  int val = analogRead(0) / 4;
  EEPROM.write(addr, val); //在地址0写入值
  delay(1000);
}

//读取：
#include <EEPROM.h>

int address = 0;
byte value;

void setup() {
  Serial.begin(9600);
}

void loop(){
  value = EEPROM.read(address); //读取地址0的值

  Serial.print(value, DEC); //串口打印
  Serial.println();
  delay(1000);
}
```



### Servo：

舵机是一种位置（角度）伺服的驱动器，适用于那些需要**角度不断变化并可以保持的控制系统**。在高档遥控玩具，如飞机、潜艇模型，遥控机器人中已经得到了普遍应用。

舵机安装了一个**电位器（或其它角度传感器）**检测输出轴转动角度，控制板根据电位器的信息能比较精确的控制和保持输出轴的角度。

舵机转动的角度是通过调节 PWM 信号的**占空比**来实现的。标准的PWM信号的周期固定为**20ms**，理论上脉宽分布应该在**1ms到2ms**之间，实际上可由**0.5ms到2.5ms**之间，脉宽与转角**0°—180°**相对应。

舵机一般都外接**三根线**，分别用**棕、红、橙**三种颜色进行区分，由于品牌不同，颜色也会有所差异，**棕色为接地线，红色为电源正极线，橙色为信号线**。

<img src="https://cbu01.alicdn.com/img/ibank/2019/011/770/11152077110_114226360.jpg" style="zoom:10%;" />

示例：



1.控制线接9。剩余两根接电源。

2.上传代码。

```c
#include <Servo.h>

Servo myservo;  // 定义Servo对象来控制
int pos = 0;    // 角度存储变量

void setup() {
  myservo.attach(9);  // 控制线连接数字9
}

void loop() {
  for (pos = 0; pos <= 180; pos ++) { // 0°到180°
    myservo.write(pos); // 舵机角度写入
    delay(5); // 等待转动到指定角度
  }
  for (pos = 180; pos >= 0; pos --) { // 从180°到0°
    myservo.write(pos); // 舵机角度写入
    delay(5); // 等待转动到指定角度
  }
}
```

**舵机在0°和180°间不断转动。**



### Stepper：

步进电机是一种将电脉冲转化为角位移的执行机构。

这里使用的步进电机型号为**28BYJ-48**，**1相励磁**方式驱动，通过给ABCD四相依次通电来实现转自不停转动。控制板型号为 **ULN2003** 驱动板。

<img src="https://alltopnotch.co.uk/wp-content/uploads/imported/0/New-Stepper-Motor-28BYJ-48-ULN2003-Driver-Board-Module-Arduino-Pi-Pic-AVR-ARM-231912389590-1080x844.jpg" style="zoom:20%;" />

示例：



1.ULN2003驱动板上IN1、IN2、IN3、IN4分别连接UNO开发板的数字引脚2，3，4，5；

驱动板电源输入+、-引脚分别连接UNO开发板的5V、GND。

2.上传代码。

```c
void setup() {
  // put your setup code here, to run once:
  for (int i = 2; i < 6; i++) {
    pinMode(i, OUTPUT);
  }
}

void clockwise(int num)
{
  for (int count = 0; count < num; count++)
  {
    for (int i = 2; i < 6; i++)
    {
      digitalWrite(i, HIGH);
      delay(3);
      digitalWrite(i, LOW);
    }
  }
}

void anticlockwise(int num)
{
  for (int count = 0; count < num; count++)
  {
    for (int i = 5; i > 1; i--)
    {
      digitalWrite(i, HIGH);
      delay(3);
      digitalWrite(i, LOW);
    }
  }
}

void loop() {
  // put your main code here, to run repeatedly:
  clockwise(512);
  delay(10);
  anticlockwise(512);
}
```

**可见电机180°正反转。**



### SD：

上文讲到数据可以存储在 EEPROM 中，但如果要存储**大量数据**，Arduino 1Kb 的存储空间就力不从心了，但是我们可以挂载 **SD** 卡，拓展出**大量空间**。

这是这里所用的 Micro SD Card 模块：

<img src="http://static.zhizaoyun.com/glib/4_1_334609/image530x430/1275893_20190321143723.jpg" style="zoom:33%;" />

还没写完……