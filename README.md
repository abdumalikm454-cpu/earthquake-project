# Argos System 2026: AI-Powered Multi-Sensor Fusion System for Post-Earthquake Human Detection

An integrated hardware and software platform designed to locate human survivors trapped beneath structural rubble during the critical post-earthquake "golden hours". Developed for the **National University Journal of Robotics and Artificial Intelligence (NURAI)**.

## Overview
Traditional search-and-rescue tools (such as standalone thermal cameras or acoustic sensors) often suffer from concrete signal blockage, environmental clutter, and false alarms. **Argos System 2026** solves this by fusing multi-modal biological and environmental data—non-contact thermal signatures, 3-axis micro-vibrations/acoustic anomalies, and respiratory gas levels—to cross-validate signs of life offline in real time.

## Key Features
* **Multi-Sensor Data Fusion:** Cross-validates body temperature (> 37.0°C), CO2/toxic gas concentrations (> 700 ppm), and micro-vibrations/acoustic thresholds (> 60%) to minimize false positives.
* **Offline Edge-to-Host Architecture:** Captures real-time telemetry via an Arduino Uno R3 and streams it over a low-latency USB serial bridge to a Python processing core—requiring zero internet connectivity.
* **Real-Time Sliding-Window Dashboard:** Uses non-blocking Matplotlib visualization (`plt.ion()`) with a 20-frame rolling queue to plot live sensor streams without freezing the execution loop.
* **Hardware Simulation & Fail-Safe Fallback:** Supports full circuit simulation via Wokwi (`diagram.json` & `wokwi.toml`) and includes an automatic synthetic data fallback mode if a physical COM port is unavailable.

## System Architecture & Tech Stack
* **Hardware & Sensors:**
  * **Microcontroller:** Arduino Uno R3
  * **Thermal Sensor:** MLX90614 (Non-contact infrared temperature via I2C)
  * **Motion / Vibration Sensor:** MPU6050 (3-axis accelerometer & gyroscope via I2C)
  * **Gas / Air Quality Sensor:** MQ-135 (CO2 and toxic gas detection via Analog pin)
  * **PCB & Enclosure:** Custom modular PCB designed in EasyEDA with a 3D-printed rugged chassis
* **Software & Simulation:**
  * **Firmware:** C / C++ (Arduino IDE)
  * **Host Analytics & GUI:** Python (`pyserial`, `matplotlib`)
  * **Simulation:** Wokwi Simulator (`wokwi.toml`, `diagram.json`)

## Repository Structure
* `sketch.ino` — Arduino C++ firmware for polling sensors over I2C/Analog pins and transmitting serial packets.
* `import serial.py` — Python host script for serial stream parsing, threshold cross-validation, LED alert commands, and real-time sliding-window plotting.
* `diagram.json` & `wokwi.toml` — Wokwi hardware circuit schematic and simulator configuration.
* `libraries.txt` — Required Arduino libraries for compiling the firmware.
* `AI-Powered Multi-Sensor Fusion System...pdf` — Full technical research paper and system documentation.

## How to Run
1. **Clone the repository:**
   ```bash
   git clone https://github.com/abdumalikm454-cpu/earthquake-project.git
   cd earthquake-project
   Hardware / Simulation Setup:

1.Upload sketch.ino to an Arduino Uno R3 (install dependencies listed in libraries.txt), OR open the project in VS Code with the Wokwi Simulator extension using diagram.json.

2.Run the Python Monitoring Dashboard:
Install required Python packages:pip install pyserial matplotlib

3.Update the serial port (e.g., COM9 or virtual port) inside import serial.py if needed, then run:
python "import serial.py"
