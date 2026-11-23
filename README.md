# IoT Smart Home Model

A university team project that demonstrates a small-scale smart home prototype built around an ESP32-compatible controller, sensors, servo motors, an RFID reader, and an LCD. The project combines a physical house model with Arduino-style firmware to demonstrate several basic home-automation and safety-related functions.

> This is an educational prototype developed as a team project. It is not a production-ready home security or fire-safety system.

## Project Demonstration

Watch the physical smart home model operating in the demonstration video:

**[▶ Watch the Smart Home Demo on Google Drive](https://drive.google.com/file/d/1qrlLFOlSptk7ZshPRZl_YtcvdfTCL_Vh/view?usp=sharing)**

The video is hosted on Google Drive rather than stored in this repository because the recording is approximately 301 MB. The Drive owner must set General access to **Anyone with the link – Viewer** for people outside the owner's account to watch it.

## Project Overview

The prototype brings together the following functions, as described in the submitted firmware and team progress report:

- **RFID door access:** checks a scanned card UID against two configured UIDs and toggles a servo-operated door between two positions.
- **Temperature and humidity monitoring:** reads a DHT11 sensor and displays temperature and humidity on a 16×2 I2C LCD.
- **Rain response:** detects a change in the rain-sensor state and moves two servo motors to represent closing or opening the window-related mechanisms.
- **Flame alert:** reads a digital flame-sensor signal and drives a buzzer alarm when the configured flame-detected state is observed.
- **Light-sensor and LED control:** reads a digital light-sensor input and switches an LED when the input state changes.

The physical model is shown in [`assets/smart-home-model.png`](assets/smart-home-model.png).

## Hardware and Libraries

| Component / library | Role in the prototype |
|---|---|
| ESP32-compatible board | Main microcontroller |
| MFRC522 RFID reader | Reads RFID cards for door access |
| Servo motors | Operate the door and rain-responsive mechanisms |
| DHT11 | Measures temperature and humidity |
| I2C LCD | Displays sensor readings |
| Rain sensor | Detects rain state |
| Flame sensor | Provides a digital flame-detection signal |
| Buzzer | Provides an audible alert |
| Light sensor and LED | Demonstrates sensor-triggered lighting |
| `SPI`, `MFRC522`, `ESP32Servo`, `DHT`, `LiquidCrystal_I2C` | Libraries referenced by the firmware |

The sketch also includes `WiFi.h`, but the submitted version does not implement a Wi-Fi connection or network-control feature. The project should therefore be understood as a locally controlled prototype, not a connected smart-home application.

## Repository Structure

```text
iot-smart-home-model/
├── assets/
│   └── smart-home-model.png
├── docs/
│   └── smart-home-project-report.docx
├── firmware/
│   └── smart_home_controller/
│       └── smart_home_controller.ino
├── videos/
│   └── README.md
├── .gitignore
└── README.md
```

## Getting Started

1. Install the Arduino IDE.
2. Select the ESP32 board variant that matches the hardware used in the prototype.
3. Install the libraries referenced in the sketch: `MFRC522`, `ESP32Servo`, `DHT sensor library`, and `LiquidCrystal_I2C`. The `SPI` and `WiFi` libraries are provided by the ESP32/Arduino platform package.
4. Open [`firmware/smart_home_controller/smart_home_controller.ino`](firmware/smart_home_controller/smart_home_controller.ino).
5. Check every pin definition against the actual board and wiring. Pin assignments are specific to the team's prototype and may not match other ESP32 boards.
6. Replace the placeholder RFID UID values in `authorizedUID1` and `authorizedUID2` with test-card UIDs for your own setup. Do not commit personal or production access credentials.
7. Verify and upload the sketch to the board.
8. Open the Serial Monitor at **115200 baud** to view status messages.

The source is provided as a single Arduino sketch. Hardware behavior depends on the exact ESP32 board, sensor modules, servo wiring, power supply, and library versions.

## Team

This is a group project. The progress report lists the following members:

- Phan Lê Quốc Ngọc
- Đỗ Minh Phú
- Nguyễn Đình Hoàng Bách

Please coordinate with the other members before making the repository public. The original team report contains student identification numbers; consider keeping the repository Private or replacing the report with a redacted version before public release.

## AI Assistance

ChatGPT/GPT was used as a supporting tool during parts of the learning and documentation process. It helped clarify selected technical concepts, discuss code-related questions, and organize the project documentation. The physical prototype, group work, and submitted firmware are the team's project; AI assistance is disclosed here rather than presenting the work as either fully AI-generated or completed without assistance.

## Known Limitations and Safety Notes

- The firmware is an educational prototype and must not be relied on for real door security, fire detection, or life-safety protection.
- RFID UID matching is suitable only for a basic demonstration. A card UID alone is not strong authentication for a real access-control system.
- The two RFID UIDs in this repository copy are placeholders (`0x00`). Configure test-card UIDs locally; do not publish real access credentials.
- The team progress report notes occasional flame-sensor response delays caused by a loose wire connection during testing. Check the wiring and re-test the sensor before demonstrations.
- The light-control class reads a light-sensor input, although some Serial messages refer to motion. The submitted code does not show a dedicated PIR motion sensor.
- `previousMillis` and `interval` are declared but are not used in the current `loop()`. Some processing methods use `delay()`, so the firmware is not fully non-blocking.
- The buzzer pin value in the report's embedded code snapshot differs from the value in the supplied `.ino` source. Use the actual tested wiring and verify the pin mapping before powering the circuit.
- The physical photo and report document the prototype and its progress; they do not independently certify that every component will operate reliably in every setup.

## Project Report

See [`docs/smart-home-project-report.docx`](docs/smart-home-project-report.docx) for the team's progress report, implementation notes, hardware references, and firmware excerpts.
