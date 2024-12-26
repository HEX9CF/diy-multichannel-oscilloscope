# 💡 DIY Multi-Channel Oscilloscope Based on Arduino UNO 🪛

[English](README.md) | [中文](README_ZH.md)

## Project Introduction

An oscilloscope is a device used to observe various types of signal voltages 📉. On a graphical display, an oscilloscope can represent voltage as a one-dimensional graph, where one axis represents time ⏱️ and the other represents voltage ⚡. This allows observers to see how the signal changes over time, such as the periodic fluctuations of the signal. As an important electronic measurement tool 🔧, oscilloscopes are widely used in circuit design, fault diagnosis, education, teaching, and scientific research 📚🔬. However, due to their high cost 💰, they may be unaffordable for students. Therefore, the author aims to use an Arduino development board to build a low-cost, multi-channel simple oscilloscope to support students' learning and research activities, providing a practical tool for electronics and electrical engineering education 🛠️.

The Arduino Uno development board has 6 analog input pins, labeled A0 to A5. These pins can be used to read the output from sensors or other analog signals from devices. These signal voltages range between 0 and 5 volts. Arduino converts this analog voltage to an integer between 0 and 1023. By using these analog input pins, four analog signals are read. Then, the Arduino's analogRead() function is used to read the voltage of an analog pin. After calculation, the actual value, average value, maximum value, and minimum value are output to the LCD1602, and the waveform image is drawn on the LCD12864.

To test the effectiveness of the oscilloscope, the project includes a simple signal generator based on Arduino Mini, which can output square wave signals of different periods from pins 2 to 12.

## Feature Introduction

### Four-Channel Analog Signal Input
The oscilloscope can simultaneously receive and process four analog signals, which can come from various sensors or other electronic devices. The oscilloscope samples every 20ms, with a sampling frequency of 50Hz.

### Numerical Display
The oscilloscope uses a 16x2 LCD1602 display screen to show information. The screen displays four parameters: voltage value, average value, minimum value, and maximum value, switching between channels every two seconds.

### Waveform Display
The oscilloscope uses a 128x64 LCD12864 display screen to show waveforms. The screen is divided into four regions: top-left, top-right, bottom-left, and bottom-right, displaying signal waveforms input from the A0, A1, A2, and A3 analog input pins, respectively. Each region has a channel label in the top-left corner to indicate the corresponding analog input pin.

![image](https://github.com/user-attachments/assets/87396110-d8ca-4106-9f47-4037a88eb5ac)

## Hardware Description

| Device | Quantity | Description |
| --- | --- | --- |
| Arduino UNO | 1 piece | Main controller, responsible for reading analog signals, processing data, and controlling the display screens to show waveforms. |
| Arduino Mini | 1 piece | Acts as a signal generator, capable of outputting square wave signals of different periods from pins 2 to 12. |
| MB-102 Power Module | 1 piece | Power supply module, used to provide power to the Arduino and LCD screens. |
| USB-to-Serial Chip CH340G | 1 piece | Used to convert the serial port signals of the Arduino Mini to USB signals, allowing communication with a computer via USB port and uploading programs to the Arduino Mini. |
| I2C LCD Adapter Module | 1 piece | Used to convert I2C signals to signals recognizable by the LCD screen. Since the LCD1602 occupies many Arduino pins, using the I2C LCD adapter module reduces the requirement to just two Arduino pins for data transmission to the LCD1602. |
| LCD1602 Liquid Crystal Display | 1 piece | 16x2 liquid crystal display, used to show numerical information. |
| LCD12864 Liquid Crystal Display | 1 piece | 128x64 liquid crystal display, used to show waveforms. |
| Dupont Wires | Several | Connecting wires, used to connect various components. |
| Breadboard | Several | Tools for temporarily setting up circuits, allowing easy insertion and removal of various components. |

![image](https://github.com/user-attachments/assets/92d471e8-f316-425f-bb3f-8bfd96835c54)

## Hardware Connections

### Arduino UNO and MB-102 Power Module

| Arduino UNO | MB-102 Power Module |
| --- | --- |
| GND | - |
| Vin | + |

### Arduino UNO and I2C LCD Adapter Module

| Arduino UNO | I2C LCD Adapter Module |
| --- | --- |
| GND | GND |
| 5V | VCC |
| A4 | SDA |
| A5 | SCL |

### Arduino UNO and LCD12864 Liquid Crystal Display

| Arduino UNO | LCD12864 Liquid Crystal Display |
| --- | --- |
| GND | GND |
| 5V | VCC |
| 2 | RS / CS |
| 3 | RW / MOSI |
| 4 | E / CLK |
| Reset | RST |
| GND | PSB |

### Arduino Mini and MB-102 Power Module

| Arduino Mini | MB-102 Power Module |
| --- | --- |
| GND | - |
| VCC | + |

### Arduino Mini and USB-to-Serial Chip CH340G

| Arduino Mini | USB-to-Serial Chip CH340G |
| --- | --- |
| GND | GND |
| VCC | 5V |
| RX | TXD |
| TX | RXD |

### Arduino UNO and Arduino Mini

| Arduino UNO | Arduino Mini |
| --- | --- |
| GND | GND |
| A0-A3 | 2-12 |

## Software Description

- **Arduino IDE**: Arduino IDE is an open-source integrated development environment. Users can write Arduino code in the Arduino IDE and upload it to the Arduino development board to run. Arduino is widely used in education, prototyping, and DIY projects due to its ease of use, flexibility, and low cost.
- **LiquidCrystal_I2C Library**: Used to drive the LCD1602 liquid crystal display. This library can communicate with Arduino via the I2C interface, requiring only two pins for data transmission.
- **U8g2 Library**: Used to drive the LCD12864 liquid crystal display. This library supports various displays, including OLED, LCD, LED, etc., and can communicate with Arduino via SPI or I2C interfaces.

## DIY Steps

1. **Prepare Materials**
   - Arduino UNO development board
   - Arduino Mini development board
   - MB-102 power module
   - USB-to-Serial chip CH340G
   - I2C LCD adapter module
   - LCD1602 liquid crystal display
   - LCD12864 liquid crystal display
   - Dupont wires
   - Breadboard

2. **Connect Hardware**
   - Connect the Arduino UNO development board to the MB-102 power module to ensure power supply.
   - Use Dupont wires to connect the I2C LCD adapter module to the Arduino UNO's I2C interface.
   - Connect the LCD1602 liquid crystal display to the I2C LCD adapter module.
   - Connect the LCD12864 liquid crystal display to the Arduino UNO's digital pins.
   - Connect the Arduino Mini development board to the USB-to-Serial chip CH340G to ensure communication with the computer via USB port.
   - Use Dupont wires to connect pins 2-12 of the Arduino Mini to the breadboard for outputting square wave signals of different periods.

3. **Install Software**
   - Download and install the Arduino IDE.
   - Install the required libraries in the Arduino IDE, including the LiquidCrystal_I2C library and the U8g2 library.

4. **Upload Code**
   - Upload the oscilloscope program code to the Arduino UNO development board.
   - Upload the simple signal generator program code to the Arduino Mini development board.

5. **Debug**
   - Ensure all connections are correct, then power on and turn on the switch on the MB-102 power module.
   - Use the simple signal generator to test the functions of the oscilloscope.
   - Check if the display screens correctly show the numerical values and waveforms.

## Precautions

- When connecting hardware, ensure the polarity of all components is correct to avoid short circuits or damage.
- If the liquid crystal display shows abnormalities or no display, try adjusting the contrast potentiometer on the back of the display or the adapter module. If there is still no display, check if all wires are conducting.
- When using the oscilloscope for measurements, ensure the input voltage is controlled within 5V to avoid damaging the Arduino development board.

## Effect Display

![image](https://github.com/user-attachments/assets/7d5b0bbb-d86c-4de5-9dc3-ba644b0520e4)

![image](https://github.com/user-attachments/assets/3c69a3fd-114b-409c-a2e1-45406b9863c9)

## Contribution

- If you find this project helpful, please give it a Star⭐️.
- If you have any questions or suggestions, welcome to submit an Issue.
- If you are interested in contributing code, welcome to submit a Pull Request.

## License

This project is licensed under the GPL-3.0 license, details can be found in the [LICENSE](LICENSE) file.