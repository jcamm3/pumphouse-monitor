# Wiring Guide

## ESP32-C3 Pinout Connections

| Component               | Pin       | Notes                  |
|------------------------|-----------|-------------------------|
| Pressure Sensor 1      | GPIO00    | ADC input               |
| Pressure Sensor 2      | GPIO04    | ADC input               |
| SHT30 Sensor           | I2C (0x44)| SDA/SCL default         |
| OLED Display (SSD1306) | I2C (0x3C)| 128x64 display          |
| Neopixel RGB LED       | GPIO08    | 5V safe                 |

## Power
- 3.3V for ESP32 and sensors
- If sensors were designed for 5V (e.g., SEN0257), accuracy may be impacted
