# Bioreactor Dashboard

A dual-page Node-RED dashboard for a bioreactor IoT control system. This repository covers the dashboard side: a companion [repository](https://github.com/ibaadm/Bioreactor-Dashboard) hosts the embedded C++ firmware used to sense and actuate the system.

## Overview

The dashboard consists of three main components:

- **Monitor page** - live time-series charts and gauges for temperature, stirring speed, and pH
- **Control page** - setpoint sliders for each subsystem and per-subsystem kill switches (pumps, heating, motor)
- **Data logging** - incoming telemetry is formatted and appended to a CSV file for later analysis

The dashboard achieves closed-loop control with target accuracies of ±1°C (25-35°C), ±10 RPM (100-1200 RPM), and ±0.2 pH (pH 3-7).

## MQTT Topics

| Topic | Direction | Purpose |
| --- | --- | --- |
| `bioreactor/telemetry` | In | Sensor readings (temperature, RPM, pH) from the ESP32 |
| `bioreactor/control/setpoints` | Out/In | Setpoint values from the dashboard sliders |
| `bioreactor/control/kill` | Out/In | Kill switch states for pumps, heating, and motor |

## Setup

Node.js and Node-RED must be installed on the user's system.
An MQTT connection (e.g. to a HiveMQ broker) must be set up to send and receive messages.

1. Start Node-RED from cmd prompt using the command "node-red"
2. Open the Node-RED editor (usually at http://localhost:1880)
3. Go to Menu (three lines) -> Manage Palette and install the @flowfuse/node-red-dashboard module
4. Go to Menu -> Import and paste or upload the flows.json code from this repository
5. Configure the MQTT broker connection with your own credentials
6. The dashboard itself can be viewed at http://localhost:1880/dashboard
