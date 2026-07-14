# Design and Implementation of a Low-Power 8-bit SAR ADC

Full custom design and simulation of an 8-bit **Successive Approximation Register (SAR) Analog-to-Digital Converter** in **45 nm CMOS technology**, built block-by-block in Cadence Virtuoso and verified through transient, static-linearity, and power analysis.

> M.Tech Major Project | Electronics & Communication Engineering (VLSI Design) | Nirma University, Ahmedabad
> Author: **Moksh Prajapati** (24MRV011) | Guide: **Dr. Piyush Bhatasana**

---

## 📌 Overview

SAR ADCs sit in the sweet spot between power, area, and speed — making them the default choice for **biomedical instrumentation, portable electronics, and IoT sensor nodes**. This project designs, simulates, and integrates every functional block of an 8-bit SAR ADC from the transistor level up, targeting low supply voltage operation and minimal energy consumption.

The converter performs an 8-cycle binary search: each clock cycle, the SAR logic makes a bit guess, the capacitive DAC generates the corresponding trial voltage, and a dynamic comparator checks it against the sampled input — narrowing the result one bit at a time until the full 8-bit digital word is resolved.

## 🧩 Architecture

| Block | Design Choice | Purpose |
|---|---|---|
| **Sample & Hold** | Bootstrapped switch | Constant V<sub>GS</sub> sampling → flat on-resistance, low distortion |
| **Comparator** | Single-tail dynamic latch | Zero static power, fast regeneration, low offset |
| **SAR Logic** | TSPC (True Single-Phase Clock) flip-flops in a ring-counter + register layout | Self-timed, asynchronous bit sequencing |
| **DAC** | Binary-weighted capacitive array (128C → 1C + dummy) | Passive charge redistribution, doubles as S/H element |
| **Output Register** | CMOS D-flip-flops | Static, glitch-free 8-bit output latch on EOC |

## ⚙️ Key Specifications

| Parameter | Value |
|---|---|
| Technology | 45 nm CMOS |
| Resolution | 8 bits |
| Supply Voltage | 1 V |
| Common-Mode Voltage | 0.5 V |
| SINAD | 43.48 dB |
| ENOB | 6.93 bits |
| Total Power | 19.88 µW |
| DNL | +0.650 / −0.650 LSB (monotonic, no missing codes) |
| INL | +1.000 / −0.598 LSB |

## 📊 Results

- **Sample & Hold** — bootstrapped switch samples cleanly at 160 MHz with negligible droop.
- **Comparator** — resolves a 50 mV differential in ~250 ps with full regeneration to logic levels before the next clock edge.
- **SAR Logic** — TSPC-based sequencer correctly steps MSB → LSB, one bit per 5 ns cycle, firing EOC after 8 cycles.
- **Capacitive DAC** — binary-weighted charge redistribution shows correct monotonic settling across all 256 codes.
- **Full ADC** — staircase output accurately tracks a sine-wave input across the full 1 V swing.

Detailed waveforms, INL/DNL plots, and per-block analysis are in the [project report](./24MRV011_Major_project_thesis.pdf).

## 🛠️ Tools

- Cadence Virtuoso (Schematic Capture & Transient Simulation)
- GPDK 45 nm CMOS PDK

## 📁 Repository Structure

```
├── schematics/        # Block-level and top-level Virtuoso schematics
├── simulations/        # Testbenches and simulation results
├── results/             # Waveforms, INL/DNL plots
└── docs/                # Full project report (PDF)
```

## 🔭 Future Work

- Differential CDAC architecture for improved noise immunity
- Asynchronous/monotonic switching to further cut switching energy
- Extension to 10–12 bit resolution for advanced mixed-signal applications

## 📄 Reference

Full report: *Design and Implementation of Low Power 8-bit SAR ADC*, Major Project Report, Department of ECE, Institute of Technology, Nirma University, May 2026.

---

⭐ If you found this project useful, consider starring the repo!
