# 【舵机 DS51150-12V】在ESP-WROOM-32开发板上的运用
本教程目的是指导如何通过ESP-WROOM-32开发板对舵机 DS51150-12V进行控制。

本教程主要对DS51150-12V 舵机的两款180°及270°的使用指导

# 1. 硬件需求

>* 舵机：DS51150-12V 270°及 DS51150-12V 180° 各一台
>   ![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/280082823237249_1.png =300x)
 
>* ESP-WROOM-32开发板：ESP-WROOM-32 开发板一块及对应的USB数据线一条
> ![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/171654822230967.png  =300x)

>* 杜邦线：两头都是公头以及一公一母的2.54mm杜邦线各一排
> ![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/566754123246639_1.png =300x)


>* 电脑：Windows/Mac 电脑一台（本教程使用Windows 11 64位系统）
> ![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/6434523242393_1.png =300x)

>*  电源：12V直流电源，可以使用适配器或者稳压电源（本教程使用稳压电源MS-305DS测试）
> ![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/52904923257877_1.png =300x)

# 2. 软件需求
>* 编程软件：Arduino IDE 1.8.19 （仅代表本教程测试版本，可以使用其他版本）
如果还未安装，请在Arduino官网链接进行Arduino IDE下载安装：[Arduino software](https://www.arduino.cc/en/software)
>* Arduino库：ESP32Servo 0.13.0（非Arduino官方库，需要单独下载，详细见本教程第3.2部分）

# 3. 开发板环境及教程需求库安装
## 3.1 ESP-WROOM-32 开发板环境安装
此部分安装也可参考ESPRESSIF教程：[installing-using-arduino-ide](https://docs.espressif.com/projects/arduino-esp32/en/latest/installing.html#installing-using-arduino-ide)
或者直接参考如下教程
1. 在Arduino IDE中，转到 **File** >  **Preferences**
![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/243090023249393.jpg =800x)

2. 在“Additional Board Manager URL”字段中输入以下内容，如下图，然后点击OK
> https://espressif.github.io/arduino-esp32/package_esp32_index.json    
![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/144330123237260.jpg =800x)

注意：如果您已经有其他的开发板的URL，您可以用逗号分隔URL，如下所示：
>  https://XXX.json,
>  https://espressif.github.io/arduino-esp32/package_esp32_index.json

3. 打开**Board Manager**。转到 **Tools** >  **Board** > **Boards Manager**
![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/312140723250095.png =800x)
4. 搜索 **ESP32** 并按 **ESP32 by Espressif Systems** 的 **Install** 按钮，等待安装完成
![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/480480723246650.png =800x)
注意：安装大概需要几分钟时间，请耐心等待一会儿，如果安装失败可以多尝试几次
![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/99250823242404.png =800x)
![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/34710923260284.png =800x)
安装成功
![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/190750923257888.png =800x)

## 3.2 ESP32Servo 0.13.0 库安装
1. 转到 **Sketch** >  **Include Library** > **Manage Libraries**
![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/102131223255390.png =800x)
2. 搜索 **ESP32Servo** 并安装，等待安装完成
![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/260261623236631.jpg =800x)

# 3. 硬件接线说明
## 3.1 DS51150-12V 180° 同ESP-WROOM-32接线说明
![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/386235823236362.png =800x)

## 3.2 DS51150-12V 270° 同ESP-WROOM-32接线说明

![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/91775923263317.png =800x)

# 4. 例程测试

想要驱动 DS51150-12V，需要通过带有PWM功能的接口。
ESP-WROOM-32 PWM接口如下图所示，本次使用开发板子上的D18；
![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/213373123247753.png =800x)

1. 打开Arduino IDE，转到 **File** >  **Examples** > **ESP32Servo** > **Sweep**
![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/253423323240887.png =800x)
2. 对例程进行修改
注：不同舵机驱动的脉宽范围会有所区别，需要根据舵机DS51150-12V的范围对Sweep例程进行修改。修改步骤如下：
>* 打开DS51150-12V的规格书，进行查看
> ![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/15814023231064.png =800x)
>* 打开Sweep例程，并对例程按照如下修改
![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/415430100249491.png =800x)
```c
//	myservo.attach(servoPin, 1000, 2000); // attaches the servo on pin 18 to the servo object
  myservo.attach(servoPin, 500, 2500); // attaches the servo on pin 18 to the servo object(DS51150-12V) 
```
3. 进行编译下载
* 点击Tools -> 选择对应开发板DOIT ESP32 DEVKIT V1以及对应COM口，点击下图红色箭头标注的编译并下载（需要在烧录模式下烧录，参考下方说明）


![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/496244023231417.png =800x)

注：下载前ESP-WROOM-32需要进入烧录模式
编译后出现连接时
![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/10554823242868.png =800x)
同时按住ESP-WROOM-32的“EN”和"BOOT"按键，然后先放开“EN”键，再放开“BOOT”键。
![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/132555023235753.png =500x)
烧录成功
![](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/129334723233921.png =800x)

3. 进行验证

![123](https://raw.githubusercontent.com/Jane-DIYmall/VNote-Image/main/%E9%A3%9E%E5%87%A1%E6%95%99%E7%A8%8B%E5%90%88%E9%9B%86/ds51150-12v%20%E6%95%B0%E5%AD%97%E8%88%B5%E6%9C%BA/%E3%80%90%E8%88%B5%E6%9C%BA%20ds51150-12v%E3%80%91%E5%9C%A8esp-wroom-32%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E7%9A%84%E8%BF%90%E7%94%A8.md/268130301259070_1.gif)