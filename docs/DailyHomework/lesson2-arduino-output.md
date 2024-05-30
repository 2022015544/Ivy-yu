## <font size="5"><h2 style="color: #e19cab;">2.Arduino IDE</h2></font>

### <h3 style="color: #e19cab;"> (1) Introduction</h3>

  **To download the Arduino IDE:**  
  The Arduino Integrated Development Environment (IDE) is the place to write, compile, and upload code to Arduino boards.It can be downloaded for free from the [Arduino website](https://www.arduino.cc/en/Main/Software)where you can choose the version you want and install it on your computer.
  
  **Connecting to the computer:**  
  Connect the Arduino board to the computer using a USB cable, and the computer will automatically detect the board.  
  In the Arduino IDE, open a new sketch by selecting`File` > `New`, which opens a new window for writing code. A basic Arduino sketch consists of two main functions: `setup()`和`loop()`。The `setup()` function is called once when the board starts, and the `loop()`unction is called repeatedly as long as the board is powered on.
  
  **Uploading the sketch:**  
  After writing the code, click the upload button (right arrow icon) in the Arduino IDE to upload it to the Arduino board. The IDE compiles the written code and sends it to the Arduino board.
  
  **Connecting components:**  
 Once the Arduino board is set up and the code is uploaded, we can begin to connect components such as LEDs, sensors, motors, etc., to the Arduino board, using Dupont wires to make connections between the components and the pins on the board.
  
  **Testing the project:**  
  After everything is connected, power on the Arduino board and observe the actual operation of the project. If something isn't working as expected, you can return to the code, make changes, and then re-upload it.

![Arduino-IDE](https://github.com/NexMaker-Fab/2024ZWU-IS-8-BUNBUN/raw/cfe7ae2c17bd472adca8561bedfd0ecc1638589b/images/Arduino/ArduinoIDE.png)

### <h3 style="color: #e19cab;">(2)Coding method</h3>
**Function Structure:**
  In Arduino, the `setup()`and`loop()`functions are the two basic functions when writing any Arduino program, and they have the following characteristics:

**1.setup()function:**
- The`setup()` function is executed only once when the Arduino program starts running, and is used for initial setup.
- With the `setup()` function, you can set pin modes (input or output), initialize variables, start serial communication, etc.
- Typically, the`setup()`function is used to configure hardware, such as initializing pins or starting external devices.
**2.loop()function:**
- The`loop()`function is the main body of the Arduino program and constantly loops until the Arduino board is powered off or reset.
- In the `loop()` function, you can write code to handle inputs, execute logic, control outputs, and more.
- By using loops and conditional statements in the`loop()`function, you can implement a variety of different functionalities, such as sensor monitoring, controlling actuators, communication, etc.
- Since the `loop()`function continuously executes, it is advisable to avoid lengthy blocking operations (such as the`delay()`函数function) to ensure that the Arduino can respond timely to external events.

In summary, the`setup()`function is for initial setup and is executed only once, whereas the`loop()`function is the core of the Arduino program, handling iterative tasks and continuously looping. These two functions together form the fundamental structure of any Arduino program.

---

In the Arduino IDE, the term "method" typically refers to a member function of a class in object-oriented programming (OOP). In traditional programming contexts, both functions and methods are considered to be blocks of code that perform specific tasks. In Arduino and its use of the C++ language, there is a subtle difference between the two terms:

- **Function:** Refers to an independent block of code that can perform a specific task. This block of code can accept some inputs (parameters), and it might return a result. Functions can exist independently of a class.
- **Method：**Specifically refers to functions that belong to a class or an object. Methods can access and modify the data of their parent class or object (i.e., member variables).

A key concept in object-oriented programming is encapsulating data (variables) and the code that operates on that data (methods) within classes. In the Arduino programming environment, using classes and objects can help users organize complex code more effectively, making it easier to understand and maintain.

**Example：**
Below is an example of a class related to an LED, which has two methods: `turnOn` and `turnOff`, used to control the LED's on and off state.

```C
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

In this example, the `turnOn` and `turnOff` functions are methods of the LED class, because they are defined within the class and operate on the instance variables of the class.


### <h3 style="color: #e19cab;">Hardware connect</h3>
- Prepare the necessary hardware components, such as sensors, LED lights, motors, and connecting wires.
- Identify the pins: Check the pin diagram on the Arduino board to understand the function and numbering of each pin. Usually, there are two types: Digital Pins and Analog Pins.
- Connect the power supply: This can be done through the power pins on the Arduino board or an external power adapter.
- Connect the ground wire: Connect the ground wire of the external device to the ground pin (GND) on the Arduino board.
- Connect the data wires: Depending on the communication method between the external device and the Arduino board, connect the data wires to the corresponding digital or analog pins.

><strong>Programming:</strong></font>
><strong>Use the Arduino IDE or another programming environment to write the program code to control and read the connected hardware devices.

><strong>Testing:</strong></font>
><strong>Upload the program to the Arduino board and test to ensure that the hardware connections and code work correctly.

><strong>Debugging:</strong></font>
><strong>If problems occur, you can systematically check the hardware connections, the power supply, and the program code to find and solve the issues.

### <font size="5"><h2 style="color: #e19cab;"> 3.Run water light program</h2></font>
Use five Leds to make a water light project.

**Required hardware:**
1. Arduino development board(We use Arduino Nano)
2. 5 leds, 10 Dupont wires

**Wiring steps:**
1.Connect the longer end of each LED bulb to Arduino pins 2, 3, 4, 5, and 6 respectivel
2.Connect the shorter end of each LED bulb to the GND pin on the Arduino

Arduino IDE code example (5 LEDs):
```C
/**
*Do one demo in arduino of the run water light program
*2024/5/30
*By BUNBUN Team
**/
//C++ code

// 定义LED引脚数量和引脚号数组
const int numOfLeds = 5; //定义一个常量numOfLeds，表示LED灯的数量是5
int ledPins[numOfLeds] = {2, 3, 4, 5, 6}; //定义一个整数数组ledPins，存储5个LED的引脚号，分别是2、3、4、5、6

void setup() {
  // 设置每个引脚为输出
  //使用for函数进行循环，依次设置led引脚
  for (int i = 0; i < numOfLeds; i++) {
    pinMode(ledPins[i], OUTPUT);
  }
}

void loop() {
  // 从左到右依次点亮LED
  for (int i = 0; i < numOfLeds; i++) {
    digitalWrite(ledPins[i], HIGH); // 点亮LED
    delay(200);                     // 等待200毫秒
    digitalWrite(ledPins[i], LOW);  // 关闭LED
  }

  // 从右到左依次点亮LED
  for (int i = numOfLeds - 1; i >= 0; i--) {
    digitalWrite(ledPins[i], HIGH); // 点亮LED
    delay(200);                     // 等待200毫秒
    digitalWrite(ledPins[i], LOW);  // 关闭LED
  }

  //blink
  // 同时点亮所有LED
  for (int i = 0; i < numOfLeds; i++) {
    digitalWrite(ledPins[i], HIGH); //点亮LED
  }
  delay(1000); // 等待1秒

  // 同时关闭所有LED
  for (int i = 0; i < numOfLeds; i++) {
    digitalWrite(ledPins[i], LOW); //熄灭LED
  }
  delay(1000); // 等待1秒
}
```

Computer Wiring Diagram
![Arduino-IDE](https://github.com/NexMaker-Fab/2024ZWU-IS-8-BUNBUN/raw/e416415e12d82490134402c0ea5d309b45bd9395/images/Arduino/Arduino%20%E6%B5%81%E6%B0%B4%E7%81%AF%E7%94%B5%E8%84%91%E7%AB%AF%E6%8E%A5%E7%BA%BF%E5%9B%BE.png)

Simulation Effect Diagram
<img src="https://github.com/NexMaker-Fab/2024ZWU-IS-8-BUNBUN/raw/e416415e12d82490134402c0ea5d309b45bd9395/images/Arduino/Arduino%E7%94%B5%E8%84%91%E7%AB%AF%E6%95%88%E6%9E%9C%E5%9B%BE.gif" alt="Arduino-IDE" width="1200">


Physical Wiring Diagram
![Arduino-IDE](https://github.com/NexMaker-Fab/2024ZWU-IS-8-BUNBUN/raw/dcf4c007f332feab0bc9f5330ccfee5ddf370db3/images/Arduino/arduino%20%E6%B5%81%E6%B0%B4%E7%81%AF%20%E6%8E%A5%E7%BA%BF%E5%9B%BE.jpg)

Physical Effect Diagram
<img src="https://github.com/NexMaker-Fab/2024ZWU-IS-8-BUNBUN/raw/dcf4c007f332feab0bc9f5330ccfee5ddf370db3/images/Arduino/Arduino%20basic%20%E6%B5%81%E6%B0%B4%E7%81%AF.gif" alt="Arduino-IDE" width="1200">
