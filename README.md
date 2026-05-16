# Perpetro-Xiao


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
