# Open Sprite Hardware Documentation

Open Sprite has two compute configurations that share the same 31-motor humanoid layout. This directory contains four interactive HTML documents for the first public hardware-documentation release.

## Open the documents

The current publication files are served directly from the repository root. Open the [published BOM site](https://beijingdynamics.github.io/open_sprite_BOM/) or any HTML file locally in a browser. No build step or local server is required for the core pages. Links to manufacturer websites require an internet connection.

| File | What it shows |
| --- | --- |
| [`spacemit-k3.html`](spacemit-k3.html) | SpacemiT K3 compute platform, four CAN FD buses, motor register and component details. |
| [`nvidia-jetson.html`](nvidia-jetson.html) | NVIDIA Jetson Orin Nano Super Developer Kit, Kunhong four-channel USB-to-CAN FD EVK, motor register and component details. |
| [`motor-location-map.html`](motor-location-map.html) | Front view of approximate motor placement. The robot faces the viewer, so its right side appears on the viewer's left. |
| [`index.html`](index.html) | Combined bill of materials with separate SpacemiT K3 and NVIDIA Jetson quantity and cost columns, plus motor CAN_ID and Master_ID assignments. |

The NVIDIA page displays a local EVK photograph. Keep [`assets/kunhong-4-channel-evk.png`](assets/kunhong-4-channel-evk.png) at that relative path when copying the HTML files. All four pages link to one another.

## Hardware layout

Both configurations use the same physical motors and address allocation. CANFD1 serves the waist and left leg; CANFD2 serves the head pitch/roll motor pair and right leg; CANFD3 serves head yaw and the left arm; CANFD4 serves the right arm. Motor names follow the robot's URDF naming where a physical motor directly represents a joint.

`head_yaw_joint` drives head yaw directly. `head_motor_1` and `head_motor_2` work together through the head linkage to produce head pitch and roll. Each ankle likewise uses two 4310P motors with ball-joint connecting rods and a universal-joint linkage to produce ankle pitch and roll. A motor in either paired drive does not correspond to just one output axis.

Both configurations include a Morningsun VCF4824EBO-120WFR3-N DC/DC converter: nominal 42 V to 24 V, 120 W, with a 36–75 V input range and a 24 V, 5 A output. Battery, fuse, emergency stop, main switch and related power components are reserved in the BOM. Detailed power distribution, connector pinouts, CAN FD bit rates, BRS and termination settings remain to be specified.

## Using the pages

- Select a motor, CANFD port or hardware block in either compute page to open its details. Search and bus filters narrow the motor register.
- Select a motor in the location map to see its approximate physical position and open that motor in either compute configuration.
- Filter the BOM or use its motor links to inspect the corresponding node in a compute page. All displayed prices are in USD; `TBD` indicates an unpriced or unspecified item.
- The compute pages allow local motor-data edits and HTML/JSON export. Save an edited HTML file before refreshing the browser. The four pages are separate documents: editing one page does not update the others automatically.
- Use the browser's print command or the page's **Print / PDF** control to save a printable copy.

The location map is an illustrative front-view guide, without wiring or exact mechanical dimensions. The compute diagrams describe communication topology; they are not complete power-wiring or connector drawings.

## Files for the first GitHub release

The initial interactive release needs the four HTML files above and the EVK image, with the `assets/` path preserved.
