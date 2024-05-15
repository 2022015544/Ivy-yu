## 2.Arduino IDE

### (1)Introduction

  **下载Arduino IDE：**  
  Arduino集成开发环境（IDE）是编写、编译和上传代码到Arduino板的地方。我们可以从[Arduino网站](https://www.arduino.cc/en/Main/Software)免费下载，自行选取想要版本并将其安装在计算机上。
  
  **连接到计算机：**  
  使用USB电缆将Arduino板连接到计算机，计算机自动检测到电路板。  
  在Arduino IDE中，通过选择`File` > `New`打开一个新的草图，打开新窗口就可以在其中编写代码。基本的Arduino草图由两个主要功能组成：`setup()`和`loop()`。当主板启动时，`setup()`函数被调用一次，只要主板开机，就会重复调用`loop()`函数。
  
  **上传草图：**  
  编写完代码后，单击Arduino IDE中的上传按钮（右箭头图标）将其上传到Arduino板上。IDE将编译所写代码并将其发送到Arduino板。
  
  **连接组件：**  
  当设置好Arduino板并完成代码上传后，我们可以开始将例如：LED、传感器、电机等组件连接到Arduino板，使用杜邦线在组件和Arduino板上的引脚之间进行连接。
  
  **测试项目：**  
  连接好一切后，打开Arduino板，并查看项目的实际操作。如果某些东西没有按预期工作，可以返回代码进行更改，然后将其重新上传。

![Arduino-IDE](https://github.com/NexMaker-Fab/2024ZWU-IS-BUNBUN/raw/d79616a100a0a6490d09397666beb436f12ff9dc/images/ArduinoIDE.png)

### (2)Coding method
  **函数结构：**
  Arduino中的`setup()`和`loop()`函数是编写任何Arduino程序时的两个基本函数，它们有以下特点：

**1.setup()函数：**
- `setup()`函数在Arduino程序开始执行时仅执行一次，用于初始化设置。
- 在`setup()`函数中，你可以设置引脚模式（输入或输出）、初始化变量、启动串口通信等。
- 通常，`setup()`函数用于配置硬件，例如初始化引脚或启动外部设备。
**2.loop()函数：**
- `loop()`函数是Arduino程序的主体，会一直循环执行，直到Arduino板断电或重置。
- 在`loop()`函数中，你可以编写处理输入、执行逻辑、控制输出等代码。
- 通过在`loop()`函数中使用循环和条件语句，你可以实现各种不同的功能，例如传感器监测、控制执行器、通信等。
- 由于`loop()`函数会一直循环执行，因此在其中应该避免使用长时间的阻塞操作（例如`delay()`函数），以确保Arduino能够及时响应外部事件。

总的来说，`setup()`函数用于初始化设置，只执行一次；而`loop()`函数是Arduino程序的主体，用于处理循环任务，会一直循环执行。这两个函数共同构成了Arduino程序的基本结构。

---

在Arduino IDE中，术语 "method" 通常指的是面向对象编程（OOP）中类的成员函数。在传统编程语境中，函数和方法被认为是执行特定任务的代码块。在Arduino及其使用的C++语言中，这两个术语有细微的区别：

- **函数（Function）：**指的是一个独立的代码块，可以执行某个特定的任务。这个代码块可以接受一些输入（参数），并且可能返回一个结果。函数不需要依附于类即可存在。
- **方法（Method）：**特指那些归属于类或对象的函数。方法可以访问和修改其父类或对象的数据（即成员变量）。

面向对象编程的一个关键概念是将数据（变量）和操作这些数据的代码（方法）封装到类中。在Arduino编程环境中，使用类和对象可以帮助用户更有效地组织复杂的代码，使之更加易于理解和维护。

**Example：**
以下是假设有关于LED的一个类，该类有两个方法：`turnOn`和`turnOff`，用于控制LED的开和关状态。

```C++
class LED {
  private:
    int pin; // LED连接的引脚
  public:
    // 构造函数，用于初始化LED对象
    LED(int pinNumber) {
      pin = pinNumber;
      pinMode(pin, OUTPUT); // 设置引脚为输出模式
    }
    
    // 方法：打开LED
    void turnOn() {
      digitalWrite(pin, HIGH); // 设置引脚为高电平，点亮LED
    }
    
    // 方法：关闭LED
    void turnOff() {
      digitalWrite(pin, LOW); // 设置引脚为低电平，熄灭LED
    }
};
``` 

在此例中，turnOn和turnOff函数是LED类的方法，因为它们是定义在类的内部，并且作用于类的实例变量。


### Hardware connect
- 准备所需的硬件组件，比如传感器、LED 灯、电机等，并且准备好了连接线。
- 识别引脚：查看 Arduino 板上的引脚图，了解每个引脚的功能和编号。通常有数字引脚（Digital Pins）和模拟引脚（Analog Pins）两种类型。
- 连接电源：这可以是通过 Arduino 板上的电源引脚，也可以是外部电源适配器。
- 连接地线：将外部设备的地线连接到 Arduino 板上的地线引脚（GND）。
- 连接数据线：根据外部设备和 Arduino 板的通信方式，将数据线连接到相应的数字或模拟引脚上。

><strong>编程：</strong></font>
><strong>使用 Arduino IDE 或其他编程环境编写程序代码，以控制和读取连接的硬件设备。

><strong>测试：</strong></font>
><strong>上传程序到 Arduino 板上，进行测试以确保硬件连接和代码都正常工作。

><strong>调试：</strong></font>
><strong>如果出现问题，可以逐步检查硬件连接、电源供应以及程序代码，以找到并解决问题。

### 3.Run water light program
由于缺少各色的LED小灯泡，因而，决定用ws2812来做流水灯项目。

**所需硬件：**
1. Arduino开发板
2. 一个2812灯环，包含8个LED灯和3根连接线（电脑端为NeoPixel Ring 12，包含12个LED灯）

**接线步骤：**
将2812灯环连接到Arduino的数字引脚上
1. 将2812灯坏的正极连接到Arduino的5V引脚
2. 将2812灯环的GND连接到Arduino的GND引脚
3. 将2812灯环的input引脚连接到Arduino的一个数字引脚6

Arduino IDE代码示例(12个LED灯)
```C++
//C++ code
//定义LED灯在R,G,B三个通道上的数值
int R[]={255,255,255,99,41,41,197,239,0,125,255,0};
int G[]={41,143,249,255,255,102,41,142,255,120,0,255};
int B[]={41,41,41,41,149,255,255,102,255,125,0,0};
int i=0; //初始化一个整型变量i，值为0

#include <Adafruit_NeoPixel.h> //引入Adafruit NeoPixel库
#ifdef __AVR__ //检查是否定义了宏 __AVR__ 
#include <avr/power.h> //为 16 MHz Adafruit Trinket 配置
#endif
//初始化NeoPixel对象（初始化为12颗LED，连接到数字引脚6，颜色顺序为GBR，信号频率是800KHz）
Adafruit_NeoPixel pixels(12, 6, NEO_GRB + NEO_KHZ800);

void setup() {
//if语句为条件语句，检查是否正在为AVR ATtiny85微控制器编译，以及信号频率是否为16000000Hz。如果这两个条件都成立，则将执行endif块中的代码
#if defined(__AVR_ATtiny85__) && (F_CPU == 16000000)
  clock_prescale_set(clock_div_1); //时钟除数设置为1，表示时钟频率没有改变，将以最快速度运行
#endif
  pixels.begin(); // 初始化 NeoPixel strip object (REQUIRED)
}

//使用for循环，变量i从0遍历到11，共12次循环
void loop() {
  for (int i = 0; i < 12;i++) { 
    pixels.clear(); // 每次循环开始，把所有LED设置为关闭状态
    pixels.setPixelColor(i, pixels.Color(R[i],G[i], B[i])); // 使用i索引一次从每个数组中取出相应的颜色值
    pixels.show();   // 使更新颜色的LED灯显示
    delay(500); // 在进入下次循环之前等待500毫秒
  }
}
```

电脑端接线图
![Arduino-IDE](https://raw.githubusercontent.com/NexMaker-Fab/2024ZWU-IS-BUNBUN/main/images/Arduinocom.png)

效果模拟图
![Arduino-IDE](https://github.com/NexMaker-Fab/2024ZWU-IS-BUNBUN/raw/d79616a100a0a6490d09397666beb436f12ff9dc/images/ArduinocomGIF.gif)

实体接线和效果图

<img src= https://github.com/NexMaker-Fab/2024ZWU-IS-BUNBUN/raw/2c8f82c334f2c5d53b697ef5c3bc2633b492bbd2/images/%E5%AE%9E%E4%BD%93%E6%8E%A5%E7%BA%BF%E5%9B%BE.jpg alt="Arduino IDE" width="600" />

![Arduino-IDE](https://github.com/NexMaker-Fab/2024ZWU-IS-BUNBUN/raw/2c8f82c334f2c5d53b697ef5c3bc2633b492bbd2/images/%E5%AE%9E%E4%BD%93%E6%8E%A5%E7%BA%BF%E5%9B%BEGIF.gif)