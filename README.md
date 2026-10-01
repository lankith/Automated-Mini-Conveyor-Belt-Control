# Automated Mini Conveyor Belt Speed Regulator

An automated mini conveyor belt system with closed-loop speed control and object proximity detection designed in Tinkercad using Arduino Uno.

## Live Simulation Link
* **Tinkercad Project:** [Interactive Simulation Link](https://www.tinkercad.com/things/5FbrYMM33mE-automated-mini-conveyor-belt-speed-regulator?sharecode=To8Hex7Fxj1QQIdaHG1_RzNIhPuRx4AOL3T2zJrdkkg)

---

## Hardware & Pin Mapping

| Component | Function | Arduino Pin |
| :--- | :--- | :--- |
| **Encoder Channel A** | Speed Feedback (Interrupt 0) | Digital Pin 2 |
| **Encoder Channel B** | Secondary Encoder Channel | Digital Pin 5 |
| **HC-SR04 TRIG** | Ultrasonic Trigger | Digital Pin 3 |
| **HC-SR04 ECHO** | Ultrasonic Echo | Digital Pin 4 |
| **L293D ENA** | Motor Speed (PWM) | Digital Pin 9 |
| **L293D IN1** | Motor Direction 1 | Digital Pin 10 |
| **L293D IN2** | Motor Direction 2 | Digital Pin 6 |

---

## System Control Strategy

1. **Closed-Loop Speed Regulation:** 
   Hardware interrupts on Pin 2 measure motor encoder pulses in 200 ms windows to compute `Actual RPM`. A proportional controller calculates speed error and updates the PWM signal (`ENA`) continuously to match `Target RPM`.

2. **Automated Proximity Adaptation:**
   An HC-SR04 sensor monitors item arrival along the transport track:
   - **Distance > 15 cm:** Standard transport velocity (**150.0 RPM**).
   - **Distance < 15 cm:** Automatic velocity reduction (**60.0 RPM**) for inspection/delicate handling.

---

## Verified Serial Telemetry Output

```text
Dist: 166.3 cm | Target RPM: 150.0 | Actual RPM: 154.2 | Error: -4.2 | Adjusted PWM: 109
Dist: 166.4 cm | Target RPM: 150.0 | Actual RPM: 153.5 | Error: -3.5 | Adjusted PWM: 109
