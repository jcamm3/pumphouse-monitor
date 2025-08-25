# Pumphouse Monitor (ESPHome) — v1.2.0

An ESP32-C3 based pumphouse monitor with dual ratiometric pressure sensors (5V, 0.5–4.5V via divider), SHT30 temp/humidity, SSD1306 OLED pages, status LED with night mode, SNTP, and a built-in web UI for calibration and runtime controls.

## Highlights
- **Accurate 5V ratiometric pressure handling** — 0 PSI at **0.5V** (→ ~**0.33V** at ADC with divider), full-scale at **4.5V** (→ ~**2.97V** at ADC).
- **Smoother pressure readings** — median + EMA + small sliding window; throttle updates to HA to reduce chatter.
- **OLED UI** with multi-page layout for time, temperature, humidity, and pressure.
- **Night Mode** for the onboard NeoPixel to keep things dark between set hours.
- **Web UI** groups for calibration, thresholds, and system info.

## Hardware
- **Board:** ESP32-C3 DevKitM-1
- **Pressure sensors:** SEN0257-class, powered at 5V, analog output 0.5–4.5V
- **Divider:** scale sensor output to ESP32 ADC range (e.g., 100k/68k); ADC sees ~0.33–2.97V
- **I²C:** SHT30 + SSD1306 OLED
- **LED:** Onboard NeoPixel (GPIO8)

### Pin Map
| GPIO | Function                    |
|-----:|-----------------------------|
|   0  | Pressure Sensor 1 (ADC)     |
|   1  | Pressure Sensor 2 (ADC)     |
|   2  | I²C SDA (OLED, SHT30)       |
|   3  | I²C SCL (OLED, SHT30)       |
|   8  | Onboard NeoPixel            |

## Calibration — Offset & Scale
- Set **offset_volts** so that *at true 0 PSI*, your **Sensor Volts (Raw)** equals the offset (typically ~**0.33V** with a 5V sensor + divider).
- Pressure (kPa) equivalent constant remains `606.0606` for a 1.6 MPa transducer (0.33–2.97V span at the ADC).
- Fine-tune against a known gauge point by nudging the offset a few hundredths of a volt.

## Smoothing Tunables
A practical chain that balances stability and responsiveness:
- `median` (window 7–11)
- `exponential_moving_average` (`alpha` 0.20–0.35)
- `sliding_window_moving_average` (window 6–10)
- `throttle: 1s` on derived kPa/psi sensors

Optional: add an anti-spike guard lambda to drop single-frame jumps (e.g., `>5 psi`).

## Web UI
Sorting groups are used to keep config/settings vs. live values organized. Tune thresholds, night mode, and calibration live.

## Getting Started
1. Review the pin map and resistor divider.
2. Flash via ESPHome; connect to Wi‑Fi and open the web UI.
3. Set **offset_volts** at 0 PSI; verify psi/kPa vs. your mechanical gauge.
4. Adjust smoothing parameters if needed.

---

**Version:** v1.2.0  

**Last Updated:** 2025-08-25  

**Author:** John Camm
