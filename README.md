[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/kzkUPShx)
# final-submission

    * Team Number: 21
    * Team Name: V50
    * Team Members: Gengzhi Zhu & Yuetian Zhao & Ruilong Liu
    * Github Repository URL: https://github.com/upenn-embedded/final-project-v50
    * Github Pages URL: https://yuetianzhao.github.io/team21.github.io/
    * Description of test hardware: 
         STM32 Microcontroller
         ATMEGA328PB Microcontroller
         MAX4466 Microphone Sensor
         1.8" Color TFT LCD with SPI Interface
         3 LEDs
         RC Servo motor

## 1. Video Presentation
<div align="center">
  <a href="https://drive.google.com/file/d/1EQbMuIp2Q4er1tXsdoMXXYFDCgoy8Ak6/view?usp=sharing">
     <img src="https://github.com/yuetianzhao/team21.github.io/blob/main/235ca63143c26eed49d467f0db3566a5.jpg" width="500">
  </a>
</div>


## 2. Project Summary and images
<div align="center">
<table><tr>
<td><img src="https://github.com/ese5160/a14g-final-submission-t05-product-scanner/blob/main/Screenshoot%20and%20photo/Userpage.png" width="1000"/></td>
<td><img src="https://github.com/ese5160/a14g-final-submission-t05-product-scanner/blob/main/Screenshoot%20and%20photo/Qrcode%20scanner.png" width="1000"/></td>
</tr><tr>
<td colspan="2"><img src="https://github.com/ese5160/a14g-final-submission-t05-product-scanner/blob/main/Screenshoot%20and%20photo/OTAFU.jpg" width="1000"/></td>
</tr></table>
</div>
*Description: Screenshot of the Node-RED backend, illustrating the flow and logic used to process data.*
### Device Description
Our device aims to create a sound detect system, allowing users to speak and the RC SERVO motor will rotate to follow the source of the sound. Users can use LCD to check the different component of the frequency. Moreover, LEDs can also be a way to show the source of the sound(left, front, right).

### Inspiration
The inspiration for our sound detection system comes from the challenges faced by cameramen in dynamic environments, where quickly identifying and tracking the source of a sound is crucial. Imagine a live event or a documentary shoot—cameramen often need to react swiftly to unexpected sound cues, such as a speaker's voice, a sudden noise, or other auditory signals. By enabling the camera to automatically identify and follow the source of the sound, our system aims to revolutionize filming dynamics, enhancing efficiency and ensuring that key moments are captured seamlessly. This innovation bridges the gap between auditory and visual tracking, empowering creators to focus on storytelling rather than manual adjustments.

### Device Functionality
Our sound detection and tracking system is designed to seamlessly integrate auditory and visual intelligence, offering the following key functionalities:
1. Sound Source Tracking: The system identifies the direction of the sound source in real time, distinguishing whether it is coming from the left, right, or directly in front of the device.
2. Directional Sound Information Display: It visually displays the detected sound's directional information, categorizing it into left, right, or front regions for intuitive understanding.
3. Frequency Component Analysis: The system analyzes the frequency components of the detected sound, providing detailed insights into the audio characteristics of each directional segment.
4. Motorized Camera Rotation: The system is equipped with motorized rotation capabilities, enabling the camera to automatically orient itself toward the source of the sound, ensuring accurate tracking and capturing of the scene.



### Challenges
In general, we faced four challenges and partly solved them in the right way.

#### 1. Microphone Calibration for Accuracy
One of the key challenges is the microphone's initial inaccuracy in detecting and localizing sound sources. Precise sound direction detection requires meticulous calibration to ensure the system's reliability. This calibration process can be time-consuming, especially in environments with varying acoustics or interference, requiring careful adjustments to align the microphone array for optimal performance.
#### 2. UART and Timer1 Conflict for Motor Rotation
Another significant challenge is managing the conflict between the UART communication protocol and Timer1, which controls the motor rotation. Both functionalities are critical, but their simultaneous operation can lead to timing issues and resource contention. Resolving this conflict requires efficient scheduling or alternative methods, such as interrupt-driven mechanisms or prioritization strategies, to ensure seamless motor control without disrupting data communication.


## 3. Hardware & Software Requirements

### Hardware Requirements

#### HRS 01 - SAMW25 Microcontroller
Our project is based on a self-designed PCB. The MCU of this PCB is the SAMW25 microcontroller, with J-link used to flash the code into the PCB.

#### HRS 02 - SHTC3-TR-10KS Sensor
In compliance with HRS 02, our system employs the SHTC3-TR-10KS sensor, which detects a wide range of temperature (-40 °C to 125 °C) and humidity (0 to 100 %RH). The typical accuracy is ±2 %RH for humidity and ±0.2°C for temperature, but our software configuration displays accuracy to ±1°C for temperature and ±1 %RH for humidity due to integer data type limitations.

#### HRS 03 - 1.8" Color TFT LCD with SPI Interface
The implementation of the 1.8" Color TFT LCD with an SPI interface in our project was crucial for displaying detailed product information. This LCD module communicates with the microcontroller through the SPI, ensuring swift and stable data updates.

#### HRS 04 - Tiny Code Reader from Useful Sensors
The Tiny Code Reader captures and interprets QR codes effectively, with an LED indicator that signals the scanning process status. It communicates with the microcontroller via I2C, changing from blue to green upon a successful scan.

#### HRS 05 - ADA1201 Vibrating Motor
The ADA1201 vibrating motor is integrated as a tactile feedback mechanism. It sends a vibration alert each time an item is scanned and when the user finishes shopping, enhancing the user experience with immediate physical feedback.

#### HRS 06 - System Integration and Control
Our development team has implemented a system that integrates multiple hardware components to ensure smooth and efficient operation. The device operates on a 3.7V Li-Ion battery, with a tested continuous operational capability of at least 3 hours.

### Software Requirements

#### SRS 01 - QR Code Scanning and Processing
The Adafruit 5744 QR code reader scans QR codes on products with a response time of less than 2 seconds per scan. While the I2C protocol speed is assumed to be efficient, we lack tools to measure the exact speed, focusing on the operational performance.

#### SRS 02 - Display Management
We manage a 1.8" Color TFT LCD screen with an SPI interface, capable of displaying product details. Current performance shows a refresh time of approximately one to two seconds, slower than the desired 500 milliseconds.

#### SRS 03 - Temperature and Humidity Monitoring
The software interfaces with the SHTC3-TR-10KS sensor, collecting and transmitting temperature and humidity data every 5 seconds via MQTT to Node-RED for real-time monitoring and analysis.

#### SRS 04 - Wireless Data Transmission
Using the SAMW25 Wi-Fi microcontroller, our system handles data transmission over a 2.4 GHz Wi-Fi network, supporting 802.11 b/g/n standards with a minimum data transfer rate of 150 Mbps. It seamlessly connects to various networks and interfaces with different server configurations.

#### SRS 05 - User Interaction and Feedback
The ADA1201 vibrating motor is controlled by software to activate for 0.5 seconds for scan confirmations and alerts, with a slight delay in the vibration timing due to code issues but still delivering timely feedback.


## 4. Project Photos & Screenshots



## 5. Project Codebase Links
- **Node-RED instance:** [http://52.177.130.52:1880/ui](http://52.177.130.52:1880/ui)
- **A12G Code Repository:** [GitHub Repository](https://github.com/ese5160/a12g-firmware-drivers-t05-product-scanner)
- **Final PCBA on Altium 365:** [Altium 365 Link](https://upenn-eselabs.365.altium.com/designs/CA7AC7AB-A449-4488-9C62-C8DDCABF01EC)
