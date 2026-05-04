# 🏎️  Dual-Mode Arduino Car

> A robotics project based on **Arduino UNO**, developed for the Microprocessors lab. The smart car features a hybrid operating mode (Manual Control via Bluetooth / Autonomous Mode with obstacle avoidance) and is programmed at the hardware level, using direct register manipulation and timers instead of standard Arduino functions.

##  Team

* **Chițimia Diana-Andreea** – Hardware / Software
* **Pogonici-Bălțățeanu Tiberiu** – Hardware / Software

> *Project developed for the **Microprocessors** course, Year 2, **Politehnica University of Timișoara**.*
---

## 📝 Project Description
This project represents the physical and software implementation of an autonomous 2WD vehicle.

The car can be controlled from a smartphone app, but at the press of a button, it switches to "Auto-Pilot", navigating its environment using an ultrasonic sensor.

### ✨ Operating Modes:
1. **🎮 Manual Mode (Bluetooth):** Directional control (Forward/Backward/Left/Right) via the **Dabble** smartphone app.
2. **🤖 Autonomous Mode:** The car drives itself forward. When the HC-SR04 sensor detects an obstacle at a distance of less than 20 cm, the car brakes, reverses, and turns right to avoid the blockage before resuming its path. (the sensor is currently at the back of the car)

---

## 🛠️ Hardware Components

The following components were used to build this project:
*  1x Arduino UNO compatible development board (ATmega328P)
*  1x 2WD Smart Car Kit (acrylic chassis, 2 wheels, 1 caster wheel)
*  2x DC Motors
*  1x L298N Motor Driver (H-Bridge)
*  1x HC-SR04 Ultrasonic Sensor
*  1x BLE Bluetooth Module (HM-10 / AT-09) iOS & Android compatible
*  2x 18650 Li-ion Batteries (7.4V total) + Battery Holder + Power Switch
* Mini-Breadboard and Dupont jumper wires (M-M, M-F)

---

## 💻 Technical & Software Concepts

Unlike standard Arduino projects, the source code implements specific Embedded Systems techniques:

* **Direct Port Manipulation (Port Registers):** No `digitalWrite()` or `pinMode()` functions are used. Pin configuration and motor direction control are achieved by directly modifying the bits in the `DDRB`, `DDRD`, `PORTB`, and `PORTD` registers.
* **Hardware Timers (Fast PWM):** Motor speed is not generated using `analogWrite()`. Instead, **Timer1** is set up in Fast PWM mode by directly configuring the `TCCR1A` and `TCCR1B` registers, and the duty cycle (speed) is defined through the `OCR1A` and `OCR1B` registers.
* **Communication:** The `Dabble` library is used to parse Bluetooth signals from the smartphone.

---

## ⚙️ Wiring Schema (Pinout)

| Component | Arduino Pin | Associated Register |
| :--- | :--- | :--- |
| **L298N - ENA** | Pin 9 | Timer1 (OC1A) |
| **L298N - ENB** | Pin 10 | Timer1 (OC1B) |
| **L298N - IN1** | Pin 4 | PORTD (Bit 4) |
| **L298N - IN2** | Pin 5 | PORTD (Bit 5) |
| **L298N - IN3** | Pin 6 | PORTD (Bit 6) |
| **L298N - IN4** | Pin 7 | PORTD (Bit 7) |
| **HC-SR04 - Trig** | Pin 8 | PORTB (Bit 0) |
| **HC-SR04 - Echo** | Pin 12 | PORTB (Bit 4) |
| **BT HM-10 - TX** | Pin 2 | SoftwareSerial (RX) |
| **BT HM-10 - RX** | Pin 3 | SoftwareSerial (TX) |



---

<!--  -->