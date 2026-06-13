# Laboratory Activity 1: Timers, Interrupts, and Task Scheduling

**Course:** BCA143 Firmware Programming
**Student:** Vincent Adrian Quitoriano
**Date:** June 2026

---

# Project Description

This project implements  time driven foreground/background scheduling system is built on STM32F407ZGT6 microcontroller using the RT-Thread RT-Spark development board and demonstrate the use of hardware timers, interrupt service routines, cyclic executive scheduling and event triggered interrupts.
---

# Hardware

* RT-Thread RT-Spark Development Board (STM32F407ZGT6)
* LEDs: PF11 (Red), PF12 (Blue)
* User Button: PA0
* Debug Pin: PE0

---

# Features

* TIM2: 1 Hz periodic interrupt (high priority)
* TIM3: 2 Hz periodic interrupt (medium priority)
* External interrupt on button press
* Foreground/background system architecture
* Timing measurement and analysis

---

# Timing Measurements

| Parameter         | Definition                 | Measured Value | Units   |
| ----------------- | -------------------------- | -------------- | ------- |
| TRelease(TIM2)    | Timer interrupt occurs     | 1.0            | seconds |
| TLatency(Task A)  | Delay before Task A starts | 72             | ms      |
| TISR(TIM2)        | Time spent in ISR          | < 1            | ms      |
| TTask(Task A)     | Task A execution time      | 50             | ms      |
| TResponse(Task A) | Total response time        | 122            | ms      |

---

# Sequence Diagram



---

# Build Instructions

1. Open project in STM32CubeIDE
2. Build: Project → Build All
3. Connect RT-Spark via USB
4. Upload: Run → Debug or Run

---

# Analysis

## 1. What is the maximum latency for Task A in your system?

The measured maximum latency for Task A is approximately 72 ms

## 2. If Task B is running when TIM2 interrupt occurs, how does it affect TLatency(Task A)?

Task A cannot start immediately because the main loop must finish executing Task B
first.

## 3. Calculate worst-case TResponse for Task A if all other tasks are running.

TResponse is calculated as TResponse = TLantency + TTask so
TResponse = 72 + 50 = 122ms therefore worst case response time for Task A is
Approximately 122ms

Therefore, the worst-case response time for Task A is approximately **122 ms**.


# References

1. Castor, P. R. P. (2025). *Software Design Basics* [Lecture 2]. BCA143 Firmware Programming, MSU-IIT.
2. STMicroelectronics. (2024). *STM32F4 HAL Driver User Manual*.
