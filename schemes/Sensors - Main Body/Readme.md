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

---

> **Address Configuration**
>
> All **VL53L0X** sensors share the same default **I²C address (0x29)**. Since multiple sensors are connected to the same I²C bus, each sensor's **XSHUT** pin is connected to a dedicated GPIO pin on the **ESP32-S3**.
>
> During system startup, the ESP32 keeps all sensors in hardware shutdown. It then enables them **one at a time**, assigns each sensor a unique I²C address through software, and finally activates the next sensor. This initialization process allows all five VL53L0X sensors to operate simultaneously on the same I²C bus without address conflicts.
