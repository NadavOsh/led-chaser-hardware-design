# led-chaser-hardware-design
LED chaser PCB using NE555 astable oscillator and CD4017 decade counter for sequential LED control

<img width="863" height="796" alt="LED_Chaser_PCB" src="https://github.com/user-attachments/assets/88d743b2-a6f6-4530-aba0-32dbdf401fec" />


<img width="1197" height="799" alt="image" src="https://github.com/user-attachments/assets/d253f02b-75eb-41c5-a0d1-f846b468a7c6" />


# LED Chaser Hardware Design

## Overview
This project is a discrete hardware implementation of a 10-LED chaser using a timer-based clock and a decade counter.

An astable oscillator built with the NE555 generates a tunable clock signal, which drives a CD4017 decade counter to sequentially light LEDs in a chasing pattern.

The design demonstrates fundamental concepts in analog timing circuits, digital sequencing, and signal conditioning.

---

## Hardware Architecture

### 🔧 Core Components
- **Timer**: NE555 (astable mode oscillator)
- **Counter**: CD74HC4017 (decade counter / decoder)
- **LEDs**: 10 outputs driven sequentially
- **Speed Control**: Potentiometer (adjustable frequency)
- **Connector**: M20-9990246 pin header

---

## ⚙️ System Operation

1. The **NE555 timer** operates in astable mode and generates a square wave clock signal.
2. The clock frequency is controlled with a **potentiometer**, allowing adjustable LED chase speed.
3. The 555 output is connected to the **clock input (CP)** of the CD4017.
4. A **pull-down resistor** is used on the clock line to ensure a defined LOW level and prevent false triggering.
5. The CD4017 advances one output HIGH per clock cycle (Q0 → Q9).
6. Each output drives an LED through a **current-limiting resistor**.
7. After the final step, the sequence resets and repeats continuously.

---

## 🔌 Power Supply
- Typical operation: 5V supply
- All components powered from the same supply rail

---

## ⏱️ Clock Configuration (NE555 Astable)

The oscillation frequency is determined by external resistors, potentiometer, and capacitor:

- Frequency:
  f ≈ 1.44 / ((R1 + 2·R2) · C)

- Duty Cycle:
  D ≈ (R1 + R2) / (R1 + 2·R2)

Where:
- R2 includes the **potentiometer**, enabling real-time speed adjustment

---


## NE555 Timer Pinout

| Pin Number | Name | Function |
|:---:|:---|:---|
| 1 | **GND** | [cite_start]Ground reference (0V) [cite: 472] |
| 2 | **TRIG** | [cite_start]Trigger Input: Initiates the timing cycle [cite: 464] |
| 3 | **OUT** | [cite_start]Output: Provides the timer's output signal [cite: 463] |
| 4 | **RESET** | [cite_start]Reset: Resets the internal flip-flop [cite: 463] |
| 5 | **CTRL** | [cite_start]Control Voltage: Access to internal threshold levels  |
| 6 | **THRES** | [cite_start]Threshold Input: Ends the timing cycle [cite: 466] |
| 7 | **DISCH** | [cite_start]Discharge Output: Used for the timing capacitor  |
| 8 | **VCC** | [cite_start]Supply Voltage: Typically +5V [cite: 471] |


## 🧪 Bring-Up Guide

### Step 1 – Power
- Apply 5V supply
- Verify voltage across VCC and GND

### Step 2 – Oscillator Check
- Probe NE555 output with oscilloscope
- Adjust potentiometer and verify frequency change

### Step 3 – Clock Integrity
- Confirm clean transitions at CD4017 CP input
- Verify pull-down prevents floating/noise

### Step 4 – Counter Verification
- Observe sequential toggling on CD4017 outputs

### Step 5 – LED Operation
- Confirm LEDs light in order with adjustable speed

---

## 🧠 Design Notes
- Potentiometer enables intuitive real-time control of chase speed
- Pull-down resistor ensures stable clock input and prevents false triggering
- Current-limiting resistor protects LEDs and controls brightness
- NE555 provides a simple clock source without requiring firmware
- CD4017 enables sequential logic without a microcontroller

---

## ⚠️ Limitations / Improvements
- Frequency accuracy depends on passive component tolerances
- Duty cycle is not independently controlled
- Could add buffering between 555 and 4017 for improved signal integrity
- Optional: add PWM-based brightness control

---

## 📁 Files Included
- Schematic (PDF)
- PCB layout
- BOM
- Gereber Files
- Pick and Place

---

## 📸 Future Additions
- Oscilloscope captures (clock signal & frequency tuning)
- Measured vs calculated frequency analysis
