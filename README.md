# dual-wavelength-ppg-system
Design and Implementation of a Dual-Wavelength Photoplethysmographic System for Real Time Estimation of Arterial Stiffness, Oxygen Saturation, and Heart Rate Variability using  Arduino and MATLAB 
# Dual-Wavelength Photoplethysmographic System for Real-Time Physiological Parameter Estimation

A low-cost, portable biomedical instrumentation system that acquires dual-wavelength optical PPG signals using the MAX30102 sensor and Arduino Uno to estimate Heart Rate (HR), Oxygen Saturation ($SpO_2$), Heart Rate Variability (HRV), and Arterial Stiffness in real time via MATLAB[cite: 1].

---

## 📌 Project Overview

Cardiovascular diseases (CVDs) remain a leading cause of global mortality[cite: 1]. Early detection of cardiovascular risk factors—such as increased arterial stiffness, reduced arterial oxygen saturation, and autonomic nervous system dysfunction—is crucial for timely intervention[cite: 1]. 

This project integrates multi-parameter estimation into a single, portable platform featuring real-time MATLAB processing, live signal visualization, and automated data logging[cite: 1].

---

## ✨ Key Features

- **Dual-Wavelength Optical Acquisition:** Captures Red (~660 nm) and Infrared (~940 nm) PPG signals using the MAX30102 sensor[cite: 1].
- **Auto-Configuration Firmware:** Dynamic brightness adjustment to prevent ADC saturation and adapt to different tissue perfusion levels[cite: 1].
- **Real-Time Signal Conditioning:** Implements a 3rd-order Butterworth bandpass filter (0.5–10 Hz) in MATLAB to eliminate baseline wander and high-frequency noise while preserving waveform morphology[cite: 1].
- **Multi-Parameter Estimation:**
  - **Heart Rate (HR):** Adaptive peak detection on the filtered IR channel[cite: 1].
  - **Oxygen Saturation ($SpO_2$):** AC/DC ratio-of-ratios ($R$) calculation with empirical calibration ($SpO_2 = 108 - 21R$)[cite: 1].
  - **Time-Domain HRV:** Computes $SDNN$, $RMSSD$, and $pNN50$ over a 60-second rolling window[cite: 1].
  - **Arterial Stiffness Analysis:** Evaluates the Second Derivative PPG (SDPPG) using Savitzky-Golay filtering to identify $b$ and $d$ inflection points for Stiffness Index (SI) and Reflection Index (RI) calculations[cite: 1].
- **Live GUI & Data Logging:** Real-time plotting of PPG waveforms, tachograms, HRV trends, SDPPG markers, and automatic CSV logging[cite: 1].

---

## 📐 System Architecture
+-------------------+        I2C (400kHz)       +-------------------+
|  MAX30102 Sensor  | ------------------------> |    Arduino Uno    |
|   (Red + IR LED)  |                           |   (ATmega328P)    |
+-------------------+                           +-------------------+
|
Serial (115200 Baud)
v
+-------------------+
| MATLAB Processing |
|  & Real-Time GUI  |
+-------------------+

---

## 🛠️ Hardware Setup & Wiring

| MAX30102 Pin | Arduino Uno Pin | Function / Description |
| :--- | :--- | :--- |
| **VIN** | `3.3V` / `5V` | Power Supply[cite: 1] |
| **GND** | `GND` | Common Ground[cite: 1] |
| **SDA** | `A4` | $I^2C$ Serial Data Line[cite: 1] |
| **SCL** | `A5` | $I^2C$ Serial Clock Line[cite: 1] |

*(Optional 16x2 LCD display pins can be connected to digital pins D2–D5, D11, D12 for standalone pulse display[cite: 1]).*

---

## 📂 Repository Structure

```text
├── Firmware/
│   └── MAX30102_Serial_MATLAB.ino   # Arduino firmware with auto-gain & AC coupling
├── MATLAB/
│   ├── HRV_Monitor_Standalone.m      # Standalone time-domain HRV processing
│   ├── Health_Monitor_MATLAB.m       # Combined HR, SpO2, and HRV live monitor
│   └── SDPPG_Arterial_Stiffness.m    # SDPPG second derivative & stiffness index script
├── Schematics/
│   └── Circuit_Diagram.png           # Hardware connection schematics
├── README.md                         # Project documentation
└── .gitignore                        # Git ignore file for CSV outputs and temporary files
```[cite: 1]

---

## ⚙️ Prerequisites & Installation

### 1. Hardware Requirements
- Arduino Uno R3[cite: 1]
- MAX30102 Pulse Oximeter & Heart-Rate Sensor Module[cite: 1]
- USB Type-A to Type-B Cable[cite: 1]
- Jumper Wires & Breadboard[cite: 1]

### 2. Software Requirements
- **Arduino IDE** (v2.0 or newer)[cite: 1]
- **MATLAB** (R2021a or newer)[cite: 1] with:
  - Signal Processing Toolbox[cite: 1]
  - MATLAB Support Package for Arduino / Serial Port Communication[cite: 1]

---

## 🚀 Running the Project

1. **Upload Microcontroller Firmware:**
   - Connect the Arduino Uno to your computer via USB[cite: 1].
   - Open `Firmware/MAX30102_Serial_MATLAB.ino` in the Arduino IDE[cite: 1].
   - Install the `MAX30105` library via the Library Manager if not already present[cite: 1].
   - Upload the sketch to the Arduino Uno[cite: 1].

2. **Run MATLAB Analysis & Dashboard:**
   - Open MATLAB and set your working directory to the `MATLAB/` folder[cite: 1].
   - Open `Health_Monitor_MATLAB.m` (or `SDPPG_Arterial_Stiffness.m`)[cite: 1].
   - Update the serial port string to match your connected Arduino COM port:
     ```matlab
     s = serialport("COM7", 115200); % Replace COM7 with your active port
     ```[cite: 1]
   - Run the script and place your finger gently on the MAX30102 sensor[cite: 1].

---

## 📊 Experimental Results & Performance

| Parameter | System Value | Reference Device | Mean Absolute Error |
| :--- | :--- | :--- | :--- |
| **Heart Rate (HR)** | 72 – 76 BPM[cite: 1] | 71 – 75 BPM[cite: 1] | **1.81%**[cite: 1] |
| **Oxygen Saturation ($SpO_2$)** | 96.7% – 97.5%[cite: 1] | 97.0% – 98.0%[cite: 1] | **0.54%**[cite: 1] |
| **SDNN (HRV)** | 38.9 – 47.6 ms[cite: 1] | Normal Resting Range[cite: 1] | N/A[cite: 1] |
| **Stiffness Index (SI)** | 6.78 – 7.23 m/s[cite: 1] | Normal Range (< 10 m/s)[cite: 1] | N/A[cite: 1] |

---

## 👥 Authors & Team Members

**Department of Electrical and Electronic Engineering (EEE)**  
**Ahsanullah University of Science and Technology (AUST)**[cite: 1]  
**Course:** EEE 4238 - Biomedical and Instrumentation Lab (Section C)[cite: 1]  

- **Md. Mehedi Hasan Hasib** (ID: 20220105161)[cite: 1]
- **Ramisa Anjum** (ID: 20220105159)[cite: 1]
- **Ramisa Maliat** (ID: 20220105176)[cite: 1]
- **Sayeda Miskatul Ferdous** (ID: 20220105175)[cite: 1]
- **Nur Mohammad Shishir** (ID: 20210105149)[cite: 1]

---

## 📜 References

1. Allen, J. (2007). *Photoplethysmography and its application in clinical physiological measurement.* Physiological Measurement, 28(3), R1–R39[cite: 1].
2. Elgendi, M. (2012). *On the analysis of fingertip photoplethysmogram signals.* Current Cardiology Reviews, 8(1), 14–25[cite: 1].
3. Millasseau, S. C., et al. (2002). *Determination of age-related increases in large artery stiffness by digital pulse contour analysis.* Clinical Science, 103(4), 371–377[cite: 1].
4. Maxim Integrated. (2018). *MAX30102 Datasheet: High-Sensitivity Pulse Oximeter and Heart-Rate Sensor for Wearable Health*[cite: 1].
