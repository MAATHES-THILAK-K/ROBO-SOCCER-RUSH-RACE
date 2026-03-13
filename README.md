# Robo Competition Bots (Robo Race • Robo Rush • Robo Soccer)

This repository contains the firmware and system configuration used for the robots built for **Robo Race, Robo Rush (All-Terrain), and Robo Soccer competitions**.
The robot is designed as a **high-torque 4-wheel drive platform** controlled using a **FlySky CT6B transmitter and receiver system**.

The control system reads PWM signals from the receiver and converts them into motor control signals to drive the robot forward, backward, and steer using differential drive.

---
![Robo Soccer Rush Race](IMAGES/Screenshot%202026-03-13%20185125.png)

# System Overview

The robot uses an **Arduino Uno** as the main controller to process receiver signals and control two **BTS7960 motor drivers**, which power **four 600 RPM DC motors**.

Each motor driver controls a pair of motors (left side and right side), enabling the robot to perform **tank steering**.

The robot was initially designed using an **ESP32 controller**, but the board was damaged due to a **buck converter voltage issue**. The system was later redesigned using **Arduino Uno** and a more stable **LM buck converter** for voltage regulation.

---

# Hardware Components

| Component         | Specification                       |
| ----------------- | ----------------------------------- |
| Microcontroller   | Arduino Uno                         |
| Transmitter       | FlySky CT6B                         |
| Receiver          | FlySky 6-Channel Receiver           |
| Motor Drivers     | 2 × BTS7960 High Power Motor Driver |
| Motors            | 4 × 600 RPM DC Motors               |
| Battery           | 70C 35W Battery Pack                |
| Voltage Regulator | LM Buck Converter                   |

---

# Motor Configuration

The robot uses a **differential drive system**.

| Side       | Motor Driver     | Motors   |
| ---------- | ---------------- | -------- |
| Left Side  | BTS7960 Driver 1 | 2 Motors |
| Right Side | BTS7960 Driver 2 | 2 Motors |

Both motors on each side are connected **in parallel** to the driver.

---

# Arduino Pin Configuration

### Receiver Input

| Function         | Arduino Pin |
| ---------------- | ----------- |
| Throttle Channel | 3           |
| Steering Channel | 2           |

```cpp
#define THROTTLE_PIN 3
#define STEER_PIN 2
```

---

### Motor Driver Pins

| Motor Driver | Arduino Pins |
| ------------ | ------------ |
| Left Driver  | 9, 10        |
| Right Driver | 5, 6         |

These pins are **PWM capable pins** and are used for motor speed control.

| Function         | Pin |
| ---------------- | --- |
| Left Motor RPWM  | 9   |
| Left Motor LPWM  | 10  |
| Right Motor RPWM | 5   |
| Right Motor LPWM | 6   |

---

# Control Logic

The robot uses **tank steering logic**:

| Input       | Left Motors | Right Motors | Robot Motion  |
| ----------- | ----------- | ------------ | ------------- |
| Throttle ↑  | Forward     | Forward      | Move Forward  |
| Throttle ↓  | Backward    | Backward     | Move Backward |
| Steering →  | Faster      | Slower       | Turn Right    |
| Steering ←  | Slower      | Faster       | Turn Left     |
| Both Center | Stop        | Stop         | Idle          |

---

# Power System

The robot is powered by a **high-discharge battery pack**:

* Battery: **70C 35W**
* Voltage regulation handled using an **LM Buck Converter**
* Buck converter steps down the voltage to safely power the **Arduino and receiver**

⚠️ Note:
A previous design using **ESP32 failed due to unstable buck converter output**, which resulted in the controller being damaged.

---

# Features

* Differential drive control
* High-torque 4WD drivetrain
* Remote control using FlySky transmitter
* PWM-based motor speed control
* Robust power system with buck regulation

---

# Applications

This robot platform was used in:

* Robo Race competitions
* Robo Rush (all-terrain challenge)
* Robo Soccer matches

The platform is designed for **high speed, strong torque, and reliable remote control operation**.




That will make your repository look **like a professional robotics project** instead of just a code repo. 🚀
