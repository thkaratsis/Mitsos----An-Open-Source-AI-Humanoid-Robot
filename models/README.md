## Model Overview

| Part | Role | Material | File |
|---|---|---|---|
| [ArmFull.stl](./Arms/ArmFull.stl) | Complete arm assembly | PETG / ASA / TPU | Full arm model |
| [BodyFull.stl](./Body/BodyFull.stl) | Complete body assembly | ASA / PETG | Full body model |
| [HeadFull.stl](./Head/HeadFull.stl) | Complete head assembly | ASA / PETG | Full head model |
| [LegFull.stl](./Legs/LegFull.stl) | Complete leg assembly | PETG / ASA / TPU | Full leg model |


## Subfolders

| Folder | Description |
|---|---|
| [Arms](./Arms) | Arm structure, gripper, elbow mechanism, and joint connectors |
| [Body](./Body) | Main torso structure, mounting points, and internal body components |
| [Head](./Head) | Head shell, display mount, face structure, and head mechanism |
| [Legs](./Legs) | Leg structure, foot assembly, knee/ankle mechanism, and support parts |


## Printing Notes

The robot uses different materials depending on the mechanical requirements of each part:

- **ASA** for stronger structural parts and components
- **PETG** for most functional parts due to its balance of strength and printability
- **TPU** for flexible parts such as the foot base, where grip and shock absorption are important

## Assembly Hierarchy

- **Body**: main structural frame of the robot
- **Head**: facial display, camera, microphone, speaker, and head motion
- **Arms**: elbow, gripper, and arm articulation
- **Legs**: support, movement, and foot structure
