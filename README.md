# smart-traffic-noise-management-system
An Arduino-based noise monitoring system with Telegram Bot integration. Detects high noise levels via sound sensor, triggers LED alerts, and sends real-time notifications. Simulated on Tinkercad with Python bridge for Telegram API.

Simulation Link:https://www.tinkercad.com/things/9Iu8duOomXU-spectacular-habbi-bruticus/editel?returnTo=https%3A%2F%2Fwww.tinkercad.com%2Fdashboard

Noise Level Alert with Telegram Notifications

This project demonstrates a noise monitoring traffic light system using Arduino.
The system continuously monitors the ambient noise level through an analog input (sound sensor or potentiometer in simulation). If the noise exceeds a predefined threshold, the traffic light switches to Red and a Telegram notification is sent to the user. Once the noise level returns to normal, another notification is sent indicating recovery.

Features

Real-time noise detection using analog input.

Traffic light simulation (Red, Yellow, Green) with LEDs.
High noise alert sent to Telegram: "⚠️ Noise too high!".
Normal condition update sent to Telegram: "✅ Level normal. Holding red for 2 sec...".

Works in:
Tinkercad with Arduino Uno + Python bridge script.

Overview

The Arduino reads input from a sound sensor (or potentiometer in simulation).
If noise exceeds the threshold, the Red LED activates and a Telegram alert is sent:
"⚠️ Noise too high!"
When noise returns to normal, the system holds Red for 2 seconds, then restores normal operation while sending:
"✅ Level normal. Holding red for 2 sec...".
Cross-Platform Simulation:

Tinkercad + Python Bridge: Arduino Uno sends Serial data to a Python script, which communicates with Telegram.
Technology Stack
Arduino Uno 
Tinkercad 
Python (pyserial, requests) for Serial-to-Telegram bridge
Telegram Bot API for notifications

Applications

Monitoring classroom or library noise levels
Industrial noise compliance systems
Smart city traffic management (noise-sensitive zones)

This project provides a simple yet effective prototype for IoT-based noise monitoring, combining embedded hardware simulation with cloud messaging.



