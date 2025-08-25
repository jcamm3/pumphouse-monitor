# Pumphouse Monitor — Changelog

## v1.2.0 — 2025-08-25
**Improved signal quality and clarified 5V offset handling**
- Documented the 5V ratiometric sensor behavior (0.5–4.5V) and the divider mapping to ~0.33–2.97V at the ADC.
- Recommended smoothing chain: `median` → `exponential_moving_average` → small `sliding_window_moving_average`, plus `throttle` to Home Assistant.
- Optional anti-spike guard pattern for rejecting single-frame transients.
- Updated header to reflect v1.2.0 with concise specs and wiring notes.

## v1.1.0 — 2025-06-12
- Added user-configurable **LED Night Mode** (22:00–06:30) and web UI control.

## v1.0.0 — 2025-06-06
- Initial release: dual pressure sensors, SHT30 temp/humidity, SSD1306 OLED UI, RGB status LED, SNTP time, and web UI.
