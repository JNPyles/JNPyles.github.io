---
layout: project
title: "Building an 8-Bit Breadboard Computer: Logic Gates and Wire Spells"
date: 2025-05-21
categories: [educational]
tags: [computers]
github_url: "https://github.com/JNPyles/8-Bit-Breadboard-Computer-Project"
description: "A deep dive into the construction of a functional 8-bit CPU built entirely from discrete 74-series logic gates on breadboards."
---

## Overview

The goal of this project was to demystify the "black box" of modern computing by building a functional 8-bit CPU from the ground up. Based on the SAP-1 (Simple-As-Possible) architecture, this machine is constructed entirely on breadboards using discrete 74-series logic gates. There are no microcontrollers or pre-programmed SOCs here—just raw digital logic, flip-flops, and several hundred meters of jumper wire.

This project serves as a hands-on exploration of von Neumann architecture, bus arbitration, and the fetch-execute cycle.

## Hardware/Tech Stack

* **Logic Gates:** 74LS series (74LS00, 74LS08, 74LS04, 74LS32).
* **Registers:** 74LS173 4-bit D-type registers (paired for 8-bit operations).
* **Bus Management:** 74LS245 Octal Bus Transceivers with tri-state outputs.
* **Arithmetic Logic Unit (ALU):** 74LS283 4-bit binary full adders and 74LS86 XOR gates for subtraction.
* **Memory:** 74189 RAM chips (configured for 16 bytes of 8-bit memory).
* **Control Logic:** AT28C64 EEPROMs for microcode mapping.
* **Clock:** 555 Timer circuit supporting both astable (auto) and monostable (manual pulse) modes.

## The Build

### The Clock Module
The heart of the system is a 555-timer-based clock. It features three modes: a variable-speed astable mode for automatic execution, a manual debounced pulse for step-by-step debugging, and a selector switch to toggle between them. Clean clock pulses are critical; even a few nanoseconds of "bounce" can cause double-triggering in the registers, leading to corrupted data.

### The Bus and Registers
The computer uses a single 8-bit backbone (the Bus). Components like the A Register, B Register, and Instruction Register connect to this bus. To prevent multiple components from "talking" at once and causing a short, I utilized **74LS245 tri-state buffers**. These allow the control logic to electrically disconnect a module from the bus when its data isn't needed for the current micro-op.

### Arithmetic Logic Unit (ALU)
The ALU handles addition and subtraction. By using XOR gates to selectively invert the bits of the B register and injecting a "carry-in" to the adder, the circuit performs subtraction using **2's complement arithmetic**:

$$A - B = A + (\text{NOT } B) + 1$$

### Control Logic (The Brain)
The most complex part of the build is the control unit. It takes the current instruction from the Instruction Register and the current step of the clock cycle, then outputs the necessary control signals (Enable, Load, etc.) to the rest of the machine. I opted for an **EEPROM-based control logic** which allows me to "reprogram" the CPU's instruction set without moving a single wire.

## Challenges

### Power Distribution and Noise
In a build spanning 10+ breadboards, power sag and logic noise are significant hurdles. Every single IC requires a **0.1µF decoupling capacitor** placed as close to the VCC and GND pins as possible. Without these, the rapid switching of logic gates creates voltage spikes that cause registers to clear or load random data.

### Signal Integrity
Using long jumper wires for the bus creates parasitic capacitance and crosstalk. I found that keeping the bus wires as short as possible and grouping them together helped stabilize the signals. Troubleshooting a single loose wire among hundreds is the primary "debugging" phase of this hardware.

## Current Status/Future Plans

The computer currently supports a basic instruction set: `LDA` (Load A), `ADD`, `SUB`, `OUT` (Output to LEDs), and `HLT` (Halt). 

**What’s next:**
* **Conditional Branching:** Implementing a Flags Register (Carry and Zero) to allow for loops and "if/then" logic.
* **Expanded RAM:** Moving from 16 bytes to 256 bytes using an 8-bit address bus.
* **Custom PCB:** Once the breadboard version is 100% stable, I plan to lay out a modular PCB version to reduce the footprint and improve reliability.

---