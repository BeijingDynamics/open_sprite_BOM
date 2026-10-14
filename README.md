# Open Sprite Hardware Documentation

Open Sprite provides two compute configurations built around the same 31-motor humanoid platform. This repository contains four interactive HTML documents covering the control architecture, motor placement, CAN FD allocation and bill of materials.

## Live website

[Open the interactive Open Sprite BOM and hardware documentation →](https://beijingdynamics.github.io/open_sprite_BOM/)

## Open the documents

Open any HTML file locally in a browser. The pages are static and require no build step. Manufacturer links require an internet connection.

| File | Description |
| --- | --- |
| [`spacemit-k3.html`](spacemit-k3.html) | SpacemiT K3-COM260 compute platform, four CAN FD buses, motor register and hardware details. |
| [`nvidia-jetson.html`](nvidia-jetson.html) | NVIDIA Jetson Orin Nano Super Developer Kit, Kunhong four-channel USB-to-CAN FD EVK, motor register and hardware details. |
| [`motor-location-map.html`](motor-location-map.html) | Front-view motor placement guide. The robot faces the viewer, so the robot's right side appears on the viewer's left. |
| [`index.html`](index.html) | Combined BOM with separate SpacemiT K3-COM260 and NVIDIA Jetson quantities and costs, plus motor CAN_ID and Master_ID assignments. |

All four pages link to one another. Keep the [`assets`](assets) directory beside the HTML files so photographs and switch diagrams remain available.

## Hardware layout

Both compute configurations use the same motors, physical layout and address allocation:

| Bus | Motor group |
| --- | --- |
| CANFD1 | Waist and left leg |
| CANFD2 | Head pitch/roll motor pair and right leg |
| CANFD3 | Head yaw and left arm |
| CANFD4 | Right arm |

Motor names follow the robot URDF. `head_yaw_joint` directly drives head yaw, while `head_motor_1` and `head_motor_2` form a coupled drive for head pitch and roll. Each ankle uses two DM-J4310P-2EC motors with ball-joint connecting rods and a universal-joint linkage to produce ankle pitch and roll.

CAN_ID and Master_ID values use hexadecimal notation (`0xNN`). The last motor on each leg bus uses an external 120 Ω resistor across CAN_H and CAN_L. DM-J3507-2EC motors use the documented internal 120 Ω switch settings shown in the motor detail panels.

## Compute, sensing and power

- **SpacemiT configuration:** K3-COM260 Kit with 8GB LPDDR5 and 128GB UFS; Morningsun VCF4824EBO-120WFR3-N, 36–75V input, 24V/5A output, 120W.
- **NVIDIA configuration:** Jetson Orin Nano Super Developer Kit; Kunhong KH-UCANFD-B2B-X4-EVK; Morningsun VCB4812SBO-100WR3, 36–75V input, 12V/8.333A output, 100W.
- **Shared sensing:** ICM-45686 six-axis IMU module connected through USB Type-C.
- **Shared battery system:** two Dong Cheng FFBL2040 batteries, each 18V nominal (20V MAX), 4.0Ah, with two XT60E-F battery holders.
- **Circuit protection:** CHINT CB-60A, 1P, 40A circuit breaker.

The final battery capacity and battery interconnection remain subject to system testing. The communication diagrams describe topology and device allocation; they are not pin-level power-wiring drawings.

## Using the pages

- Select a motor, CANFD port or hardware block to open its detail panel.
- Use search and bus filters to narrow the motor register.
- Select a motor in the location map to identify its approximate physical position and open it in either compute configuration.
- Use the BOM filters and motor links to inspect the corresponding nodes.
- Use the browser print command or **Print / PDF** to create a printable copy.
- The compute pages support local motor-data editing and HTML/JSON export. Save an exported file before refreshing the browser.

All displayed prices are in USD. The BOM total includes the motor set and every currently priced item. `N/A` means that a component is not used in that configuration.

## Repository files

The interactive release requires these files to remain together:

```text
.
├── README.md
├── spacemit-k3.html
├── nvidia-jetson.html
├── motor-location-map.html
├── index.html
└── assets/
    ├── kunhong-4-channel-evk.png
    ├── dm-j3507-switch-direction.png
    ├── dm-j3507-120r-off.jpg
    └── dm-j3507-120r-on.jpg
```
