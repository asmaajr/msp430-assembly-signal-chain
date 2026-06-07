## Overview
This repository contains a low level embedded system implemented entirely in MSP430 Assembly (.s43). Designed with strict engineering practices, the system establishes a portable, interrupt-driven analog signal chain interface capable of real time waveform sampling, signal classification, high-precision fixed-point math emulation, and live LCD telemetry.

## Software Architecture & Portability
Unlike traditional monolithic assembly code, this project employs a modular, layered architecture to decouple hardware dependencies from core application logic:
* Board Support Package (BSP): Manages board-specific pin configurations, clock initializations, and physical mappings.
* Hardware Abstraction Layer (HAL): Provides clean APIs for internal peripherals (ADC, DAC, Timer) and external components (Character LCD, Pushbuttons), allowing seamless portability across different MSP430 MCU families.
* Finite State Machine (FSM): A centralized control unit coordinates system behaviors (e.g., Sleep, Idle, Active Sampling, Configuration) based on external asynchronous events.
* Interrupt-Driven Execution: Relies entirely on hardware interrupts (Timer ticks, ADC conversions, Pushbuttons) to trigger state transitions, maximizing CPU sleep time and optimizing power efficiency.

## Key Features
* Dynamic Signal Classification: Automatically samples and classifies periodic input signals (Sine, Triangle, and PWM waves) with a deterministic 1-second display refresh cycle.
* Fixed-Point Math Emulation (UQ12.20): Implements robust 32-bit fixed-point arithmetic routines in assembly to accurately calculate average voltage without floating-point hardware support.
* Custom Peripheral Drivers:
    * Character LCD Driver: Direct port-mapped control and data timing loops.
    * ADC10/ADC12 Interface: Configured for maximum signal-to-noise ratio (SNR) and optimized sampling rates.
    * DAC12 Controller: Reconstructs or modifies analog wave outputs dynamically.
* Software Debouncing: Robust interrupt-handling with software-timed guard bands to prevent bouncing from physical pushbuttons.

## Tools & Development Environment
* Development Language: MSP430 Assembly Language (.s43)
* IDE / Toolchain: IAR Embedded Workbench for MSP430
* Target Hardware: MSP430 Personal Evaluation Board, Digital Oscilloscope, Function Generator.

