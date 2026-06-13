# Laboratory Activity 1: Timers, Interrupts, and Task Scheduling

**Course:** BCA143 Firmware Programming
**Student:** Vincent Adrian Quitoriano
**Date:** June 2026

---

# Project Description

This project implements timer-based interrupts and a cyclic executive scheduler on the STM32F407ZGT6 microcontroller (RT-Thread RT-Spark board). The system demonstrates the use of hardware timers, interrupt service routines (ISRs), foreground/background scheduling, timing analysis, and event-triggered interrupts.

---

# Hardware

* RT-Thread RT-Spark Development Board (STM32F407ZGT6)
* LEDs:

  * PF11 (Red LED)
  * PF12 (Blue LED)
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

Insert your sequence diagram image here.

Example:

```text
sequence_diagram.png
```

or

```markdown
![Sequence Diagram](sequence_diagram.png)
```

---

# Build Instructions

1. Open project in STM32CubeIDE
2. Build: Project → Build All
3. Connect RT-Spark via USB
4. Upload: Run → Debug or Run

---

# Analysis

## 1. What is the maximum latency for Task A in your system?

The measured maximum latency for Task A was approximately **72 ms**. This is the time between the TIM2 interrupt setting the task flag and Task A beginning execution in the foreground loop.

## 2. If Task B is running when TIM2 interrupt occurs, how does it affect TLatency(Task A)?

If Task B is already executing when TIM2 triggers, Task A must wait until Task B finishes. This increases the latency of Task A by approximately the execution time of Task B plus loop overhead.

## 3. Calculate worst-case TResponse for Task A if all other tasks are running.

Response time is calculated as:

```text
TResponse = TLatency + TTask
```

Using measured values:

```text
TResponse = 72 ms + 50 ms
          = 122 ms
```

Therefore, the worst-case response time for Task A is approximately **122 ms**.

## 4. How would response time change with a preemptive scheduler?

With a preemptive scheduler, high-priority tasks can interrupt lower-priority tasks immediately. This would reduce Task A latency and improve overall response time compared to the cyclic executive system used in this laboratory.

---

# Observation Questions

## 1. What is TRelease for the timer ISR?

TRelease for TIM2 is **1 second**, since the timer interrupt is configured to occur every second.

## 2. What is TISR for your callback function?

Using debugger breakpoints at the entry and exit of the callback function, both measurements showed the same tick value. This indicates that the ISR execution time is less than 1 ms and below the resolution of the system tick counter.

## 3. How does this differ from the polling-based LED blink in Lab 0?

In the polling-based approach, the CPU continuously checks conditions and waits for events. In the interrupt-based approach, the CPU performs other tasks and only executes code when an interrupt occurs, making the system more efficient and responsive.

---

# References

1. Castor, P. R. P. (2025). *Software Design Basics* [Lecture 2]. BCA143 Firmware Programming, MSU-IIT.
2. STMicroelectronics. (2024). *STM32F4 HAL Driver User Manual*.
