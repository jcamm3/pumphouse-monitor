# Pumphouse Monitor

Monitors water system pressure and temperature in pumphouse environments using dual analog pressure sensors and a digital temp/humidity sensor. Includes OLED display, RGB status LED, and web interface for real-time monitoring and calibration. Integrates with Home Assistant.

## Features

- Dual 100 PSI analog pressure transducers (SEN0257)
- Temperature-compensated pressure correction (auto/manual)
- OLED display cycling through multiple data views
- RGB LED status indicator (color-coded by pressure state)
- Web interface with grouped values and calibration controls
- Home Assistant integration via encrypted API
- OTA firmware updates via ESPHome

## Hardware

- ESP32-C3 (Espressif DevKitM-1)
- (2x) SEN0257 analog pressure sensors
- SHT30 temperature & humidity sensor
- SSD1306 128x64 OLED display (I2C)
- Neopixel RGB LED (WS2812 or compatible)

## Wiring

| Component               | ESP32-C3 Pin | Notes                |
|------------------------|--------------|----------------------|
| Pressure Sensor 1      | GPIO00       | ADC input            |
| Pressure Sensor 2      | GPIO04       | ADC input            |
| SHT30 Sensor (I2C)     | SDA/SCL      | I2C address: `0x44`  |
| OLED Display (I2C)     | SDA/SCL      | I2C address: `0x3C`  |
| RGB LED (Neopixel)     | GPIO08       | Single-pin data line |

> All components powered at 3.3V. SEN0257 accuracy may vary slightly due to suboptimal voltage.

## Getting Started

1. Flash the ESP32-C3 with `pumphouse.yaml` using ESPHome.
2. Update `!secret` values for Wi-Fi, API, and OTA credentials.
3. Save folers under .esphome directory to your local HA esphome directory.
4. Power the device and access its web interface at `http://<device-ip>`.
5. Use the web UI or Home Assistant to calibrate and monitor sensors.

## License

MIT License  
© 2025 John Camm
