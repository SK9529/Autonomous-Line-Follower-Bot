# Autonomous-Line-Follower
Developed an autonomous line-following robot for warehouse inventory management using sensor-based navigation and real-time path tracking.The system combines reliable line-following control, obstacle avoidance, and a lightweight inventory-management interface to streamline material handling in small to medium-sized storage environments.

Status: Prototype
Platform: Arduino IDE
Use case: repetitive transfer of small inventory items, route verification, stock-taking assistance

## Features

- Line detection using reflectance (IR) sensors or camera-based detection
- Obstacle detection and avoidance (ultrasonic)
- Simple inventory task handling (pickup/drop via servo or small actuator)
- Configurable routes via RFID markers
- Modular software layers (sensor drivers, control, navigation)

---

## Applications

- Transporting small goods between stations
- Routine aisle scanning for inventory checks
- Parcel sorting in small warehouses
---

## System Overview

- Sensors:
  - Line sensors (IR reflectance array)
  - Proximity sensors (HC-SR04 ultrasonic )
- Actuators:
  - DC motors with motor driver (H-bridge) or geared motors
  - Servo for gripper/pusher mechanism
- Compute:
  - Microcontroller (Arduino Uno/Nano/Mega) for low-level control
  - Single-board computer (Raspberry Pi / Jetson Nano) for vision/ROS
- Communication:
  - Serial, I2C wireless (Wi-Fi)

---

## Calibration & Tuning

1. Line sensor thresholds:
   - Records raw ADC values on white vs black surfaces.
   - Sets threshold to midpoint or implement adaptive thresholding.
2. PID tuning (suggested method):
   - Start with Ki = 0, Kd = 0
   - Increase Kp until oscillation, back off ~30%
   - Kd to reduce overshoot
   - Small Ki only if steady-state error persists
3. Motor PWM limits:
   - Determine minimum PWM that starts the motor and max safe PWM for your battery.

---

## Algorithms & Architecture

- Line Detection:
  - IR array: compute weighted error from sensor readings to get lateral offset
  - Camera: use color thresholding + Hough/contour to estimate line center
- Control:
  - Classic PID on error to compute steering correction; map steering to motor speed differential
- Obstacle Avoidance:
  - If obstacle within threshold distance, stop and reroute or wait until clear
- High-level:
  - Finite-state machine
  - (IDLE → FOLLOW_LINE → AVOID_OBSTACLE → EXECUTE_TASK → IDLE)

---

## Testing & Validation

- Tests for sensor readings (mocked or hardware-in-loop)
- Track tests: measure deviation over repeated runs, plot error vs time
- Battery & thermal tests: verify operation time and motor/driver temperatures
- Edge cases: broken line, intersection handling, low-light conditions

---

## Troubleshooting

- Robot doesn't move:
  - Check motor power supply and motor driver enable pins
  - Verify PWM signals from the controller
- Poor line detection:
  - Clean sensors, adjust height and angle, recalibrate thresholds
  - Improve contrast of the line (use matte tape)
- Oscillation or jitter:
  - Reduce Kp, increase Kd, verify encoder feedback
- RF/serial dropouts:
  - Add error handling and reconnection logic; use hardware flow control if available
