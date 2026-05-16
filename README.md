# PerPetro XIAO — Voice Controlled Quadruped Robot

PerPetro XIAO is a compact quadruped robot powered by the Seeed Studio XIAO ESP32S3 Sense and ESP-Skainet speech recognition.
The robot responds to voice commands and performs multiple animated movements including walking, stretching, sitting, dancing, and posture transitions.

<img width="1310" height="1201" alt="robot" src="https://github.com/user-attachments/assets/77abca19-3e70-4f05-8071-66625f3b2e0b" />

---

# Features

* Voice-controlled quadruped robot
* ESP-Skainet speech recognition
* Fully wireless operation
* Compact and lightweight design
* Animated movement routines
* Custom 3D printed structure
* Open-source ESP-IDF firmware

---

# Wake Word & Voice Commands

The robot activates with the wake word:

```text id="h3njlwm"
JARVIS
```

After activation, say one of the supported commands clearly.

---

# Voice Recognition Recommendations

For the best recognition performance:

* Speak clearly and naturally
* Avoid loud environments
* Keep the microphone facing the speaker
* Pause briefly after saying the wake word
* Use simple English pronunciation
* Avoid speaking too fast

ESP-Skainet performs better with:

* strong consonants
* clearly separated syllables
* medium speaking speed

Commands with highly distinguishable phonetics are recognized more reliably.

---

# Supported Commands

| Command  | Phonetic (Skainet) | Action                     |
| -------- | ------------------ | -------------------------- |
| Good boy | GwD Bu             | Rear leg wag               |
| Sit down | SgT DtN            | Sit with weight shift      |
| Lie down | Li DtN             | Slow lie flat              |
| Stretch  | STRfp              | Front then rear stretch    |
| Walk     | WeK                | Forward movement           |
| Dance    | DaNS               | Full choreographed routine |

---

# Hardware

## Main Components

| Component       | Details                       |
| --------------- | ----------------------------- |
| Microcontroller | Seeed XIAO ESP32S3 Sense      |
| Servos          | 4x MG90S 180°                 |
| Battery         | 3.7V LiPo                     |
| Power Module    | 5V Boost + LiPo charger       |
| Leg Tips        | Rubber feet / electrical tape |

---

# Servo Connections

| Servo | Position    | XIAO GPIO   |
| ----- | ----------- | ----------- |
| FL    | Front Left  | D2 (GPIO 3) |
| FR    | Front Right | D3 (GPIO 4) |
| BL    | Back Left   | D4 (GPIO 5) |
| BR    | Back Right  | D5 (GPIO 6) |

All servo signal wires connect directly to the GPIO pins listed above.

IMPORTANT:

Servo power and GND must be connected to the external boost module, NOT directly to the XIAO ESP32S3.

---

# Mechanical Compatibility

IMPORTANT:

Before assembly, verify that all purchased electronic components are mechanically compatible with:

* the 3D printed parts
* screw dimensions
* mounting tolerances

Small dimensional differences between manufacturers may require minor adjustments.

---

# Screw List

| Item       | Quantity | Description                                         | Comment                                                        |
| ---------- | -------- | --------------------------------------------------- | -------------------------------------------------------------- |
| M2 x 6mm   | 6        | Attach lower and upper body, power switch, and ears | Can be longer, but not shorter                                 |
| M2 x 10mm  | 2        | Charge module mounting                              | Can be longer, but not shorter                                 |
| M2 x 4mm   | 8        | PCB and PCB base mounting                           | Exact size recommended                                         |
| M2 Nuts    | 4        | Used with M2 screws                                 | Used for switch, charge module, and optional extra ear support |
| M2.5 x 8mm | 1        | Servo arm screw                                     | Default screws are too short for the legs                      |

Recommendation:

Keeping a small assortment of M2 screws in:

* 3mm
* 4mm
* 5mm
* 6mm
* 8mm
* 10mm

is highly recommended during assembly and adjustment.

Note:

The lower screw of the charging module does not necessarily require a nut.

---

# Circuit Diagram

<img width="1661" height="947" alt="Circuit" src="https://github.com/user-attachments/assets/81a867fc-00f0-48e1-ac6b-921877af6a7b" />


---

# Documentation

Additional technical information can be found inside:

```text id="fjlwm2"
DOCUMENTATION/
```

Important files:

* `Requirements_List_PerPetro.xlsx`
* `Requirements_List_PerPetro.pdf`
* `TechnicalReportPerPetroXIAO.pdf`

These documents include:

* complete component lists
* electrical information
* assembly references
* design details
* technical explanations

---

# Assembly Recommendations

* Test all servos before assembly
* Verify servo center position before mounting legs
* Route cables before closing the body
* Use thread-safe screw pressure on printed parts
* Avoid overtightening screws
* Keep battery wires away from moving joints
* Test firmware before final assembly

---
# Additional Assembly Recommendation

Using a perforated PCB (perfboard) is highly recommended, as it can significantly simplify the internal wiring and overall assembly of the robot.

A perfboard allows you to:

* Create cleaner and more reliable electrical connections
* Mount the XIAO ESP32S3 more securely
* Add servo headers/connectors for easier servo installation and replacement
* Distribute power more efficiently between the boost module and servos
* Integrate the power switch directly into the main wiring layout
* Reduce loose cables inside the robot body
* Improve maintenance and future modifications

Recommended implementation:

* Use female headers for the XIAO ESP32S3
* Use 3-pin servo headers/connectors for each servo
* Create shared power rails for 5V and GND
* Use proper wire gauge for servo power distribution
* Add a connector between the power switch, boost module, battery, and servo power lines

IMPORTANT:

All electrical connections should always follow the provided circuit diagram and power distribution scheme.

Improper power routing may cause:

* unstable servo behavior
* ESP32 resets
* brownout issues
* electrical noise affecting voice recognition

Careful cable management and stable power connections greatly improve the robot’s reliability and overall performance.

---

# Firmware

The project uses:

* ESP-IDF v5.3.1
* ESP-Skainet
* ESP32-S3 speech recognition models

Voice commands can be modified through:

```bash id="fjlwm3"
idf.py menuconfig
```

---



# XIAO ESP32S3 Speech Commands Firmware Guide

## Requirements

Before starting, install the following:

### 1. Install ESP-IDF v5.3.1

Install:

* ESP-IDF v5.3.1
* ESP-IDF Tools Installer
* Python environment
* Xtensa toolchain

Official installer:

https://dl.espressif.com/dl/esp-idf/?idf=5.3.1

Recommended installation path:

```text
C:\Espressif
```

---

## 2. Required Hardware

* XIAO ESP32S3 / XIAO ESP32S3 Sense
* USB-C cable with DATA support
* Windows PC

IMPORTANT:

Some USB cables are power-only and will NOT work for flashing.

---

# Project Setup

Extract the project folder somewhere simple, for example:

```text
C:\Users\YourName\Downloads\en_speech_commands_recognition_F
```

---

# Open ESP-IDF PowerShell

Open:

```text
ESP-IDF 5.3 PowerShell
```

NOT regular PowerShell.

---

# Navigate to the Project

```powershell
cd "C:\Users\YourName\Downloads\en_speech_commands_recognition_F"
```

---

# Build the Firmware

Run:

```powershell
idf.py build
```

Expected result:

```text
Project build complete.
```

---

# Connect the ESP32S3

Connect the XIAO ESP32S3 using USB-C.

Check the COM port in Device Manager.

Example:

```text
COM11
```

---

# Flash the Firmware

Run:

```powershell
idf.py flash
```

Expected result:

```text
Hash of data verified.
Hard resetting via RTS pin...
Done
```

---

# Open Serial Monitor

Run:

```powershell
idf.py monitor
```

Expected output:

```text
TOP 1, command_id:
```

or:

```text
servo_Task received command:
```

---

# Exit Serial Monitor

Press:

```text
Ctrl + ]
```

---

# Flash + Monitor Together

Recommended command:

```powershell
idf.py flash monitor
```

This:

* flashes firmware
* reboots automatically
* opens serial monitor

---

# Changing Speech Commands

Run:

```powershell
idf.py menuconfig
```

Navigate to:

```text
ESP Speech Recognition
```

Then:

```text
Speech Commands
```

or:

```text
Multinet
```

Then edit:

```text
Add English speech commands
```

After saving:

```powershell
idf.py build
idf.py flash
```

---

# Common Errors and Solutions

---

# ERROR — "waiting for download"

Example:

```text
boot:0x23 (DOWNLOAD(USB/UART0))
waiting for download
```

## Cause

The ESP32 entered bootloader/download mode instead of running firmware.

## Solution

### Method 1

1. Disconnect USB
2. Hold BOOT button
3. Connect USB
4. Wait 2 seconds
5. Release BOOT
6. Press RESET once

Then run:

```powershell
idf.py monitor
```

---

### Method 2

Run:

```powershell
idf.py flash monitor
```

This usually forces a correct reboot.

---

### Method 3

Check GPIO0 connections.

IMPORTANT:

If GPIO0 is connected to GND during boot, the ESP32 ALWAYS enters download mode.

Disconnect anything connected to GPIO0.

---

# ERROR — Device Not Found

Example:

```text
Failed to connect to ESP32
```

## Solutions

### Check USB Cable

Use a DATA USB cable.

---

### Check COM Port

List serial ports:

```powershell
mode
```

or check Device Manager.

---

### Specify COM Port Manually

Example:

```powershell
idf.py -p COM11 flash
```

---

# ERROR — Permission Denied / Port Busy

Example:

```text
Access denied
Port is busy
```

## Solution

Close:

* Arduino IDE Serial Monitor
* VS Code Serial Monitor
* Putty
* Other terminal programs

Then retry.

---

# ERROR — Build Failed

Example:

```text
ninja failed
```

## Solutions

Clean build files:

```powershell
idf.py fullclean
```

Then rebuild:

```powershell
idf.py build
```

---

# ERROR — Python Environment Problems

Example:

```text
Python was not found
```

## Solution

Always use:

```text
ESP-IDF PowerShell
```

NOT normal PowerShell.

---

# Recommended Workflow

```powershell
idf.py build
idf.py flash monitor
```

This is the easiest and most reliable workflow.

---

# Notes

* First boot may take several seconds.
* Speech recognition works best in quiet environments.
* Use simple English commands.
* Avoid very short or difficult-to-pronounce words.
* Keep microphone close during testing.
---

# Final Recommendation

Do not rush the process or expect everything to work perfectly in a single day. Robotics, embedded systems, electronics, and firmware development require patience, iteration, and continuous learning.

Mistakes, redesigns, debugging sessions, and unexpected problems are all part of the engineering process.

If you truly want to grow in this field:

* take your time understanding each subsystem
* experiment with different solutions
* learn from failures instead of avoiding them
* focus on consistency rather than speed

Every small improvement builds real experience.

The goal is not only to finish the robot, but to understand how and why it works.

---
# License

This project is released under the MIT License.

Feel free to use, modify, and distribute the project with proper attribution.


