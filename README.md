# Real-Time LED-Based Orientation Indicator Using STM32 and Jetson Nano

https://github.com/Sorna-Xerxes/Jetson-Nano-RxTx-Gyro-from-STM32-with-LED/assets/147555989/62ed350d-d964-43b5-94dd-c907737a6582


## INTRODUCTION
- **Objective**: Visually represent roll, pitch, and yaw of an STM32 development board using onboard LEDs.
- **Data Source**: *Gyroscopic data* collected by the STM32 board.
- **Data Transmission**: Data transmitted over *USB* to a Jetson Nano.
- **Data Processing and Control**: *Python script* running on Jetson Nano receives the data and parses it then dynamically controls onboard LEDs of the STM32.
- **Real-time Feedback**: *LEDs* provide real-time indication of device orientation relative to the horizontal plane.

## SYSTEM OVERVIEW
The following **block diagram** illustrates the system architecture and data flow between the components:

![image](https://github.com/Sorna-Xerxes/Jetson_Nano_Rx_STM32_Gyro_Tx_LED/assets/147555989/c39454e1-ed12-4318-866a-b4732e7baae8)




### Hardware Requirements:

**1. STM 32 F3 Discovery (Micro Controller):** The STM32F3 series microcontrollers are commonly used in a wide range of embedded applications, including industrial automation, consumer electronics, and IoT devices. They are suitable for applications that require precise timing, sensor data acquisition, and control tasks.
- ARM Cortex-M4 core
- Onboard Sensors (MEMS Gyroscope, MEMS Accelerometer, e-Compass)
- lower processing power and are optimized for low power consumption 
- Integrated peripherals such as GPIO, UART, SPI, I2C, ADC, DAC, timers, and PWM controllers.![L3GD20_Gyroscope](https://github.com/Sorna-Xerxes/Jetson-Nano-RxTx-Gyro-from-STM32-with-LED/assets/147555989/abb31c4b-3062-4631-b696-ae6d6915a9f0)




https://github.com/Sorna-Xerxes/Jetson-Nano-RxTx-Gyro-from-STM32-with-LED/assets/147555989/e3f29be0-a8b1-41d4-a662-0e4d1704ee91


**2. NVDIA Jetson Nano (Micro Processor):** The NVIDIA Jetson Nano is a small, powerful computer designed for AI and robotics applications. Jetson Nano is capable of running complex algorithms and deep learning models, making it suitable for tasks such as image recognition, object detection, and autonomous navigation.
- Quad-core ARM Cortex-A57 CPU with a NVIDIA Maxwell GPU.
- Various interfaces: USB, HDMI, Ethernet, CSI camera interface, and GPIO headers.

![Jetson_Nano](https://github.com/Sorna-Xerxes/Jetson_Nano_Rx_STM32_Gyro_Tx_LED/assets/147555989/62be1bb8-5a20-448f-b5b2-cfbc1a061141)



### Software Requirements:

**1.STM32 Cube IDE:** Using STM32CubeIDE, an integrated development environment for STM32 microcontrollers, the firmware is developed to interface with the gyroscope sensor, collect data from onboard sensors, read the roll, pitch, and yaw angles, and transmit them over USB to the Jetson Nano.

**2. Visual Studio Code:** Visual Studio Code connects to the NVIDIA Jetson Nano through a remote connection. The Python script running on the Jetson Nano communicates with the STM32 board over USB to receive gyroscopic data. It reads and parses the received data to extract the roll, pitch, and yaw angles, and then controls the onboard LEDs of the STM32 board to visually indicate these angles. The script utilizes the PySerial library for serial communication with the STM32 board.

### Data Parameters:
- **Roll Angle:** The angle of rotation around the longitudinal axis of the STM32 board, measured in degrees.
- **Pitch Angle:** The angle of rotation around the lateral axis of the STM32 board, measured in degrees.
- **Yaw Angle:** The angle of rotation around the vertical axis of the STM32 board, measured in degrees.
  
![Aircraft_Axis](https://github.com/Sorna-Xerxes/Jetson_Nano_Rx_STM32_Gyro_Tx_LED/assets/147555989/908bf1d1-fe9f-48da-80b2-1946cadb9f12)


## INSTRUCTIONS
To run the code:

### STM32 Firmware:
- Import the provided STM32 project file Project_Gyro.zip into STM32CubeIDE. (Unarchive it into the STM32 Workspace before importing).
- All necessary project configurations, such as enabling USB communication and integrating the gyroscope sensor, have already been pre-configured. These settings encompass connectivity interfaces (SPI, I2C), clock configurations, baud rates (9600), etc.
- Flash the firmware onto the STM32 development board using STM32CubeIDE.
  
![STM32_Printout_ _Configurations](https://github.com/Sorna-Xerxes/Jetson-Nano-RxTx-Gyro-from-STM32-with-LED/assets/147555989/96b94cbe-d52a-43ed-8354-0e616d482035)

  
### Jetson Nano Connection with Visual Code:

- **Jetson Nano runs headless:** It operates without a monitor, keyboard, or mouse.
- **Configure network for SSH access:** Adjust network settings to connect to Jetson Nano remotely.
- **Use Visual Studio Code to manage port gateway:** VS Code sets up communication with Jetson Nano.Ensure that Python 3 is installed on Visual Code. Install the necessary dependencies by running the following command in the terminal:

Install pySerial on Jetson Nano
```bash
unzip pyserial-master.zip
cd pyserial-master
sudo python3 setup.py install
```
- **Setup Communication Device Class on STM32:**
Once connected figure out the address of the STM32, this can be done by running the following command in the terminal:
```bash
ls /dev/ttyA*
```
   set the access permissions on the device’s address by running the following, remembering to replace with the device’s address.
```bash
sudo chmod 666 /dev/ttyACM0
```
## PYTHON SCRIPT LOGIC
The `VS Code - X,Y,Z LED Logic (Final).py` provides real-time indication of the roll, pitch and yaw angles of the STM32 development board through the onboard LEDs. As the orientation of the board changes, the LEDs adjust accordingly to reflect the current roll and pitch angles. This visual feedback allows users to monitor the orientation of the device and make informed decisions based on its position

- **Request Gyro data**: print X,Y,Z of Previous posiiton, Current Position
- **Parsing Gyro Data**: calculates its difference
- **LED Logic**:
```
x_diff is > 5000, it's a "Pitch Down" movement. (LED 4)
x_diff is < -5000, it's a "Pitch Up" movement. (LED 0)
y_diff is > 20000, it's a "Roll West" movement (LED 6)
y_diff is < -20000, it's a "Roll East" movement. (LED 2)
```
## OUTCOME
The STM32 Roll, Pitch and Yaw Indicator project demonstrates the integration of gyroscopic data sensing and LED control to create a practical orientation indicator system. The project showcases the capabilities of microcontroller-based systems for sensor integration and real-time data processing. Additionally, the project serves as a foundation for further exploration into embedded systems development and sensor-based applications.

## DEPENDENCIES

- **PySerial:** It is a Python library used for serial communication. It provides support for accessing serial ports and communication with serial devices. Install PySerial using the following command:
```bash
pip install pyserial
```
- **re:** The regular expression module in Python, utilized for pattern matching with regular expressions. In this context, it's employed to `extract x, y, and z coordinates from gyro data`.

- **time:** Python's standard library module offering various time-related functions. Within the code, it `introduces delays between operations`, preventing the code from executing too rapidly and potentially overloading the connected device.

## TABLE OF CONTENTS

| File Name        | Brief           |
| ------------- |:-------------:|
| Project_Gyro_LED.zip      | Contains the entire STM32 project that is to be flashed onto the STM32 |
| VS Code - 4 LED Logic      | Contains the Python script with 4 LED Logic that is to be run in VS Code after setting up the connection      |
| pyserial-master.zip      | Install pySerial on Jetson Nano      |
|  VS Code - 8 LED Logic      | Contains the Python code with 8 LED logic where the code can be improvised with data parsing or improvising using data fusion      |

## CREDITS
The STM32F3 discovery board and Jetson Nano were provided as part of the project materials for the completion of our coursework in Embedded Systems for the MSc in Robotics, AI, and Autonomous Systems at City, University of London.

## CONTRIBUTIONS ARE WELCOMED
Contributions to this project are highly appreciated. To contribute:
- Fork the repository.
- Make your changes or enhancements.
- Submit a pull request for review.

## LICENSE
This project is licensed under the MIT License.
