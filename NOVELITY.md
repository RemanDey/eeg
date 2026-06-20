# Architectural Novelty & Edge Capabilities

By upgrading the legacy open-source EEG architecture from a dual-chip configuration (PIC32MX + RFduino) to a unified **ESP32-S3 SoC + ADS1299 Analog Front-End**, this project introduces several novel, edge-computing capabilities previously impossible on open-source biosensing hardware.

---

## 1. On-Edge AI Artifact Rejection (TinyML)
* **The Novelty:** Real-time, localized signal cleansing directly on the headset.
* **Implementation:** Utilizing the ESP32-S3's dual-core vector instructions, we can deploy a lightweight **TensorFlow Lite for Microcontrollers** model (such as a 1D Convolutional Neural Network or an Autoencoder). By cross-referencing raw EEG feeds with the onboard `LIS3DH` 3-axis accelerometer, the chip can identify and dynamically subtract muscle artifacts (electromyography / EMG) and eye-blinks (electrooculography / EOG) on the fly.
* **Advantage:** Eliminates the need for heavy post-processing scripts on the host machine; downstream apps receive a clean, pre-filtered neural stream.

## 2. Standalone Active Impedance Diagnostics
* **The Novelty:** Visual hardware-level skin-to-electrode resistance tracking without host software dependencies.
* **Implementation:** The architecture utilizes the ADS1299's built-in **Lead-Off Detection** circuitry to inject a low-level, high-frequency test current into the connected channels. The ESP32-S3 continuously samples this return current to calculate impedance. 
* **User Interface:** The headset maps these values directly to a localized strip of addressable micro-LEDs (e.g., WS2812B), dynamically color-coding connection quality (*Red = Poor Contact, Yellow = Margin Noise, Green = High Signal Integrity*). 
* **Advantage:** Enables swift, standalone physical setup of the EEG cap before any computer or smartphone pairing takes place.

## 3. Phase-Locked Closed-Loop Auditory Stimulation
* **The Novelty:** Real-time neurological feedback targeting specific brainwave phases with sub-millisecond precision.
* **Implementation:** The $240\text{ MHz}$ processor allows the firmware to run a localized phase-tracking algorithm (such as a lock-in amplifier or short-time Fourier transform) on localized bands, such as Slow-Wave Delta waves ($0.5 - 4\text{ Hz}$).
* **Action:** Upon identifying the precise ascending peak of a Delta wave, the ESP32 triggers a microsecond-synchronized auditory click via an onboard I2S DAC or low-latency Bluetooth Audio stream.
* **Advantage:** Replicates expensive, clinical-grade sleep-optimization and neuro-memory consolidation hardware at a fraction of the cost.

## 4. Multi-User "Swarm" Hyperscanning via ESP-NOW
* **The Novelty:** Peer-to-peer inter-headset synchronization for multi-user social neuroscience.
* **Implementation:** By leveraging Espressif’s proprietary connection protocol, **ESP-NOW**, multiple headsets can communicate directly with one another over a low-latency (<2ms), packet-isolated channel without requiring a central Wi-Fi router or access point.
* **Advantage:** Enables mobile "hyperscanning" studies (tracking how brainwaves synchronize between musicians, gamers, or conversational pairs) natively out in the field without regional networking limits.

## 5. Dynamic Web-Based OTA "Brain-State" Switching
* **The Novelty:** Zero-software setup adjustment through localized web-hosting.
* **Implementation:** The ESP32-S3 hosts an internal asynchronous web server. By connecting a smartphone or PC to the headset's local access point, users can access an interactive dashboard.
* **Capabilities:** Users can hot-swap digital Infinite Impulse Response (IIR) filters or alter sample rates on the fly (e.g., switching from *Alpha Meditation Tracking at 250Hz* to *Gamma Cognitive Capture at 1000Hz*) via an Over-the-Air (OTA) web command, completely eliminating the need for firmware re-flashing.
