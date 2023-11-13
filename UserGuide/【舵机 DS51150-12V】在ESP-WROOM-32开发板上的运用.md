# 【舵机 DS51150-12V】在ESP-WROOM-32开发板上的运用
本教程目的是指导如何通过ESP-WROOM-32开发板对舵机 DS51150-12V进行控制。

本教程主要对DS51150-12V 舵机的两款180°及270°的使用指导

# 1. 硬件需求

>* 舵机：DS51150-12V 270°及 DS51150-12V 180° 各一台
>   ![](../main/vx_images280082823237249.png)
 
>* ESP-WROOM-32开发板：ESP-WROOM-32 开发板一块及对应的USB数据线一条
> ![](../main/vx_images171654822230967.png)

>* 杜邦线：两头都是公头以及一公一母的2.54mm杜邦线各一排
> ![](../main/vx_images566754123246639.png)


>* 电脑：Windows/Mac 电脑一台（本教程使用Windows 11 64位系统）
> ![](../main/vx_images6434523242393.png)

>*  电源：12V直流电源，可以使用适配器或者稳压电源（本教程使用稳压电源MS-305DS测试）
> ![](../main/vx_images52904923257877.png)

# 2. 软件需求
>* 编程软件：Arduino IDE 1.8.19 （仅代表本教程测试版本，可以使用其他版本）
如果还未安装，请在Arduino官网链接进行Arduino IDE下载安装：[Arduino software](https://www.arduino.cc/en/software)
>* Arduino库：ESP32Servo 0.13.0（非Arduino官方库，需要单独下载，详细见本教程第3.2部分）

# 3. 开发板环境及教程需求库安装
## 3.1 ESP-WROOM-32 开发板环境安装
此部分安装也可参考ESPRESSIF教程：[installing-using-arduino-ide](https://docs.espressif.com/projects/arduino-esp32/en/latest/installing.html#installing-using-arduino-ide)
或者直接参考如下教程
1. 在Arduino IDE中，转到 **File** >  **Preferences**
![](../main/vx_images243090023249393.jpg)

2. 在“Additional Board Manager URL”字段中输入以下内容，如下图，然后点击OK
> https://espressif.github.io/arduino-esp32/package_esp32_index.json    
![](../main/vx_images144330123237260.jpg)

注意：如果您已经有其他的开发板的URL，您可以用逗号分隔URL，如下所示：
>  https://XXX.json,
>  https://espressif.github.io/arduino-esp32/package_esp32_index.json

3. 打开**Board Manager**。转到 **Tools** >  **Board** > **Boards Manager**
![](../main/vx_images312140723250095.png)
4. 搜索 **ESP32** 并按 **ESP32 by Espressif Systems** 的 **Install** 按钮，等待安装完成
![](../main/vx_images480480723246650.png )
注意：安装大概需要几分钟时间，请耐心等待一会儿，如果安装失败可以多尝试几次
![](../main/vx_images99250823242404.png)
![](../main/vx_images34710923260284.png)
安装成功
![](../main/vx_images190750923257888.png)

## 3.2 ESP32Servo 0.13.0 库安装
1. 转到 **Sketch** >  **Include Library** > **Manage Libraries**
![](../main/vx_images102131223255390.png)
2. 搜索 **ESP32Servo** 并安装，等待安装完成
![](../main/vx_images260261623236631.jpg)

# 3. 硬件接线说明
## 3.1 DS51150-12V 180° 同ESP-WROOM-32接线说明
![](../main/vx_images386235823236362.png)

## 3.2 DS51150-12V 270° 同ESP-WROOM-32接线说明

![](../main/vx_images91775923263317.png)

# 4. 例程测试

想要驱动 DS51150-12V，需要通过带有PWM功能的接口。
ESP-WROOM-32 PWM接口如下图所示，本次使用开发板子上的D18；
![](../main/vx_images213373123247753.png)

1. 打开Arduino IDE，转到 **File** >  **Examples** > **ESP32Servo** > **Sweep**
![](../main/vx_images253423323240887.png)
2. 对例程进行修改
注：不同舵机驱动的脉宽范围会有所区别，需要根据舵机DS51150-12V的范围对Sweep例程进行修改。修改步骤如下：
>* 打开DS51150-12V的规格书，进行查看
> ![](../main/vx_images15814023231064.png)
>* 打开Sweep例程，并对例程按照如下修改
![](../main/vx_images415430100249491.png)
```c
//	myservo.attach(servoPin, 1000, 2000); // attaches the servo on pin 18 to the servo object
  myservo.attach(servoPin, 500, 2500); // attaches the servo on pin 18 to the servo object(DS51150-12V) 
```
3. 进行编译下载
* 点击Tools -> 选择对应开发板DOIT ESP32 DEVKIT V1以及对应COM口，点击下图红色箭头标注的编译并下载（需要在烧录模式下烧录，参考下方说明）


![](../main/vx_images496244023231417.png)

注：下载前ESP-WROOM-32需要进入烧录模式
编译后出现连接时
![](../main/vx_images10554823242868.png)
同时按住ESP-WROOM-32的“EN”和"BOOT"按键，然后先放开“EN”键，再放开“BOOT”键。
![](../main/vx_images132555023235753.png)
烧录成功
![](../main/vx_images129334723233921.png)

3. 进行验证

![](../main/vx_images268130301259070.gif)