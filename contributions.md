**Note:** All tasks, achievements, logs, and examples provided in this portfolio represent my individual work and personal contributions only. No other team member’s input or work is included or referenced here.

# Portfolio Introduction: Lead Node-RED Engineer and Unity engineer

# Individual Contribution Tracking
## Individual Contribution Log

**Week 1: Monday, October 27, 2025 -- Friday, October 31, 2025**

**Tasks:**
* Explored and documented the requirements for MES and OEE data integration for Machine 401.
* *Identified Error Variables from SIF 401 PLC* : Held initial meetings about which error variables were available in the SIF 401 PLC. Established the working environment in Node-RED for communications, both simulation and live PLC reads.
* *Document Workflow and Architecture* (#37): Created rough system diagrams showing connection between PLC, Node-RED, and InfluxDB. Drafted a workflow document for the project repository.

**Challenges:**
* Understanding PLC data models and OPC UA address mapping.
* Matching PLC and MES variable types for smooth integration.

**Solutions and Learnings:**
* Consulted SMC_HMI_API.pdf for OPC UA type definitions.
* Discovered that repeatedly testing on real PLC hardware was inefficient, so shifted some testing to simulation with extracted variable lists.

![Plc variables through Prosys](images/WhatsApp%20Image%202025-11-09%20at%2022.08.57_1e8f6908.jpg)
*Plc variables through Prosys*

![First flow/plan discussed](images/WhatsApp%20Image%202025-11-02%20at%2016.50.29_07d0ba95.jpg)
*First flow/plan discussed*

**Week 2: Tuesday, November 4, 2025 -- Saturday, November 8, 2025**

**Tasks:**
* *Build Node-RED Flow to Expose the Variable* (#21): Constructed first working Node-RED flow to inject, read, and debug OPC UA values for AlarmState, AlarmCode, running_time, and related tags.
* Developed custom function nodes to format OPC UA output for payload normalization.
* Designed an HTTP endpoint with function nodes to expose latest variables as JSON for HMI/API.
* Created placeholder images and annotated screenshots for all flow setups.
* *Exploratory SMC Inventory Variable Acquisition*: Dedicated time to investigate and experiment with SMC OPC UA variables linked to inventory data. Developed prototype Node-RED flows to access and visualize live inventory counts from the PLC, mainly as part of an initial exploration effort. 
* Documented findings regarding available fields, data types, and the stability of connection approaches, laying groundwork for future inventory-related integration tasks.

**Challenges:**
* Node-RED OPC UA node sometimes disconnects server.
* fetching failed nodered writes (undefined errors).

**Solutions and Learnings:**
* Standardized all function outputs to single-object payload format per InfluxDB node requirements.
* Used debug nodes at every stage to trace message shapes.
* Stored system architecture and image placeholders for reference.

![intial node-red work](images/Intial%20prposed%20node-red%20work.png)
*intial node-red work*

![Prototype Node-RED flow for exploratory SMC inventory variable acquisition.](images/Screenshot%20PPF.png)
*Prototype Node-RED flow for exploratory SMC inventory variable acquisition.*

---

**Week 3: Monday, November 10, 2025 -- Thursday, November 13, 2025**

**Tasks:**
* *Setup and Configure InfluxDB* (#50): Installed InfluxDB 2.0, created org, token, and buckets. Configured Node-RED server settings for XRBucket.
* Updated all Node-RED Measurement, Organization, and Token fields to ensure reliable connectivity.
* Implemented and tested Flux queries in Data Explorer to retrieve AlarmCode and running_time.
* Created and tested rolling queries for last 30 days, working with aggregateWindow and last().
* Regularly updated logs and documentation with each new flow or fix.

**Challenges:**
* Token masking and credentials persistence in Node-RED.
* Timeout/network errors between Node-RED and InfluxDB.

**Solutions and Learnings:**
* Verified InfluxDB health endpoint and container network mappings.
* Adjusted credentialSecret in Node-RED settings for persistent tokens.
* Learned to map and filter InfluxDB fields to ensure queries use numeric data, avoiding unsupported string aggregates.

![after DB installation](images/WhatsApp%20Image%202025-11-09%20at%2022.45.52_5e318bb4.jpg)
*after DB installation*

![Data visualized in node red](images/Data%20Visualization%20with%20the%20format.png)
*Data visualized in node red*

![Testing DB to check if data flows](images/Testing.png)
*Testing DB to check if data flows*

---

**Week 4: Sunday, November 16, 2025 -- Friday, November 21, 2025**

**Tasks:**
* *Extend Node-RED Logic* (#41): Refined the flow to split XR state and timer categories, dynamically route data to appropriate buckets, and expose API for mitigation feedback.
* *Enabled Unity Integration via Node-RED HTTP Publishing*:
    * Implemented Node-RED flows to publish XR state and inventory data through HTTP endpoints.
    * Designed the endpoints so Unity and other machines could access real-time project data via network queries.
    * Allowed remote systems to retrieve specific machine status, error codes, or inventory values based on their query parameters.
    * Collaborated with the Unity team to verify that their clients could successfully connect and fetch needed data.
    * Established a reliable framework for cross-platform, real-time integration and visualization within the project.
* Finalized documentation, prepared all screenshots and images for inclusion in project report.
* Set up regular data pulls via GET /machine/latest.
* *Podcast research paper selection* : paper that we will discuss for the podacast had been researched and selected after various selections.

**Challenges:**
* Ensuring API endpoints were robust and matched Unity’s requirements.
* Harmonizing tags, fields, and measurements across systems for final data visualization.

**Solutions and Learnings:**
* Iteratively improved function node filtering and output, tested full API responses in both browser and Unity.
* Created a detailed project log with image placeholders for every stage: logic extension, API setup, server configuration, Data Explorer queries, Unity integration.

![query used to send data to unity](images/Query%20to%20fetch%20Data%20to%20publish.png)
*query used to send data to unity*

![Data Visualized on XR machine](images/Data%20visualized%20on%20XR%20device.jpg)
*Data Visualized on XR machine*

---

![Data which was sent to machine](images/Screenshot%202025-11-21%20191236.png)
*Data which was sent to machine*

---

---

### Week 5: Sunday, December 1, 2025 – Saturday, December 14, 2025

**Tasks:**

* **Extension of Node-RED Data Logic:** Extended the existing Node-RED data acquisition and processing logic to include additional real-time machine variables required for XR visualization and monitoring. Newly integrated variables included:
    * AirFlow
    * Current
    * Voltage
    * Power
    * Power Factor
    * BusyTime

* Designed and implemented additional OPC UA read nodes and function nodes to normalize these variables into a consistent JSON structure suitable for both InfluxDB storage and Unity consumption.

* Updated InfluxDB write logic to ensure that each newly added variable was stored with correct measurements, fields, timestamps, and machine identifiers, preserving compatibility with existing queries.

* Extended existing HTTP API endpoints to expose the newly added variables, ensuring that Unity could retrieve a complete snapshot of the machine’s live operational state through a single request.

* **Unity Live Data Integration (Individual Responsibility):** Began working on the Unity side of the project, where I was solely responsible for the live data integration component.
    * Implemented HTTP-based data fetching from Node-RED endpoints.
    * Parsed incoming JSON payloads inside Unity.
    * Verified correct mapping between backend variables and XR UI elements.

* Conducted repeated end-to-end tests to validate that real-time changes in PLC values were correctly reflected in Unity without data loss or mismatch.

**Challenges:**

* Managing the increasing complexity of Node-RED flows as more variables were added.
* Ensuring consistent naming conventions and data types across PLC, Node-RED, InfluxDB, and Unity.
* Handling occasional zero, null, or delayed values from OPC UA reads, which could affect Unity visual stability.

**Solutions and Learnings:**

* Refactored Node-RED function nodes to centralize variable formatting logic, reducing duplication and improving maintainability.
* Introduced validation checks and default fallback values before publishing data to Unity.
* Gained a deeper understanding of real-time system integration, particularly the importance of predictable payload structures when working with XR frontends.

**Figures:**

![Extended Node-RED flow showing additional machine variables](images/Screenshot%202025-12-19%20110920.png)
*Extended Node-RED flow showing additional machine variables*

---

**Raw JSON Data Stream**
```json
{
  "AirFlow": {
    "name": "AirFlow",
    "time": "2026-01-12T15:18:04Z",
    "value": 0,
    "machine": "401"
  },
  "BusyTime": {
    "name": "BusyTime",
    "time": "2026-01-12T15:17:52Z",
    "value": 0,
    "machine": "401"
  },
  "Current": {
    "name": "Current",
    "time": "2026-01-12T15:17:57Z",
    "value": 0.20000000298023224,
    "machine": "401"
  },
  "Power": {
    "name": "Power",
    "time": "2026-01-12T15:18:01Z",
    "value": 26,
    "machine": "401"
  },
  "PowerFactor": {
    "name": "PowerFactor",
    "time": "2026-01-12T15:18:02Z",
    "value": 0.550000011920929,
    "machine": "401"
  },
  "Voltage": {
    "name": "Voltage",
    "time": "2026-01-12T15:17:55Z",
    "value": 232.8000030517578,
    "machine": "401"
  },
  "bCycle": {
    "name": "bCycle",
    "time": "2026-01-12T15:17:49Z",
    "value": 0,
    "machine": "401"
  }
}
**Final Json for Live Data.**

![Unity inspector view showing live data bindings](images/liveDataBindings.png)
*Unity inspector view showing live data bindings*

---

### Week 6: Tuesday, January 7, 2026 – Monday, January 13, 2026

**Tasks:**

* **Full System Integration:** Integrated all three major project components developed by the team:
    * PLC and OPC UA data acquisition
    * Node-RED data processing, storage, and API publishing
    * Unity-based XR visualization

* Made necessary changes across Node-RED flows, API endpoints, and Unity scripts to resolve compatibility issues discovered during integration testing.

* Optimized data polling intervals and request handling to ensure stable real-time performance during live demonstrations.

* Verified that all error states, machine status indicators, and live numerical values were displayed correctly and updated reliably in XR.

* **Live Demo Preparation:**
    * Prepared the system for a complete end-to-end live demonstration.
    * Tested system behavior under different machine states and simulated error conditions.
    * Ensured fallback behavior in case of temporary data unavailability.

* **Presentation Preparation:**
    * Contributed to the final project presentation by providing architecture explanations, data flow diagrams, and live demo support.
    * Assisted in structuring the narrative to clearly explain how Node-RED, InfluxDB, and Unity interacted as a unified XR system.

**Challenges:**

* Coordinating changes across multiple subsystems under time constraints.
* Debugging issues that only appeared during full system execution rather than in isolated components.
* Ensuring system stability and responsiveness suitable for a live demonstration environment.

**Solutions and Learnings:**

* Adopted a systematic integration testing approach, validating one data path at a time before enabling the full pipeline.
* Improved logging and debugging practices in both Node-RED and Unity to quickly identify integration-level issues.
* Learned the importance of final-stage integration ownership and thorough testing when delivering a real-time XR system.

**Figures:**

![Final integrated system architecture overview](images/Gemini_Generated_Image_lzm6xrlzm6xrlzm6.png)
*Final integrated system architecture overview*

![Unity XR view during live demo](images/live%20demo.png)
*Unity XR view during live demo*

![Screenshot from Live data I personally wored on before integration](images/prelim.jpeg)
*Screenshot from Live data I personally wored on before integration*

---
