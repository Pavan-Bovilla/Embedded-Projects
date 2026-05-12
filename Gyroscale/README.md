# Gyroscale
Gyroscale is a smart digital angle measuring device which can replace minidrafter, protractor, setsquares and scale etc.


## The Story Behind Gyroscale
During my engineering drawing classes, I really struggled with the traditional minidrafter. It takes about 10 to 15 minutes just to set it up before you can draw a  single line. Plus, carrying an 1kg machine to class is a big physical hassle. That daily frustration gave me the idea for this project.  Gyroscale is a small,digital scale that tells you its tilt angle in real time on a little screen. Unlike the old tools, you can use it on any flat surface without a fixed table, and it fits right in your bag

## How It Works
The Gyroscale uses a GY-271 magnetometer to sense the Earth's magnetic field. The main brain of the device is an STM32 "Blue Pill" microcontroller. It takes the sensor readings, calculates the angle using a simple math function, and shows the result on a small OLED display. The microcontroller, sensor, and display all talk to each other using the I2C communication protocol.

<img width="432" height="272.8" alt="Screenshot_20260512-144555" src="https://github.com/user-attachments/assets/d7859390-817d-4055-bab8-751bbc8a5196" />

<img width="432" height="272.8" alt="Screenshot_20260512-143910" src="https://github.com/user-attachments/assets/7089ddcc-d037-4d49-89fa-671c6336303f" />

## Hardware Needed
* Microcontroller: STM32F103C8T6 (Blue Pill)
* Sensor: GY-271 module (HMC5883L magnetometer)
* Display: 0.96-inch SSD1306 OLED screen
* Extras: A 30 cm plastic ruler, jumper wires, a push button, and a few 4.7 kΩ pull-up resistors \
The total cost to build this prototype is under INR 400.




## connections 
### Power Connections
The entire system operates on 3.3V logic. 
* STM32F103C8T6 (Blue Pill): Can be powered via its micro-USB port (using a power bank or laptop).
* GY-271 (HMC5883L): Connect its VCC pin to the 3.3V output pin on the STM32.
* SSD1306 OLED: Connect its VCC or VDD pin to the 3.3V output pin on the STM32.
* Ground: Connect the GND pins of the GY-271 and the SSD1306 to any GND pin on the STM32.All grounds must be tied together.
### I2C Data Connections (I2C1 Bus)
Both the sensor and the display connect to the I2C1 bus of the STM32. On a standard STM32 Blue Pill, the I2C1 pins are PB6 and PB7.
* SCL (Clock Line): Connect the SCL pins of both the GY-271 and the SSD1306 to the PB6 pin on the STM32.
* SDA (Data Line): Connect the SDA pins of both the GY-271 and the SSD1306 to the PB7 pin on the STM32.
### Pull-Up Resistors(if needed)
* Connect one 4.7 kΩ resistor between the 3.3V line and the SDA line.
* Connect another 4.7 kΩ resistor between the 3.3V line and the SCL line. \
(Note: Some pre-made sensor or display modules already have pull-up resistors soldered onto their tiny circuit boards. If your I2C communication fails or hangs, double-check if adding external resistors makes it too strong, but definitely follow your report's spec first!)

## Key Features
* Super Fast Setup: It is ready to use in under 5 seconds, compared to the long setup of a minidrafter.
* Highly Portable: It weighs only about 200 grams, making it pocket-sized.
* Easy Calibration: You just press one button to set your zero reference angle.
* Practical Accuracy: It gives an accuracy of around 4 to 5 degrees, which is a good trade-off for quick student drawings.

## Software Details
The code is written in C using STM32CubeIDE.
* It uses HAL (Hardware Abstraction Layer) drivers for easy I2C setup.
* The magnetometer runs in continuous-measurement mode at 15 Hz.
* The raw X and Y axis data are converted into degrees using the atan2 function.
