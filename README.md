# PILOT Dataset — Privacy-preserving data collectIon of wireLess cOmmunication Technologies

[![Paper](https://img.shields.io/badge/Paper-IEEE%20IWCMC%202024-blue)](https://doi.org/10.1109/IWCMC61514.2024.10592486)
[![Preprint](https://img.shields.io/badge/Preprint-HAL%20Open%20Science-green)](https://inria.hal.science/hal-04524617)
[![License](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey)](LICENSE)

---

## Overview

The **PILOT dataset** is a labeled, multi-technology wireless sensing dataset collected across a range of real-life mobility scenarios. It jointly captures traces from three wireless communication technologies — **WiFi**, **BLE (Bluetooth Low Energy)**, and **LoRa** — alongside inertial sensor measurements (acceleration, roll, pitch), all recorded simultaneously using Pycom FiPy microcontrollers.

The dataset is intended for research in **human mobility classification**, **context-aware sensing**, and **IoT data analysis**. It is the first publicly available labeled dataset combining multi-technology wireless traces and inertial measurements across diverse mobility contexts.

**Key statistics:**
- ~90 hours of collected data
- ~200 MB total size
- 120 labeled log files across 11 mobility scenarios
- Collected in France and South Africa

**Reference paper:**  
J. Koteich and N. Mitton, *"Dataset Collection of Multi-Communication Technologies Monitored in Different Mobility Contexts,"* in *20th IEEE International Wireless Communications and Mobile Computing Conference (IWCMC)*, 2024.  
DOI: [10.1109/IWCMC61514.2024.10592486](https://doi.org/10.1109/IWCMC61514.2024.10592486) · Open access: [HAL](https://inria.hal.science/hal-04524617)

---

## Table of Contents

- [Dataset Description](#dataset-description)
- [Mobility Scenarios](#mobility-scenarios)
- [Data Collection Setup](#data-collection-setup)
- [File Structure](#file-structure)
- [Data Format](#data-format)
- [Privacy and Security](#privacy-and-security)
- [Application and Validation](#application-and-validation)
- [How to Cite](#how-to-cite)
- [Contact](#contact)

---

## Dataset Description

Each log file in the dataset corresponds to a single scanning session of between 10 minutes and approximately 3 hours. Files are organized by mobility scenario and labeled with the conditions of collection.

Each session produces four files, one per sensing modality:

| File | Technology | Node | Sampling |
|------|-----------|------|----------|
| `WiFi.csv` | WiFi probe responses | Node W | Every 2 s |
| `BLE.csv` | BLE advertisement beacons | Node B | Every 1 s |
| `LoRa.csv` | LoRa packets (EU868 band) | Node L | Every ~2 s |
| `acc.csv` | Acceleration, roll, pitch, battery | Node X | Continuous |

---

## Mobility Scenarios

The dataset covers 11 labeled scenarios divided into two top-level categories:

### Static Scenarios
| Label | Scenario | Description |
|-------|----------|-------------|
| H1 | Home | Apartment in a residential building, village |
| U1 | University | University campus environment |
| O1 | Office (rural) | Office in a low-density area |
| O2 | Office (urban) | Office surrounded by other buildings |
| R1 | Restaurant | City restaurant, low crowd density |

### Mobile Scenarios
| Label | Scenario | Description |
|-------|----------|-------------|
| B1 | Bus (intercity) | Autocar between city and village, crowded |
| B2 | Bus (urban) | City bus, very crowded |
| C1 | Car (highway) | Auto-route, rural area |
| C2 | Car (mixed) | Auto-route transitioning to village roads |
| T1 | Train (TER) | Regional train between two cities |
| T2 | Train (TGV) | High-speed train |

Data was collected across France (including TGV, TER, and RER lines, and various urban and rural environments) and in South Africa. Several scenarios include repeated collection sessions to ensure behavioral consistency across files.

---

## Data Collection Setup

Four Pycom FiPy microcontrollers were used, each dedicated to a single sensing modality to avoid interrupt-induced delays in multi-technology single-device setups. Each FiPy was connected to a Pytrack or Pysense expansion board providing an accelerometer and SD card storage.

Time synchronization was achieved by connecting to an NTP server via a local WiFi access point at the start of each session, synchronizing the real-time clock (RTC) on each device.

**Hardware:**
- Pycom FiPy microcontrollers (MicroPython-based)
- Pytrack / Pysense expansion boards
- External LoRa antenna (EU868 band)
- SD cards for local data storage

---

## File Structure


Each scenario folder contains sub-folders named with the scenario label prefix. Each sub-folder holds the four CSV files for that session alongside a short annotation file describing the scanning conditions and time interval.

---

## Data Format

### WiFi (`WiFi.csv`)
| Field | Description |
|-------|-------------|
| `timestamp` | Unix timestamp of probe response detection |
| `ssid` | Network name (pseudonymized) |
| `bssid` | MAC address of the AP (anonymized, see Privacy section) |
| `sec` | Security type (0=Open, 1=WEP, 2=WPA-PSK, 3=WPA2-PSK, 4=WPA/WPA2-PSK) |
| `channel` | WiFi channel (1–11) |
| `rssi` | Received signal strength (dBm) |

Scanning band: 2.4 GHz – 2.4835 GHz (802.11b/g/n).

### BLE (`BLE.csv`)
| Field | Description |
|-------|-------------|
| `timestamp` | Unix timestamp of advertisement reception |
| `mac` | MAC address (anonymized, see Privacy section) |
| `name` | Device name (pseudonymized) |
| `rssi` | Received signal strength (dBm) |
| `adv_tx_pwr` | Advertising TX power |
| `tx_range` | Transmission range |
| `def_tx_pwr` | Default TX power |
| `scan_tx_pwr` | Scanning TX power |
| `conn_tx_pwr` | Connection TX power |

### LoRa (`LoRa.csv`)
| Field | Description |
|-------|-------------|
| `timestamp` | Unix timestamp of packet reception |
| `spreading_factor` | LoRa spreading factor |
| `data` | Packet payload (masked) |
| `frequency` | Listening frequency (Hz) |
| `bandwidth` | Channel bandwidth |
| `rx_timestamp` | Reception timestamp from radio |
| `rssi` | Received signal strength (dBm) |
| `snr` | Signal-to-noise ratio (dB) |
| `sfrx` | Spreading factor used on RX |
| `sftx` | Spreading factor used on TX |
| `tx_trials` | Number of transmission attempts |
| `tx_power` | Transmission power |
| `tx_time_on_air` | Time on air for transmission (ms) |
| `tx_counter` | Transmission counter |
| `tx_frequency` | Transmission frequency (Hz) |

Monitored frequencies (EU868 band): 863–869 MHz across 15 frequency slots.

### Acceleration (`acc.csv`)
| Field | Description |
|-------|-------------|
| `timestamp` | Unix timestamp |
| `acceleration` | Acceleration magnitude |
| `roll` | Roll angle |
| `pitch` | Pitch angle |
| `battery_voltage` | Device battery voltage (V) |
| `battery_percentage` | Battery charge level (%) |

---

## Privacy and Security

This dataset complies with the **General Data Protection Regulation (GDPR)**, which classifies MAC addresses and device names as personal data.

**Anonymization approach:**  
The dataset is organized into files corresponding to independent time windows (10 minutes to ~3 hours each). For each file, MAC addresses are transformed into pseudonymous device identifiers using **HMAC-SHA-256** with a randomly generated secret key. The key is unique per file and discarded after processing, ensuring that device identifiers cannot be linked across files. Device names are replaced with random symbols, and LoRa packet payloads are fully masked.

---

## Application and Validation

The utility of the dataset was demonstrated by training a classical machine learning classifier (XGBoost) on the WiFi and BLE traces to predict mobility context. The model achieved **94% classification accuracy** across 10 scenarios, confirming that the multi-technology wireless environment carries strong discriminative signal for mobility state detection.

This application is described in detail in:

> J. Koteich and N. Mitton, *"Machine Learning Approach for Mobility Context Classification using Radio Beacons,"* in *IEEE MASCOTS 2023*, New York, USA, October 2023.

---

## How to Cite

If you use the PILOT dataset in your research, please cite:

```bibtex
@inproceedings{koteich2024pilot,
  author    = {Jana Koteich and Nathalie Mitton},
  title     = {Dataset Collection of Multi-Communication Technologies Monitored in Different Mobility Contexts},
  booktitle = {20th IEEE International Wireless Communications and Mobile Computing Conference (IWCMC)},
  year      = {2024},
  doi       = {10.1109/IWCMC61514.2024.10592486}
}
```

---

## Contact

**Jana Koteich**  
Postdoctoral Researcher, Inria / INSA Lyon — CITI Lab  
[jana.koteich@inria.fr](mailto:jana.koteich@inria.fr)  
[janakoteich.org](https://janakoteich.org) · [GitHub](https://github.com/Janakoteich) · [LinkedIn](https://linkedin.com/in/jana-koteich-62549218b/)

**Nathalie Mitton**  
Research Director, Inria Lille — FUN Team  
[nathalie.mitton@inria.fr](mailto:nathalie.mitton@inria.fr)
