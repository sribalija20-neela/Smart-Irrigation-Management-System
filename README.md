# Smart-Irrigation-Management-System
# Automated Smart Irrigation & Soil Moisture Management System

A closed-loop automated agricultural hardware and firmware system built on the **ATmega328P microcontroller** using bare-metal **Embedded C**. The system tracks soil moisture constraints dynamically via analog sensors, scales input matrices, and handles real-time delivery control of isolated high-current water pumps while reporting live telemetry parameters.

## 🚀 Key Features
* **Low Pin-Count Interface:** Configured a 16x2 character LCD display via **I2C serial protocol** (SDA/SCL) to maximize available microcontroller physical pins.
* **Data Scaling Matrix:** Developed low-level ADC hardware sampling routines to translate continuous raw analog sensor voltage ranges directly into discrete 0-100% moisture percentage bounds.
* **High-Current Isolation Sub-circuit:** Designed a discrete switching relay network utilizing logic-level transistor configurations to protect the MCU core from inductive motor voltage spikes.

## 📊 System Architecture Block Diagram
![System Architecture](architecture_diagram.png)  
*Figure 1: Control loop block diagram mapping continuous analog input tracking, I2C bus communications, and physical load decoupling.*

## 🛠️ How It Works (System Architecture)
1. **Moisture Sensing:** A capacitive soil moisture sensor outputs a stable analog voltage based on the surrounding soil matrix moisture concentration.
2. **Firmware Evaluation:** The internal Analog-to-Digital Converter (ADC) channels sample this incoming data stream.
3. **Control Action Loop:** If the scaled percentage falls below the targeted safety limit boundary:
   * A targeted GPIO pin transitions to a logic `HIGH` state.
   * This logic signal drives a discrete BJT/MOSFET transistor configuration into saturation, closing the circuit to trigger the 5V DC submersible pump.
4. **Closed-Loop Feedback termination:** Once moisture conditions are satisfied, the control variable drops back to `LOW`, disengaging power to the load cleanly.
5. **Live Telemetry Interface:** The microcontroller bundles status telemetry metrics into structured data packets and transfers them over the **I2C bus lines** to update the local LCD frame buffer.

## 📂 Repository Structure
* `main.c` : Contains the bare-metal firmware source file.
* `architecture_diagram.png` : Functional system block architecture.

## 🔧 Tools & Tech Stack
* **Language:** Embedded C / C++
* **Hardware Profile:** ATmega328P Core, Capacitive Soil Moisture Sensor, 5V DC Submersible Pump, 16x2 LCD with I2C Module, Transistor Driver Switching Circuit
* **IDE & Design Environments:** Arduino IDE / Keil uVision
