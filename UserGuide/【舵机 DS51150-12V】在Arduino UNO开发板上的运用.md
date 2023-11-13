# 【舵机 DS51150-12V】在Arduino UNO开发板上的运用
本教程目的是指导如何通过Arduino UNO开发板对舵机 DS51150-12V进行控制。

Arduino IDE本身自带有**Servo**库，无需下载就可以直接使用。

本教程主要对DS51150-12V 舵机的两款180°及270°的使用指导

# 1. 硬件需求

>* 舵机：DS51150-12V 270°及 DS51150-12V 180° 各一台
>   ![](../tree/main/vx_images/280082823237249.png)
 
>* Arduino开发板：Arduino UNO Rev3 开发板一块及对应的USB数据线一条
> ![](../tree/main/vx_images//232963823250084.png)

>* 杜邦线：两头都是公头的2.54mm杜邦线一排
> ![](../tree/main/vx_images//566754123246639.png)


>* 电脑：Windows/Mac 电脑一台（本教程使用Windows 11 64位系统）
> ![](../tree/main/vx_images/6434523242393.png)

>*  电源：12V直流电源，可以使用适配器或者稳压电源（本教程使用稳压电源MS-305DS测试）
> ![](../tree/main/vx_images/52904923257877.png)

# 2. 软件需求
>* 编程软件：Arduino IDE 1.8.19 （仅代表本教程测试版本，可以使用其他版本）
如果还未安装，请在Arduino官网链接进行Arduino IDE下载安装：[Arduino software](https://www.arduino.cc/en/software)
>* Arduino库：Servo 1.1.8（仅代表本教程测试版本，可以使用其他版本）
注：不同舵机驱动的脉宽范围会有所区别，需要根据舵机DS51150-12V的范围对Servo库进行修改。修改步骤如下：
>1. 打开DS51150-12V的规格书，进行查看
> ![](../tree/main/vx_images/15814023231064.png)
>2. 打开库文件，库文件位置在Arduino安装位置：\Arduino\libraries\Servo\src  的Servo.h文件。
>3. 对Servo.h库文件进行如下修改
![](../tree/main/vx_images/172790200237358.png)
```c
//#define MIN_PULSE_WIDTH       544     // the shortest pulse sent to a servo  
//#define MAX_PULSE_WIDTH      2400     // the longest pulse sent to a servo
#define MIN_PULSE_WIDTH       500     // the shortest pulse sent to a servo(DS51150-12V)  
#define MAX_PULSE_WIDTH      2500     // the longest pulse sent to a servo (DS51150-12V)  
```

# 3. 硬件接线说明
## 3.1 DS51150-12V 180° 同Arduino接线说明
![](../tree/main/vx_images/254111500260283.png)

## 3.2 DS51150-12V 270° 同Arduino接线说明

![](../tree/main/vx_images/583221600257887.png)

# 4. 例程测试

想要驱动 DS51150-12V，需要通过带有PWM功能的接口。
Arduino UNO PWM接口：3，5，6，9，10和11，本次例程使用了PIN 9;

1. 打开Arduino IDE，复制下方对应代码
* DS51150-12V 180°源码

```c
#include <Servo.h>

Servo myservo;  // create servo object to control a servo
// twelve servo objects can be created on most boards

int pos = 0;    // variable to store the servo position

void setup() {
  myservo.attach(9);  // attaches the servo on pin 9 to the servo object
}

void loop() {
  for (pos = 0; pos <= 180; pos += 1) { // goes from 0 degrees to 180 degrees
    // in steps of 1 degree
    myservo.write(pos);              // tell servo to go to position in variable 'pos'
    delay(15);                       // waits 15ms for the servo to reach the position
  }
  for (pos = 180; pos >= 0; pos -= 1) { // goes from 180 degrees to 0 degrees
    myservo.write(pos);              // tell servo to go to position in variable 'pos'
    delay(15);                       // waits 15ms for the servo to reach the position
  }
}
```

* DS51150-12V 270°源码

```c
#include <Servo.h>

Servo myservo;  // create servo object to control a servo
// twelve servo objects can be created on most boards

int pos = 0;    // variable to store the servo position

void setup() {
  myservo.attach(9);  // attaches the servo on pin 9 to the servo object
}

void loop() {
  for (pos = 0; pos <= 270; pos += 1) { // goes from 0 degrees to 270 degrees
    // in steps of 1 degree
    myservo.write(pos);              // tell servo to go to position in variable 'pos'
    delay(15);                       // waits 15ms for the servo to reach the position
  }
  for (pos = 270; pos >= 0; pos -= 1) { // goes from 270 degrees to 0 degrees
    myservo.write(pos);              // tell servo to go to position in variable 'pos'
    delay(15);                       // waits 15ms for the servo to reach the position
  }
}
```

2. 进行编译下载
* 点击Tools -> 选择对应开发板Arduino Uno以及对应COM口，点击下图红色箭头标注的编译并下载，等Done uploading代表上传成功
![](../tree/main/vx_images/120364400255389.png)

3. 进行验证

![123](../tree/main/vx_images/268130301259070.gif)