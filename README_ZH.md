# 💡 基于 Arduino UNO 的多通道示波器 DIY 制作 🪛

[English](README.md) | [中文](README_ZH.md)

## 项目介绍

示波器是一种用于观察各种不同类型信号电压的设备📉。在一个图形显示器上，示波器可以将电压显示为一维的图形，其中一轴代表时间⏱️，另一轴代表电压⚡。这使得观察者可以看到信号随时间的变化，例如信号的周期性波动。示波器作为一种重要的电子测量工具🔧，广泛应用于电路设计、故障诊断、教育教学和科学研究等领域📚🔬。然而，由于其高昂的价格💰，学生可能难以承担。因此，作者希望使用 Arduino 开发板，构建一个低成本、多通道的简易示波器，以支持学生的学习和研究活动，为电子和电气工程教育提供了一个实用的工具🛠️。

Arduino Uno 开发板上有 6 个模拟输入引脚，标记为 A0 到 A5。这些引脚可以用来读取传感器的输出，或者读取其他设备的模拟信号。 这些信号的电压在 0 到 5 伏特之间。Arduino 会将这个模拟电压转换为一个介于 0 到 1023 的整数。通过使用这些模拟输入引脚，来读取四个模拟信号。然后使用 Arduino 的 analogRead() 函数来读取一个模拟引脚的电压。经过计算后，将实际值、平均值、最大值、最小值输出到 LCD1602上，并将波形图像绘制在 LCD12864 上。

为了检测示波器的效果，该项目配备一个基于 Arduino Mini 制作的简易信号发生器，可以在2-12引脚输出不同周期的方波信号。	

## 功能介绍

### 四通道模拟信号输入
示波器可以同时接收和处理四个模拟信号，这些信号可以来自各种传感器或其他电子设备。示波器每 20ms 采样一次，采样频率为 50Hz。

### 数值显示
示波器使用一个 16x2 的 LCD1602 显示屏来显示信息。屏幕上显示电压值、平均值、最小值、最大值四个参数，每两秒切换一个通道。

### 波形显示
示波器使用一个 128x64 的 LCD12864 显示屏来显示的波形。屏幕被分为左上、右上、左下、右下四个区域，分别显示从A0、A1、A2、A3模拟输入引脚输入的信号波形。每个区域的左上角有一个通道标签，用于指示该区域对应的模拟输入引脚。

![image](https://github.com/user-attachments/assets/87396110-d8ca-4106-9f47-4037a88eb5ac)

## 硬件说明

| 设备 | 数量 | 说明 |
| --- | --- | --- |
| Arduino UNO | 一块 | 主控制器，负责读取模拟信号，处理数据，并控制显示屏显示波形。 |
| Arduino Mini | 一块 | 作为信号发生器，可以在2-12引脚输出不同周期的方波信号。 |
| MB-102 电源模块 | 一块 | 供电模块，用于为 Arduino和 LCD 液晶屏提供电源。 |
| USB转串口芯片CH340G | 一块 | 用于将 Arduino Mini 的串口信号转换为 USB 信号，可以通过 USB 端口与电脑进行通信，上传程序到 Arduino Mini。 |
| I2C液晶屏转接模块 | 一块 | 用于将 I2C 信号转换为液晶屏可以识别的信号。由于 LCD1602 会占用大量 Arduino 引脚。通过 I2C 液晶屏转接模块转接后，只需要使用两个 Arduino 引脚就能传输数据驱动 LCD1602。 |
| LCD1602 液晶显示屏 | 一块 | 16x2 的液晶显示屏，用于显示数值信息。 |
| LCD12864 液晶显示屏 | 一块 | 128x64 的液晶显示屏，用于显示波形。 |
| 杜邦线 | 若干条 | 连接线，用于连接各个元件。 |
| 面包板 | 若干块 | 用于临时搭建电路的工具，可以方便地插入和移除各种元件。 |

![image](https://github.com/user-attachments/assets/92d471e8-f316-425f-bb3f-8bfd96835c54)

## 硬件连接

### Arduino UNO 与 MB-102电源模块

| Arduino UNO | MB-102电源模块 |
| --- | --- |
| GND | - |
| Vin | + |

### Arduino UNO 与 I2C液晶屏转接模块

| Arduino UNO | I2C液晶屏转接模块 |
| --- | --- |
| GND | GND |
| 5V | VCC |
| A4 | SDA |
| A5 | SCL |

### Arduino UNO 与 I2C液晶屏转接模块

| Arduino UNO | I2C液晶屏转接模块 |
| --- | --- |
| GND | GND |
| 5V | VCC |
| A4 | SDA |
| A5 | SCL |

### Arduino UNO 与 LCD12864 液晶显示屏

| Arduino UNO | LCD12864 液晶显示屏 |
| --- | --- |
| GND | GND |
| 5V | VCC |
| 2 | RS / CS |
| 3 | RW / MOSI |
| 4 | E / CLK |
| Reset | RST |
| GND | PSB |

### Arduino Mini 与 MB-102电源模块

| Arduino Mini | MB-102电源模块 |
| --- | --- |
| GND | - |
| VCC | + |

### Arduino Mini 与 USB转串口芯片CH340G

| Arduino Mini | USB转串口芯片CH340G |
| --- | --- |
| GND | GND |
| VCC | 5V |
| RX | TXD |
| TX | RXD |

### Arduino UNO 与 Arduino Mini

| Arduino UNO | Arduino Mini |
| --- | --- |
| GND | GND |
| A0-A3 | 2-12 |

## 软件说明

- **Arduino IDE**：Arduino IDE 是一个开源的集成开发环境。用户可以通过 Arduino IDE 编写 Arduino 代码，并将其上传到 Arduino 开发板上运行。 Arduino 由于其简单易用、灵活性高以及价格低廉的特点，广泛应用于教育、原型设计和DIY项目中。
- **LiquidCrystal_I2C 库**：用于驱动 LCD1602 液晶显示屏。该库可以通过 I2C 接口与 Arduino 进行通信，只需要两个引脚即可实现数据传输。
- **U8g2 库**：用于驱动 LCD12864 液晶显示屏。该库支持多种显示屏，包括 OLED、LCD、LED 等。可以通过 SPI 或 I2C 接口与 Arduino 进行通信。

## DIY步骤

1. **准备材料**
   - Arduino UNO 开发板
   - Arduino Mini 开发板
   - MB-102 电源模块
   - USB转串口芯片CH340G
   - I2C液晶屏转接模块
   - LCD1602 液晶显示屏
   - LCD12864 液晶显示屏
   - 杜邦线
   - 面包板

2. **连接硬件**
   - 将 Arduino UNO 开发板与 MB-102 电源模块连接，确保供电。
   - 使用杜邦线将 I2C 液晶屏转接模块连接到 Arduino UNO 的 I2C 接口。
   - 将 LCD1602 液晶显示屏连接到 I2C 液晶屏转接模块。
   - 将 LCD12864 液晶显示屏连接到 Arduino UNO 的数字引脚。
   - 将 Arduino Mini 开发板与 USB转串口芯片CH340G连接，确保可以通过 USB 端口与电脑通信。
   - 使用杜邦线将 Arduino Mini 的 2-12 引脚连接到面包板，用于输出不同周期的方波信号。

3. **安装软件**
   - 下载并安装 Arduino IDE。
   - 在 Arduino IDE 中安装所需的库，包括 LiquidCrystal_I2C 库和 U8g2 库。

4. **上传代码**
   - 将示波器程序代码上传到 Arduino UNO 开发板。
   - 将简易信号发生器程序代码上传到 Arduino Mini 开发板。

5. **调试**
   - 确保所有连接正确后，接入电源，并打开 MB-102 电源模块上的开关。
   - 使用简易信号发生器来测试示波器的功能。
   - 检查显示屏是否正确显示数值和波形。

## 注意事项

- 在连接硬件时，请确保所有元件的极性正确，避免短路或损坏。
- 如果液晶屏显示异常或不显示，可以尝试调节液晶屏背面或者转接模块上的对比度电位器。如果还是没有显示，请测量所有导线是否导通。
- 在使用示波器测量时，输入电压应控制在 5V 以内，否则可能会烧坏 Arduino 开发板。

## 效果展示

![image](https://github.com/user-attachments/assets/7d5b0bbb-d86c-4de5-9dc3-ba644b0520e4)

![image](https://github.com/user-attachments/assets/3c69a3fd-114b-409c-a2e1-45406b9863c9)

## 参与贡献

- 如果你觉得这个项目对你有所帮助，欢迎给个 Star⭐️。
- 如果你有任何问题或建议，欢迎提交 Issue。
- 如果你有兴趣参与贡献代码，欢迎提交 Pull Request。

## 许可

本项目采用 GPL-3.0 license 进行许可，详情请参阅 [LICENSE](LICENSE) 文件。

