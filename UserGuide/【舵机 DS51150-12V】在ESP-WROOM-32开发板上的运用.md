# 【舵机 DS51150-12V】在ESP-WROOM-32开发板上的运用
本教程目的是指导如何通过ESP-WROOM-32开发板对舵机 DS51150-12V进行控制。

本教程主要对DS51150-12V 舵机的两款180°及270°的使用指导

# 1. 硬件需求

>* 舵机：DS51150-12V 270°及 DS51150-12V 180° 各一台
>   ![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/280082823237249.png)
 
>* ESP-WROOM-32开发板：ESP-WROOM-32 开发板一块及对应的USB数据线一条
> ![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/171654822230967.png)

>* 杜邦线：两头都是公头以及一公一母的2.54mm杜邦线各一排
> ![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/566754123246639.png)


>* 电脑：Windows/Mac 电脑一台（本教程使用Windows 11 64位系统）
> ![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/6434523242393.png)

>*  电源：12V直流电源，可以使用适配器或者稳压电源（本教程使用稳压电源MS-305DS测试）
> ![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/52904923257877.png)

# 2. 软件需求
>* 编程软件：Arduino IDE 1.8.19 （仅代表本教程测试版本，可以使用其他版本）
如果还未安装，请在Arduino官网链接进行Arduino IDE下载安装：[Arduino software](https://www.arduino.cc/en/software)
>* Arduino库：ESP32Servo 0.13.0（非Arduino官方库，需要单独下载，详细见本教程第3.2部分）

# 3. 开发板环境及教程需求库安装
## 3.1 ESP-WROOM-32 开发板环境安装
此部分安装也可参考ESPRESSIF教程：[installing-using-arduino-ide](https://docs.espressif.com/projects/arduino-esp32/en/latest/installing.html#installing-using-arduino-ide)
或者直接参考如下教程
1. 在Arduino IDE中，转到 **File** >  **Preferences**
![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/243090023249393.jpg)

2. 在“Additional Board Manager URL”字段中输入以下内容，如下图，然后点击OK
> https://espressif.github.io/arduino-esp32/package_esp32_index.json    
![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/144330123237260.jpg)

注意：如果您已经有其他的开发板的URL，您可以用逗号分隔URL，如下所示：
>  https://XXX.json,
>  https://espressif.github.io/arduino-esp32/package_esp32_index.json

3. 打开**Board Manager**。转到 **Tools** >  **Board** > **Boards Manager**
![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/312140723250095.png)
4. 搜索 **ESP32** 并按 **ESP32 by Espressif Systems** 的 **Install** 按钮，等待安装完成
![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/480480723246650.png )
注意：安装大概需要几分钟时间，请耐心等待一会儿，如果安装失败可以多尝试几次
![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/99250823242404.png)
![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/34710923260284.png)
安装成功
![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/190750923257888.png)

## 3.2 ESP32Servo 0.13.0 库安装
1. 转到 **Sketch** >  **Include Library** > **Manage Libraries**
![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/102131223255390.png)
2. 搜索 **ESP32Servo** 并安装，等待安装完成
![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/260261623236631.jpg)

# 3. 硬件接线说明
## 3.1 DS51150-12V 180° 同ESP-WROOM-32接线说明
![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/386235823236362.png)

## 3.2 DS51150-12V 270° 同ESP-WROOM-32接线说明

![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/91775923263317.png)

# 4. 例程测试

想要驱动 DS51150-12V，需要通过带有PWM功能的接口。
ESP-WROOM-32 PWM接口如下图所示，本次使用开发板子上的D18；
![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/213373123247753.png)

1. 打开Arduino IDE，转到 **File** >  **Examples** > **ESP32Servo** > **Sweep**
![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/253423323240887.png)
2. 对例程进行修改
注：不同舵机驱动的脉宽范围会有所区别，需要根据舵机DS51150-12V的范围对Sweep例程进行修改。修改步骤如下：
>* 打开DS51150-12V的规格书，进行查看
> ![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/15814023231064.png)
>* 打开Sweep例程，并对例程按照如下修改
![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/415430100249491.png)
```c
//	myservo.attach(servoPin, 1000, 2000); // attaches the servo on pin 18 to the servo object
  myservo.attach(servoPin, 500, 2500); // attaches the servo on pin 18 to the servo object(DS51150-12V) 
```
3. 进行编译下载
* 点击Tools -> 选择对应开发板DOIT ESP32 DEVKIT V1以及对应COM口，点击下图红色箭头标注的编译并下载（需要在烧录模式下烧录，参考下方说明）


![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/496244023231417.png)

注：下载前ESP-WROOM-32需要进入烧录模式
编译后出现连接时
![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/10554823242868.png)
同时按住ESP-WROOM-32的“EN”和"BOOT"按键，然后先放开“EN”键，再放开“BOOT”键。
![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/132555023235753.png)
烧录成功
![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/129334723233921.png)

3. 进行验证

![](https://raw.githubusercontent.com/Jane-DIYmall/DS51150-12V/main/vx_images/268130301259070.gif)