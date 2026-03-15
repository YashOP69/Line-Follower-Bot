# Line-Follower-Bot
A PID-based line follower robot built using Arduino Nano, TB6612FNG motor driver, and an 8-channel line sensor array.

# PID Line Follower Robot

This project is a two-wheel differential drive line follower robot using PID control.

## Hardware

- Arduino Nano
- TB6612FNG Motor Driver
- SmartElex RLS-08 Line Sensor Array
- N20 600RPM Gear Motors
- 3S LiPo Battery
- LM2596 Buck Converter

## Features

- 8-sensor line detection
- PID control for smooth tracking
- Adjustable speed and PID constants

## Wiring

Motor Driver:
PWMA → D5
AIN1 → D7
AIN2 → D8
PWMB → D6
BIN1 → D9
BIN2 → D10
STBY → D4

Sensors:
A0–A7 → Arduino A0–A7

- Bluetooth PID tuning
- Faster sensor reading
- Encoders for speed control
