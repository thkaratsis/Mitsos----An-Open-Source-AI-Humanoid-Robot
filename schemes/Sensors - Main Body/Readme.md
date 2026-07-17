# Sensors- Main Body

<p align="center">
  <img src="https://raw.githubusercontent.com/thkaratsis/Mitsos----An-Open-Source-AI-Humanoid-Robot/main/schemes/Sensors - Main Body/Sheet_3.png" alt="" width="900">
</p>


# Distance Sensors

To enable safe and autonomous navigation, the robot is equipped with **five VL53L0X Time-of-Flight (ToF) distance sensors**. These measure the distance to nearby objects, allowing the robot to avoid obstacles, navigate environments, and estimate its surroundings with millimeter-level precision.

Each sensor is mounted at a location to maximize environmental coverage:

1. **Head-Mounted ToF** – Installed on top of the robot's head. Mounted on a two-axis mechanism driven by **two MG90S servos**, allowing it to scan the environment similarly to a low-cost LiDAR.
2. **Rear ToF** – Positioned at the back of the robot to monitor obstacles while reversing.
3. **Front ToF** – Mounted on the front of the robot and angled **30° downward** to detect obstacles and changes in terrain directly ahead.
4. **Front-Right ToF** – Mounted at the front and angled **30° to the right** for obstacle detection during turns.
5. **Front-Left ToF** – Mounted at the front and angled **30° to the left** to provide additional environmental awareness.

Together, these sensors provide nearly **360° obstacle awareness**, enabling the robot to navigate safely.

## VL53L0X Specifications

| Specification | Value |
|---|---|
| Sensor Type | Time-of-Flight (ToF) |
| Measuring Range | 3 cm – 2 m |
| Resolution | 1 mm |
| Accuracy | ±3% to ±5% |
| Interface | I²C |
| Default I²C Address | 0x29 |
| Field of View (FOV) | 25°–35° |
| Operating Voltage | 2.6–3.5 V |


> **Address Configuration**
>
> All **VL53L0X** sensors share the same default **I²C address (0x29)**. Since multiple sensors are connected to the same I²C bus, each sensor's **XSHUT** pin is connected to a dedicated GPIO pin on the **ESP32-S3**.
>
> During system startup, the ESP32 keeps all sensors in hardware shutdown. It then enables them **one at a time**, assigns each sensor a unique I²C address through software, and finally activates the next sensor. This initialization process allows all five VL53L0X sensors to operate simultaneously on the same I²C bus without address conflicts.

# Inertial Measurement Unit (IMU)

Maintaining balance is one of the most important parts of a humanoid robot. To achieve this, the robot is equipped with an **LSM6DS3 Inertial Measurement Unit (IMU)**, which  measures both **linear acceleration** and **angular velocity** along the **X, Y, and Z axes**.

The IMU provides real-time orientation and motion data, allowing the robot to detect body tilt, acceleration, and rotational movement. This information is used by the control algorithms to maintain stabilit and achieve smooth walking and motion sequences.

The LSM6DS3 combines a **3-axis accelerometer** and a **3-axis gyroscope** into a single low-power package, making it an ideal sensor for humanoid robotics applications.

## LSM6DS3 Specifications

| Specification | Value |
|---|---|
| Sensor Type | 6-Axis Inertial Measurement Unit (IMU) |
| Accelerometer | 3-Axis |
| Gyroscope | 3-Axis |
| Accelerometer Range | ±2 / ±4 / ±8 / ±16 g |
| Gyroscope Range | ±125 / ±245 / ±500 / ±1000 / ±2000 dps |
| Operating Voltage | 1.71 V – 3.6 V |
| Interface | I²C (up to 1 MHz) or SPI (up to 10 MHz) |
| Default I²C Address | 0x6A (0x6B configurable) |
| Output Data Rate | Up to 6.66 kHz |
| Power Consumption | As low as 0.9 mA (typical) |

> **Sensor Integration**
>
> The **LSM6DS3** is connected to the **ESP32-S3** through the **I²C bus**. The ESP32 continuously gathers acceleration and gyroscope measurements, processes the raw sensor data, and transmits orientation and motion information to the **Raspberry Pi 5** via the **UART** interface. This allows the ESP32 to perform  real-time sensor acquisition while the Raspberry Pi focuses on high-level control


# Servo Controller

The robot is actuated by a total of **16 servo motors**, each requiring three electrical connections: **Power (V+), Ground (GND), and a PWM control signal**. Driving all servos directly from the ESP32 would require a large number of GPIO pins, making the design unnecessarily complex.

To simplify the hardware architecture, the robot uses **two PCA9685 16-channel PWM controllers**, which communicate with the **ESP32-S3** over the **I²C bus**. This allows all servos to be controlled using only two communication lines (SDA and SCL), while providing precise 12-bit PWM signals for every servo.

The first PCA9685 is dedicated to the **leg servos (8× WP5335)**, while the second controls the **arm servos (6× MG996R)** and the **head pan-tilt mechanism (2× MG90S)**.

Although the PCA9685 includes a **V+** terminal for powering servos, the board is designed for voltages up to approximately **6.5 V**. Since the **WP5335** servos achieve their maximum performance at **8.4 V (VBAT)**, they are powered directly from the battery through dedicated header pins installed on the custom PCB. The PCA9685 is therefore used only to provide the PWM control signals for these servos.

The **MG996R** arm servos and **MG90S** head servos operate from **V+** and are powered directly through the PCA9685 module.



## Servo Types

| Servo | Quantity | Location | Operating Voltage |
|---|:---:|---|:---:|
| WP5335 | 8 | Legs | 8.4 V (VBAT) |
| MG996R | 6 | Arms | 5 V |
| MG90S | 2 | Head Pan-Tilt | 5 V |



## PCA9685 Specifications

| Specification | Value |
|---|---|
| Device | PCA9685 |
| Function | 16-Channel PWM Servo Controller |
| Channels | 16 |
| PWM Resolution | 12-bit (4096 steps) |
| PWM Frequency | 24 Hz – 1.6 kHz |
| Communication Interface | I²C |
| Logic Voltage (VCC) | 3.3–5 V |
| Servo Supply (V+) | Up to 6.5 V |
| Maximum Modules | 62 on one I²C bus |


<table style="border:none;">
<tr style="border:none;">

<td valign="top" width="34%" style="border:none; padding-right:20px;">

<b>WP5335 (Legs)</b>

| Joint | Ch |
|---|:---:|
| Left Pelvis | 4 |
| Left Hip | 11 |
| Left Knee | 9 |
| Left Ankle | 14 |
| Right Pelvis | 5 |
| Right Hip | 10 |
| Right Knee | 8 |
| Right Ankle | 15 |

</td>

<td valign="top" width="33%" style="border:none; padding:0 20px;">

<b>MG996R (Arms)</b>

| Joint | Ch |
|---|:---:|
| Left Shoulder | 0 |
| Left Elbow | 2 |
| Left Hand | 4 |
| Right Shoulder | 1 |
| Right Elbow | 3 |
| Right Hand | 5 |

</td>

<td valign="top" width="33%" style="border:none; padding-left:20px;">

<b>MG90S (Head)</b>

| Joint | Ch |
|---|:---:|
| X-axis | 14 |
| Y-axis | 15 |

</td>

</tr>
</table>

# Camera

The robot is equipped with an **IMX219 camera module**, which its primary vision sensor.

Its applications includes **AI-based object detection**, **embedded vision-language models (Vision LLMs)**, and **inverse kinematics**. By combining computer vision with AI inference, the robot can identify and classify objects, estimate their position relative to its body, and calculate the arm movements required to grasp or interact with them. The camera also supports future applications such as visual navigation, human detection, gesture recognition, and object tracking.


## IMX219 Camera Specifications

| Specification | Value |
|---|---|
| Sensor | Sony IMX219 |
| Resolution | 8 Megapixels |
| Maximum Still Resolution | 3280 × 2464 pixels |
| Video Resolution | 1080p @ 30 FPS |
| Maximum Frame Rate | Up to 120 FPS (reduced resolution) |
| Sensor Size | 1/4" CMOS |
| Pixel Size | 1.12 μm × 1.12 μm |
| Interface | MIPI CSI-2 (2-lane) |
| Focus | Fixed Focus |
| Field of View | ~62.2° Horizontal |
| Operating Voltage | 3.3 V |


## Ribbon Connector

The robot utilizes **two custom-designed boards**: a **main board**, located inside the robot's torso, and a **secondary head board**, mounted inside the head. 

The two boards are connected through a **16-pin ribbon cable**, which gives both power and communication signals between the body and the head. This connection distributes **5 V** and **3.3 V** power while also providing **I²S** and **SPI** communication interfaces for the sensors and peripherals mounted on the head.

## 16-Pin Ribbon Cable Pinout

| Pin | Signal | Description |
|:---:|---|---|
| 1 | MOSI | SPI Master Out Slave In |
| 2 | BCLK | I²S Bit Clock |
| 3 | MISO | SPI Master In Slave Out |
| 4 | LRC | I²S Left/Right Clock (Word Select) |
| 5 | SCLK | SPI Clock |
| 6 | DIN (Microphone) | I²S Data from Microphone |
| 7 | CS | SPI Chip Select |
| 8 | DIN (Speaker) | I²S Data to MAX98357A Amplifier |
| 9 | RESET | TFT Display Reset |
| 10 | Reserved | Not Connected |
| 11 | DC | TFT Display Data/Command |
| 12 | 3.3 V | Logic Power Supply |
| 13 | Reserved | Not Connected |
| 14 | Reserved | Not Connected |
| 15 | GND | Common Ground |
| 16 | 5 V | Power Supply |
