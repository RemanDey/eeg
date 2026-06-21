Repository Structure:
<br>
1.  The Resources folder contains learning resources for the implementation of the EEG device
2.  THe PROBLEMS.md file contains the current problems
3.  The NOVELITY.md file contains the novel features adding to this project
4.  FRONTEND FOR THE EEG IS LIVE HERE : https://eeg-data-visualizer.onrender.com
<h1>COMPONENTS NEEDED FOR THE BREADBOARD VERIFICATION OF THE CIRCUIT</h1>
# EEG Data Logger Component Cost Breakdown

Here is a comprehensive breakdown of the components required to build a simple, standalone EEG Data Logger using Upside Down Labs circuits, complete with estimated market prices in India (INR).

### 1. Component Price List

| # | Component Name | Description | Source / Vendor | Est. Price (INR) |
|---|----------------|-------------|-----------------|------------------|
| 1 | **BioAmp EXG Pill** (Assembled) | Analog Front-End (AFE) for filtering & amplifying brain signals. Includes 1x BioAmp Cable v3 & 3x Jumper wires. | Upside Down Labs / Robu.in | ₹2,599 |
| 2 | **Brain BioAmp Band** or **Gel Electrodes** | For dry electrode placement or a reusable set of pre-gelled Ag/AgCl disposable electrodes (Pack of 30+). | Upside Down Labs | ₹599 |
| 3 | **Arduino Nano / ESP32** | Microcontroller with an ADC to read analog data from the EXG Pill and interface with the SD card. | Local Electronic Store / Robu | ₹350 |
| 4 | **MicroSD Card SPI Module** | Breakout board allowing the microcontroller to write `.csv`/`.txt` data streams onto an SD card. | Local Electronic Store / Robu | ₹80 |
| 5 | **MicroSD Card (8GB / 16GB)** | Standard Class 10 MicroSD card to save log files. | Amazon / Local Store | ₹250 |
| 6 | **MB102 Breadboard + Jumper Wires** | Half/Full-sized breadboard with male-to-male & male-to-female wire pack for solderless prototyping. | Local Electronic Store / Robu | ₹180 |
| 7 | **Portable Power Bank / Battery** | 5V USB output power bank to safely isolate the circuit from AC mains noise and prevent shock hazards. | Retail Store / Amazon | ₹499 |
| **-** | **Total Estimated Budget** | **Complete hardware setup for 1-channel standalone EEG logger.** | **-** | **~₹4,557** |

---

### 2. Wiring Guide

follow this configuration to route the amplified signals into the logging unit:

| BioAmp EXG Pill Pin | Microcontroller (e.g., Arduino Nano) | SD Card Module (SPI) | Notes |
|---------------------|---------------------------------------|----------------------|-------|
| **VCC** | 5V or 3.3V                            | VCC                  | Power rail connection |
| **GND** | GND                                   | GND                  | Common Ground (Essential) |
| **OUT** | Analog Pin `A0`                       | -                    | Transmits raw analog EEG waveform |
| -                   | Digital Pin `D13`                     | **SCK** / Clock      | SPI Clock |
| -                   | Digital Pin `D12`                     | **MISO** | SPI Master In Slave Out |
| -                   | Digital Pin `D11`                     | **MOSI** | SPI Master Out Slave In |
| -                   | Digital Pin `D4` (or any IO)          | **CS** / Chip Select | Controlled via `SD.begin(4)` |

---

Components needed:
| Component Name | Description | Qty | Estimated Unit Price (INR) | Total Price (INR) |
| :--- | :--- | :---: | :---: | :---: |
| **ADS1299IPAG** | Low-Noise, 8-Channel, 24-Bit Analog Front-End for EEG | 1 | ₹4,074.00 | ₹4,074.00 |
| **ESP32-S3-MINI-1-N8** | Dual-Core 240MHz MCU, Native 2.4GHz Wi-Fi & BLE 5.0 Module | 1 | ₹492.00 | ₹492.00 |
| **LIS3DHTR** | 3-Axis MEMS Accelerometer (Motion Artifact Detection) | 1 | ₹151.20 | ₹151.20 |
| **Micro SD Card Slot** | Push-Push Micro SD Card Socket (SPI Interface) | 1 | ₹100.80 | ₹100.80 |
| **Voltage Regulators & Inverters** | TPS73233 (3.3V LDO) & Charge Pump for ±2.5V Analog Rails | 1 | ₹462.00 | ₹462.00 |
| **Passives (Resistors/Capacitors)** | SMD 0603/0805 decoupling caps, ferrite beads, 40MHz crystal | 1 | ₹336.00 | ₹336.00 |
| **Connectors & Pins** | Female headers for electrode inputs, Programming pins | 1 | ₹150.00 | ₹150.00 |
| **Custom PCB** | FR4 Modern Octagon Board (Optimized for ESP32 routing) | 1 | ₹252.00 | ₹252.00 |
| **Battery Holder / JST Connection** | 2-pin JST-PH connector for 3-6V Battery Input | 1 | ₹67.20 | ₹67.20 |
| **TOTAL ESTIMATED COST** | | | | **₹6,185.20** |

Circuit Diagram:(this is the opensource circuit-currently working on the custo circuit)
<img width="5037" height="3237" alt="OPEN BCI CYTON CIRCUIT DIAGRAM" src="https://github.com/user-attachments/assets/b83968f6-8dbb-411b-bc5c-96e01ce6df37" />

ROugh Circut diagram for the eeg submodule:
<img width="838" height="310" alt="eeg circuit diagram" src="https://github.com/user-attachments/assets/98ed4bdc-581e-4b3e-b280-47554836bbd1" />
<br>
Rough Breadboard Implementation of the circuit:
<img width="362" height="286" alt="eeg breadboard" src="https://github.com/user-attachments/assets/abe0f9d4-5627-4767-9166-fa3163ca5c63" />


