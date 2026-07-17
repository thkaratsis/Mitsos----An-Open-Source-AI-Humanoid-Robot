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


> **💡 Sensor Integration**
>
> The **LSM6DS3** is connected to the **ESP32-S3** through the **I²C bus**. The ESP32 continuously gathers acceleration and gyroscope measurements, processes the raw sensor data, and transmits orientation and motion information to the **Raspberry Pi 5** via the **UART** interface. This allows the ESP32 to perform  real-time sensor acquisition while the Raspberry Pi focuses on high-level control
