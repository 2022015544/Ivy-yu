# learn how to do a website

```markdown
<!-- _coverpage.md -->

<img src="https://raw.githubusercontent.com/2022015544/Ivy-yu/main/image/image/imagelogo-02.png" alt="LOGO" width="400" />

# <span style="color: white;">BUNBUN</span>

> <span style="color: white;">Hello! This is Ivy! Here is my personal website! Nice to meet you!</span>

- <span style="color: white;">Keep working!</span>

[Get Started](#hello)

<!-- 在Markdown文件中设置背景 -->

<!-- 设置背景颜色 -->
![color](#030e1b)
```
```markdown
<!-- 侧边栏 docs/_sidebar.md -->
- Self introduction
  - [Self-Introduction](self-introduction.md)

- Daily Homework
  - [Lesson1: Web Setup](DailyHomework/lesson1-web-site-setup.md)
  - [Lesson2: Arduino-Output](DailyHomework/lesson2-arduino-output.md)
  - [Lesson3: Arduino-Intput](DailyHomework/lesson3-arduino-intput.md)
  - [Lesson4: 3D Printer](DailyHomework/lesson4-3d-printer.md)
  ```

```C
const int soundDOPIN = 2; //声音传感器接引脚2
const int redPin = 13; //LED小灯
const int playPin = 5;
boolean LEDs = 0;
unsigned long duration;
void setup() {
  Serial.begin(9600);
  pinMode(soundDOPIN, INPUT);
  pinMode(redPin, OUTPUT);
  digitalWrite(redPin, LOW);
  pinMode(playPin, OUTPUT);
  digitalWrite(playPin, HIGH);
}
void loop() {
  do {
    duration = pulseInLong(soundDOPIN, HIGH);
    if (duration > 0 & duration < 200) LEDs = 1;
    delay(1);
  } while (LEDs==0);
  Serial.println("hand");
  digitalWrite(redPin, HIGH);
  delay(3000);
  do {
    duration = pulseInLong(soundDOPIN, HIGH);
    if (duration > 300) LEDs = 0;
    delay(1);
  } while (LEDs==1);
  Serial.println("wind");
  digitalWrite(redPin, LOW);
  digitalWrite(playPin, LOW);
  for (int i = 0; i < 42; i++) {
    Serial.println(i);
    delay(1000);
  }
  digitalWrite(playPin, HIGH);
  while (1);
}
```

按windows加alt加R键进行屏幕录制

![CAD](https://cdn.jsdelivr.net/gh/2022015544/Ivy-yu@main/C:%5CUsers%5CIvy%5CDocuments%5CGitHub%5CIvy-yu%5Cdocs%5CimageArduino%20%E6%B5%81%E6%B0%B4%E7%81%AF%E7%94%B5%E8%84%91%E7%AB%AF%E6%8E%A5%E7%BA%BF%E5%9B%BE.png)