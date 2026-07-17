# Controllers 

<p align="center">
  <img src="https://raw.githubusercontent.com/thkaratsis/Mitsos----An-Open-Source-AI-Humanoid-Robot/main/schemes/Controllers/Controllers.png" alt="Power Management Schematic" width="900">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/thkaratsis/Mitsos----An-Open-Source-AI-Humanoid-Robot/main/schemes/Controllers/Controllers_Diagram.drawio" alt="Power Management Schematic" width="900">
</p>


The robot's main controller is the **Raspberry Pi 5**, a powerful single-board computer (SBC) responsible for high-level control, computer vision, and AI inference. An **ESP32-S3-N8R8** microcontroller is used alongside the Raspberry Pi to accurate controll and gather data from all of the sensors.

To ensure reliable communication between the two processing units, the **Raspberry Pi 5** and the **ESP32-S3-N8R8** exchange data over a **full-duplex UART interface**. This bidirectional communication enables simultaneous transmission and reception of commands and sensor data.

The **Raspberry Pi 5** performs the high-level control tasks, generating servo commands and transmitting them to the ESP32. The **ESP32**, acting as the real-time controller, executes these commands while continuously collecting data from all onboard sensors and transmitting the measurements back to the Raspberry Pi.This set up allows the Raspberry Pi to focus on AI and navigation while the ESP32 handles real-time hardware interaction.
