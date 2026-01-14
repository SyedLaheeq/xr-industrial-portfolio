---
layout: page
title: Individual Contribution Log
---

# Individual Contribution Tracking

---

## Week 1 (Oct 27 – Oct 31, 2025)

### Tasks
- Identified MES and OEE requirements for Machine 401
- Analyzed SIF 401 PLC variables
- Set up Node-RED for OPC UA communication
- Created early system architecture drafts

### Challenges
- OPC UA address mapping
- PLC–MES data compatibility

### Solutions & Learnings
- Used `SMC_HMI_API.pdf`
- Shifted early testing to simulation

### Evidence
![PLC variables](assets/images/WhatsApp%20Image%202025-11-09%2022.08.57.jpg)

---

## Week 2 (Nov 4 – Nov 8, 2025)

### Tasks
- Built Node-RED flows for AlarmState and AlarmCode
- Created HTTP JSON APIs
- Explored inventory OPC UA variables

### Challenges
- Node-RED OPC UA instability

### Solutions
- Standardized payload formats
- Extensive debug logging

### Evidence
![Node-RED flow](assets/images/Intial%20prposed%20node-red%20work.png)

---

## Week 3 (Nov 10 – Nov 13, 2025)

### Tasks
- Installed and configured InfluxDB 2.0
- Integrated Node-RED with InfluxDB
- Tested Flux queries

### Evidence
![InfluxDB setup](assets/images/WhatsApp%20Image%202025-11-09%2022.45.52.jpg)

---

## Week 4 (Nov 16 – Nov 21, 2025)

### Tasks
- Extended Node-RED logic for XR
- Published real-time APIs for Unity
- Validated XR data visualization

### Evidence
![XR data](assets/images/Data%20visualized%20on%20XR%20device.jpg)

---

## Week 5 (Dec 1 – Dec 14, 2025)

### Tasks
- Added AirFlow, Current, Voltage, Power, PowerFactor, BusyTime
- Extended InfluxDB schema
- **Sole responsibility for Unity live data integration**

### Raw JSON Payload
```json
{
  "AirFlow": { "value": 0 },
  "Current": { "value": 0.2 },
  "Voltage": { "value": 232.8 },
  "Power": { "value": 26 },
  "PowerFactor": { "value": 0.55 },
  "BusyTime": { "value": 0 }
}
