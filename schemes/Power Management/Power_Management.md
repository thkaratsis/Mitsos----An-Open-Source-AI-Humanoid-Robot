# Mitsos Current Consumption Analysis

## Overview

Mitsos is powered by a 2S Li-ion battery system.

The electrical system is separated into two main power domains:

1. **Logic Power**
   - Raspberry Pi 5
   - ESP32 controller
   - Sensors
   - TFT display
   - Audio system

2. **Motor Power**
   - PCA9685 servo controllers
   - Servo motors

This separation prevents voltage drops and electrical noise from affecting the computational systems during servo movement.

---

# Battery System

## Battery Configuration

| Parameter | Value |
|-|-|
| Battery type | 2S Li-ion |
| Nominal Voltage | 7.4V |
| Maximum Voltage | 8.4V |
| Minimum Voltage | ~6.0V |

The battery output is protected by:

- HX-2S-01 BMS
- Fuse protection
- Main power switch

---

# Logic Power Consumption

## Raspberry Pi 5

The Raspberry Pi 5 is the main computer of Mitsos.

Responsibilities:

- Artificial intelligence inference
- Computer vision
- Camera processing
- TFT face rendering
- Robot decision making
- Communication with ESP32


| Operating Condition | Current |
|-|-|
| Idle | ~0.7A - 1A |
| Normal operation | ~1.5A - 2.5A |
| Heavy AI workload | ~3A - 5A |

Estimated power:
