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

##Code

#define PWMA 5
#define PWMB 6
#define AIN1 7
#define AIN2 8
#define BIN1 9
#define BIN2 10
#define STBY 4

int sensorPins[8] = {A0,A1,A2,A3,A4,A5,A6,A7};
int sensorValues[8];

float Kp = 18;
float Ki = 0;
float Kd = 12;

int baseSpeed = 150;

float error = 0;
float previousError = 0;
float integral = 0;
float derivative = 0;
float correction = 0;

void setup()
{
pinMode(PWMA,OUTPUT);
pinMode(PWMB,OUTPUT);
pinMode(AIN1,OUTPUT);
pinMode(AIN2,OUTPUT);
pinMode(BIN1,OUTPUT);
pinMode(BIN2,OUTPUT);
pinMode(STBY,OUTPUT);

digitalWrite(STBY,HIGH);
}

void loop()
{
long weightedSum = 0;
long total = 0;

for(int i=0;i<8;i++)
{
sensorValues[i] = analogRead(sensorPins[i]);
int value = 1023 - sensorValues[i];
weightedSum += (long)value * (i*1000);
total += value;
}

if(total != 0)
{
error = (weightedSum/total) - 3500;
}

integral += error;
derivative = error - previousError;

correction = Kp*error + Ki*integral + Kd*derivative;

int leftSpeed = baseSpeed + correction;
int rightSpeed = baseSpeed - correction;

leftSpeed = constrain(leftSpeed,0,255);
rightSpeed = constrain(rightSpeed,0,255);

digitalWrite(AIN1,HIGH);
digitalWrite(AIN2,LOW);
analogWrite(PWMA,leftSpeed);

digitalWrite(BIN1,HIGH);
digitalWrite(BIN2,LOW);
analogWrite(PWMB,rightSpeed);

previousError = error;
}

## Future Improvements

- Bluetooth PID tuning
- Faster sensor reading
- Encoders for speed control
