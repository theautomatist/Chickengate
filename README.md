# Chickengate Controller

Controller that opens or closes a chicken coop gate. It uses Node-RED as the brain and MQTT for communication. The gate opens and closes based on sunrise/sunset. You can set time windows for opening and closing; if sunrise or sunset falls outside the window, the window times are used instead. [You can adjust the sun time events](https://github.com/rdmtc/node-red-contrib-sun-position/wiki/Base-Functions#sun-times).

## Overview
- ESP32-based gate controller with a linear actuator and encoder feedback.
- Node-RED handles scheduling and publishes MQTT commands.
- Node-RED dashboard for manual open/close control.

![Controller overview](https://user-images.githubusercontent.com/87583841/177513696-c317f795-c482-4f3a-914d-01099f40bae9.png)
Controller overview with the gate hardware.

## Schedule behavior
Example settings:
- open from: 6:00 AM
- open until: 8:00 AM
- close from: 5:30 PM
- close until: 7:30 PM

Example cases:
- Sunrise @ 5:40 AM, gate opens @ 6:00 AM
- Sunrise @ 7:20 AM, gate opens @ 7:20 AM
- Sunrise @ 8:10 AM, gate opens @ 8:00 AM

## Main components
- Linear actuator with integrated rotary encoder
- ESP32 Matrix Core + WiFi antenna
- VNH3ASP30-E full-bridge motor driver
- DC-DC stepdown
- Waterproof connectors (TE Connectivity AMP Superseal 1.5)
- 3D-printed sealed housing

## Build photos
![Controller electronics and enclosure](./img/IMG_20220623_113807.png)
Components
![Gate and actuator installation](./img/IMG_20220120_204701.jpg)
Assembled controller electronics and enclosure.
![](./img/IMG_20220205_131544.jpg)
Gate and actuator installation in the coop.


## Wiring and hardware notes
![Wiring overview](https://user-images.githubusercontent.com/87583841/177510831-5efa2f2f-81bf-4123-974b-35eee85741f6.png)
Wiring overview for the motor driver, power, and sensors. Current-sense output of the motor driver is filtered with a low-pass.

## Node-RED dashboard
![Node-RED dashboard](https://user-images.githubusercontent.com/87583841/177512667-4377206e-3c97-492d-b42d-e400036e0bc6.PNG)
Node-RED dashboard used for manual control and status display.

## Node-RED and MQTT
![Node-RED flow](img/node-red-flow.png)
Node-RED flow that schedules open/close actions and publishes MQTT commands.

### Required Node-RED nodes
- [node-red-contrib-sun-position](https://flows.nodered.org/node/node-red-contrib-sun-position)
- [node-red-dashboard](https://flows.nodered.org/node/node-red-dashboard)
- [node-red-contrib-ui-led](https://flows.nodered.org/node/node-red-contrib-ui-led)

### Example configs
- `src/Example Docker Compose.yml`
- `src/Example MQTT Config`
- `src/Node Red Flow.json`
