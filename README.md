# led-chaser-hardware-design
LED chaser PCB using NE555 astable oscillator and CD4017 decade counter for sequential LED control

<img width="863" height="796" alt="LED_Chaser_PCB" src="https://github.com/user-attachments/assets/88d743b2-a6f6-4530-aba0-32dbdf401fec" />


<img width="1197" height="799" alt="image" src="https://github.com/user-attachments/assets/d253f02b-75eb-41c5-a0d1-f846b468a7c6" />


# LED Chaser Hardware Design

## Overview
This project is a discrete hardware implementation of a 10-LED chaser using a timer-based clock and a decade counter.

An astable oscillator built with the NE555 generates a continuous clock signal, which drives a CD4017 decade counter to sequentially light LEDs in a chasing pattern.

The design demonstrates fundamental concepts in analog timing circuits and digital sequencing.

---

## Hardware Architecture

### 🔧 Core Components
- **Timer**: NE555 (astable mode oscillator)
- **Counter**: CD74HC4017 (decade counter / decoder)
- **LEDs**: 10 outputs driven sequentially
- **Connector**: M20-9990246 pin header

---

## ⚙️ System Operation

1. The **NE555 timer** is configured in astable mode and generates a square wave clock signal.
2. The clock signal is fed into the **CD4017 counter clock input**.
3. The CD4017 advances one output HIGH per clock cycle (Q0 → Q9).
4. Each output drives an LED, creating a running "chaser" effect.
5. After the 10th LED, the sequence resets and repeats.

---

## 🔌 Power Supply
- Typical operation: 5V supply
- All components powered from the same supply rail

---

## ⏱️ Clock Configuration (NE555 Astable)

The oscillation frequency is determined by external resistors and capacitor:

- Frequency:
  f ≈ 1.44 / ((R1 + 2·R2) · C)

- Duty Cycle:
  D ≈ (R1 + R2) / (R1 + 2·R2)

This allows tuning the LED chase speed by adjusting R and C values.

---

## 🔗 Key Connections

| Signal        | Source     | Destination   | Description                     |
|--------------|------------|--------------|---------------------------------|
| CLOCK        | NE555 OUT  | CD4017 CLK   | Drives counter progression      |
| RESET        | CD4017 Q9  | CD4017 RESET | Resets after 10th LED           |
| LED Outputs  | CD4017 Q0–Q9 | LEDs       | Sequential LED control          |
| VCC          | Supply     | All ICs      | Power                           |
| GND          | Supply     | All ICs      | Ground                          |

---

## 🧪 Bring-Up Guide

### Step 1 – Power
- Apply 5V supply
- Verify voltage across VCC and GND

### Step 2 – Oscillator Check
- Probe NE555 output with oscilloscope
- Confirm square wave signal

### Step 3 – Counter Verification
- Observe sequential toggling on CD4017 outputs

### Step 4 – LED Operation
- Confirm LEDs light in order (chasing pattern)

---

## 🧠 Design Notes
- NE555 provides a simple and reliable clock source without a microcontroller
- CD4017 eliminates the need for firmware by handling sequencing in hardware
- Reset is connected to Q9 to create a repeating 10-step cycle
- Design demonstrates integration of analog and digital components

---

## ⚠️ Limitations / Improvements
- No brightness control (PWM could be added)
- Frequency stability depends on passive component tolerances
- Could add variable resistor for adjustable speed
- No current limiting discussion (ensure proper resistors for LEDs)

---

## 📁 Files Included
- Schematic (PDF)
- PCB layout
- BOM

---

## 📸 Future Additions
- Board images
- Oscilloscope captures of clock signal
- Measured frequency vs calculated values
