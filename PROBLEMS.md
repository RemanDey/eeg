# Known Issues & Hardware Limitations (Cyton Architecture)

This document outlines the known architectural bottlenecks, component deprecations, and performance limitations inherent to this specific hardware configuration (ADS1299 + PIC32MX + RFduino). Contributors and developers looking to fork or iterate on this design should review these challenges before manufacturing.

---

## 1. Supply Chain & Component Obsolescence
* **RFduino (RFD22301) Deprecation:** The RFduino BLE module and its ecosystem are entirely deprecated and out of production. Sourcing genuine components for new builds is highly difficult, relying on residual distributor stock or expensive liquidations.
* **Prototyping Risk:** The TI ADS1299 is a medical-grade, highly specialized analog front-end. Because it represents over 50% of the total Bill of Materials (BOM) cost, any manual assembly errors (e.g., thermal damage during SMD reflow) result in high financial penalties per prototype iteration.

## 2. Wireless Overheads & Latency Instability
* **High Timing Jitter:** The legacy firmware stack passing data from the PIC32 through the RFduino introduces variable packet latency (jitter). This makes the baseline architecture poorly suited for strict **Event-Related Potential (ERP)** research, where neural responses must be tightly synchronized with external stimuli within sub-millisecond precision.
* **Lack of Encryption:** The default radio protocol streams raw microvolt data packets over an unencrypted wireless channel to a dedicated USB dongle, offering no hardware-level data masking or modern cybersecurity protocols.

## 3. Bandwidth Limitations & Sampling Degradation
* **Channel vs. Sample Rate Bottleneck:** While the ADS1299 is capable of high sampling rates, the system is bottlenecked by the PIC32's processing overhead and the BLE radio bandwidth. 
* **Scaling Penalty:** Sampling operates at $250\text{ Hz}$ for the base 8 channels. However, expanding the architecture to 16 channels forces the firmware to slash the sampling rate in half to **$125\text{ Hz}$** to avoid dropping frames over the air. This limits the ability to safely capture higher-frequency Gamma band fluctuations without risk of signal aliasing.

## 4. Compute Constraints (No On-Device DSP)
* **Pass-Through Architecture:** The PIC32MX250F128B acts purely as a SPI-to-BLE data pass-through controller. It lacks the computational overhead, Floating Point Unit (FPU), or memory layout required to run edge-computing tasks.
* **Host Dependence:** Digital Signal Processing (DSP) tasks—including real-time Fast Fourier Transforms (FFTs), high-pass/low-pass line-noise filtering ($50\text{ Hz}/60\text{ Hz}$), and automated eye-blink artifact removal—cannot be done on the headset and must be offloaded entirely to a host computer.

## 5. Layout-Sensitive Signal Integrity
* **Analog/Digital Ground Crosstalk:** The tiny footprint ($2.41" \times 2.41"$) means high-frequency digital clock lines from the PIC32 and high-power radio bursts from the BLE module sit in ultra-close proximity to the ultra-sensitive nanovoltage traces of the ADS1299. Poor PCB ground plane isolation (splitting AGND and DGND) easily corrupts the signal-to-noise ratio, neutralizing the $121\text{ dB}$ capability of the ADC.

---

## Proposed Next-Generation Upgrades
If you are modifying this repository for a modern production run, it is highly recommended to abandon the legacy PIC32 + RFduino dual-chip layout and upgrade to:
1. **ESP32-S3 or nRF52840 SoC:** Replaces both legacy chips, lowers build cost by roughly ₹1,000, adds native Bluetooth 5.0/Wi-Fi, and provides hardware encryption.
2. **On-Board ARM Cortex Core:** Grants the processing power required to execute on-device filtering and basic machine learning classification before transmitting data.1. Cost of the instrumentation amplifier is high- we need to find alternative to it
   
