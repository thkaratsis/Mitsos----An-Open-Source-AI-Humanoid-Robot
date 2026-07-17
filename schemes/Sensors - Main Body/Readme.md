# Sensors- Main Body

<p align="center">
  <img src="https://raw.githubusercontent.com/thkaratsis/Mitsos----An-Open-Source-AI-Humanoid-Robot/main/schemes/Sensors - Main Body/Sheet_3.png" alt="" width="900">
</p>


In order to make the robot oporate a variety of sensors are used to ensure it has every safety measure

To begin with, there are a total of 5x1 male headers to which 5 vl53l0x TOF sensors connect each at a different posistion
1) On top of the Head, that works like a lidar duo to having 2 mg90s serovs that allow it to move freelly
2) at the back of the robot giving feedback abotu the backwards distance
3) at the front that looks down at a 30 degree angle
4) at the front looking right at a 30 degree angle
5) at the fron looking left at a 30 degree angle

These sensor help the robot navigate places and not crash into walls 

## VL53l0X

| Specification | Value |
|---|---|
| Measuring Range |  3 cm to 2 m |
| Measurement Accuracy | ± 3% to ± 5% |
| Resolution | 1mm |
| Interface | I²C |
| Field of View (FOV) | 25° to 35° |
