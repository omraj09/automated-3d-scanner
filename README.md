# Development of an Automated 3D Scanning System

[cite_start]An open-source, cost-effective, and fully automated 3D scanning platform built through the integration of mechanical design, embedded electronics, and full-stack software development[cite: 50, 571]. [cite_start]By synchronizing a single high-resolution 16MP optical sensor with dual-axis stepper motor motion, this system completely eliminates the need for complex multi-sensor configurations (such as infrared or LiDAR arrays) to produce accurate, consistent 3D models suitable for reverse engineering, automation, and digital archiving[cite: 53, 58].

---

## 🚀 Key Features

* [cite_start]**Complete Automation:** Eliminates manual scanning entirely by automating object rotation, camera positioning, and image capture into a single seamless workflow[cite: 100, 117, 127].
* [cite_start]**Single-Sensor Photogrammetry:** Leverages a 16-megapixel Arducam IMX519 camera module with programmable autofocus, bypassing expensive or bulky multi-sensor hardware arrays[cite: 53, 76].
* [cite_start]**Custom Pi Shield PCB:** Centralizes power distribution, voltage regulation, and motor control onto a single board, removing fragile breadboard connections and maximizing electrical signal integrity[cite: 52, 475, 476, 534].
* [cite_start]**Remote Web Interface:** A custom dashboard facilitating remote operation, real-time system status monitoring, manual hardware overrides, and full parameter tuning (shutter speed, motor angles, focus stacks, and cropping metrics)[cite: 56, 79, 80, 604, 605, 607].
* [cite_start]**Cloud Infrastructure Integration:** Dedicated cloud-based file management allows secure storage, remote accessibility, project organization, and streamlined handling of large image datasets[cite: 57, 587, 617, 618].
* [cite_start]**True-to-Life Scaling Calibration:** A corrective global scaling workflow is permanently integrated into post-processing to fix depth discrepancies and maintain absolute physical fidelity[cite: 689, 690].
* [cite_start]**Dual Operational Modes:** The scanner can be easily switched from fully automated mode to manual override mode whenever specific edge cases require manual manipulation[cite: 118].

---

## 🛠️ System Hardware & Specifications

[cite_start]The hardware architecture uses a Raspberry Pi 4B as a central processing unit to bridge user dashboard inputs directly to low-level mechanical actuation registers via a custom interface board[cite: 234, 235, 237, 391].

### Hardware Component Configurations

| Component | Specification / Model | Role in System |
| :--- | :--- | :--- |
| **Central Controller** | [cite_start]Raspberry Pi 4 Model B [cite: 74] | [cite_start]Main processing unit; coordinates peripheral devices, executes control logic, handles data flow, and hosts the web interface backend[cite: 148, 578, 643]. |
| **Optical Sensor** | [cite_start]Arducam IMX519 (16MP Sony CMOS) [cite: 76, 424, 432] | [cite_start]Connects natively via the MIPI CSI protocol; captures high-resolution surface details with automated focus tracking[cite: 54, 76, 439, 440]. |
| **Turntable Actuator** | [cite_start]NEMA 17 Stepper Motor (13 Ncm torque) [cite: 377, 380] | [cite_start]Rotates the object platform smoothly in predefined, precise angular step increments across a full 360° space[cite: 238, 380]. |
| **Rotor/Arm Actuator** | [cite_start]NEMA 17 Stepper Motor (40 Ncm torque) [cite: 377, 383] | [cite_start]High-torque motor managing the height, framing, and tilt orientation of the camera subsystem along the structural arm[cite: 240, 384]. |
| **Motor Drivers** | [cite_start]Dual A4988 Modules [cite: 417, 505] | [cite_start]Mounted to the Pi Shield; translates low-power GPIO signals from the Pi into clean current/voltage steps for the motors[cite: 387, 388]. |
| **Power Solution** | [cite_start]Custom Pi Shield PCB & Buck Converter [cite: 52, 530] | [cite_start]Regulates a single external 12V DC input down to stable operational voltage levels for the Pi, protection circuitry, and drivers[cite: 478, 531]. |
| **Illumination Hub** | [cite_start]Synchronized PWM LED Ring/Strip Light [cite: 146, 533] | [cite_start]Regulated via switching components on the shield to deliver uniform, shadowless lighting to optimize texture clarity[cite: 146, 455, 458]. |

---

## 💻 Software Architecture & Workflow

[cite_start]The system software workflow relies on an unmanaged backend runtime script communicating directly with hardware peripherals, paired alongside a responsive full-stack web frontend[cite: 50, 56, 590].

### Step-by-Step Functional Lifecycle:
1. [cite_start]**System Initialization:** Powering up triggers the Raspberry Pi to initialize core software libraries, load camera subsystem modules, and spin up communication layers[cite: 332, 333].
2. [cite_start]**Calibration:** Both NEMA 17 stepper motors self-calibrate back to internal home references while the camera exposure parameters settle matching the internal ambient context[cite: 335, 336].
3. [cite_start]**Object Placement & Configuration:** The scanning target is placed on the turntable platform[cite: 338]. [cite_start]The operator utilizes the web application interface to define parameters like image resolution, rotation step angles, and focus capture options[cite: 340].
4. **Synchronized Ingestion Loop:** The execution automated scripts sequentially iterate:
   * [cite_start]The turntable increments to the current index step angle[cite: 341].
   * [cite_start]The system fires the lighting control hub to achieve uniform texture exposures[cite: 457, 520].
   * [cite_start]The Arducam IMX519 executes a uncompressed frame transfer down the low-latency CSI pipeline[cite: 54, 442, 443].
   * [cite_start]The rotor adjustments shift vertical heights dynamically to completely resolve compound dimensional curves[cite: 240, 342].
5. [cite_start]**Reconstruction & Scaling Calibration:** Categorized datasets save securely locally onto the microSD card before uploading to integrated cloud endpoints[cite: 244, 398]. [cite_start]The model compiles via photogrammetry steps into an optimized `.obj` file[cite: 346, 347]. [cite_start]A permanent global scalar calculation applies an inverse factor to reverse depth anomalies, guaranteeing true-to-life dimensional accuracy[cite: 689, 690].

---
👥 Contributors & Credits
Developed in partial fulfillment of the requirements for the award of the degree of Bachelor of Engineering in Mechatronics Engineering under Visvesvaraya Technological University (Jnanasangama, Belagavi) at Acharya Institute of Technology.  
Project Development Team: Anurag Kumar, Kedar Topajiche, Omraj Sawant
