# Power Management

The system is powered by **four 18650 batteries**, consisting of **two parallel cell groups connected in series**, creating a **2S2P lithium-ion battery pack**.

By connecting **two batteries in parallel**, the battery capacity is doubled, increasing the overall runtime of the robot.

By connecting the **two parallel cell groups in series**, the maximum output voltage is doubled from **4.2 V** (a single Li-ion cell) to **8.4 V**, which is the recommended operating voltage for the **WP5335 servos** used in the robot's legs.

Following this, the batteries connect directly to a **HX-2S-01 Battery Management System (BMS)**, which protects the robot from:

- Short circuits
- Overcharge
- Over-discharge
- Over-current

Moreover, a **4 A fuse** and an **SPDT power switch** are connected to the battery output to safely turn the robot **ON/OFF** , ensuring that any short circuit cannot cause damage to the electronics.

