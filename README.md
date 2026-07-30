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
  - Line sensors (IR reflectance array or camera)
  - Proximity sensors (HC-SR04 ultrasonic or LiDAR)
  - Optional: encoders for odometry, RFID/QR reader for location IDs
- Actuators:
  - DC motors with motor driver (H-bridge) or geared motors
  - Servo for gripper/pusher mechanism
- Compute:
  - Microcontroller (Arduino Uno/Nano/Mega) for low-level control
  - Single-board computer (Raspberry Pi / Jetson Nano) for vision/ROS
- Communication:
  - Serial, I2C, SPI, or wireless (Wi-Fi / MQTT / ROS)

---
