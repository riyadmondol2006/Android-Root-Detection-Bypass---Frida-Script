# Android Root Detection Bypass - Frida Script

This repository contains a powerful Frida script designed to bypass root detection mechanisms in Android applications. By intercepting both native and Java-based checks, this script effectively hides the presence of root, enabling smooth testing and debugging on rooted devices.

## Features

- **Native Function Interception:** Blocks file access checks (`fopen`, `access`, `stat`, `lstat`) for root-related files and paths.
- **Java Method Overrides:** Hooks into Java methods (`File.exists`, `File.length`) to prevent root detection at the application layer.
- **System Property Manipulation:** Spoofs system properties (`ro.secure`, `ro.debuggable`, etc.) to simulate a non-rooted environment.
- **Package Detection Evasion:** Masks root-related applications like Magisk or SuperSU by overriding package manager queries.
- **Command Blocking:** Prevents execution of shell commands (`su`, `magisk`, etc.) commonly used to check root access.
- **Comprehensive Root Indicators:** Includes an extensive list of paths, packages, and commands related to root detection.

## How to Use

### Prerequisites

1. Install **Frida** on your system. Follow the [Frida Installation Guide](https://frida.re/docs/installation/) for details.
2. Deploy the Frida server on your Android device:
   - Download the appropriate Frida server binary from [Frida Releases](https://github.com/frida/frida/releases).
   - Push the binary to your device and grant execute permissions:
     ```bash
     adb push frida-server /data/local/tmp/
     adb shell "chmod +x /data/local/tmp/frida-server"
     ```
   - Start the Frida server:
     ```bash
     adb shell "/data/local/tmp/frida-server &"
     ```

### Script Injection

1. Load the script into the target application using Frida:
   ```bash
   frida -U -f com.example.targetapp -l root.js --no-pause
