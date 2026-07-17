# Camera Ring Light

<p align="center">
  <img src="https://raw.githubusercontent.com/thkaratsis/Mitsos----An-Open-Source-AI-Humanoid-Robot/main/schemes/Camera%20RingLight/CameraRinglight.png" alt="Camera Ring Light Schematic" width="900">
</p>

```mermaid
flowchart LR
    HB["Head Board"]
    RL["Camera Ring Light PCB"]
    CAM["IMX219 Camera"]

    HB -->|5 V / GND| RL
    RL -->|Illumination| CAM
```

The **Camera Ring Light PCB** is mounted on the robot's head and provides controlled illumination for the **IMX219 camera module**. It is a physical board assembled outside the head and powered directly from the **2-pin connector on the head board**. By supplying constant lighting around the camera based on the environment, the ring light improves image quality and helps the vision system perform more reliably in darker area.


## Purpose

The ring light helps the robot:

- maintain consistent camera exposure,
- reduce shadows around the face and head,
- improve object detection performance,
- support embedded vision and inverse kinematics tasks.


## Electrical Connection

| Signal | Purpose |
|---|---|
| 5 V | Power supply for the ring light |
| GND | Common ground |


## Design Notes

The ring light is intentionally simple:
- it is mounted on the head assembly,
- it receives power from the head board,
- it does not require separate data lines,
- it is controlled as a passive illumination module.

