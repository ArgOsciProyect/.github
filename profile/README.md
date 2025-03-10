# ARG_OSCI User Manual

## Introduction

ARG_OSCI is an open-source oscilloscope project that transforms an ESP32 microcontroller into a digital signal acquisition device. The complete system consists of:

1. **ESP32 Firmware** - Software that enables the ESP32 to acquire analog signals and transmit them wirelessly
2. **Desktop/Mobile Application** - Interface for visualizing and analyzing the acquired signals
3. **Optional Hardware Add-ons** - External ADC connections and signal conditioning circuits

This manual covers the setup, operation, and maintenance of the ARG_OSCI system, focusing on practical usage scenarios and technical specifications.

## 1. Installing the Firmware

### 1.1 Requirements

Before installing the ARG_OSCI firmware, ensure you have:

- ESP32 development board
- Micro USB cable
- Computer with Internet connection
- [Optional] External ADC module for higher sampling rates

### 1.2 Installing the Firmware Installer

The ARG_OSCI firmware can be installed using our dedicated installer application which handles downloading the ESP-IDF framework, building the firmware, and flashing the ESP32.

#### Windows Installation

1. Download the latest Windows installer package from the [official releases page](https://github.com/ArgOsciProyect/ARG_OSCI_FIRMWARE/releases)
2. Extract the ZIP file to a folder of your choice
3. Run the `ARG_OSCI_Installer.exe` application

**Note**: Windows SmartScreen may show a warning. This is normal for applications without a digital signature. Click "More information" and then "Run anyway".

#### Linux Installation

1. Download the latest Linux installer package from the [official releases page](https://github.com/ArgOsciProyect/ARG_OSCI_FIRMWARE/releases)
2. Extract the ZIP file to a directory of your choice
3. Open a terminal in the extracted directory
4. Run the helper script:
   ```bash
   ./run.sh
   ```

**Note**: The installation script for Linux may need to install additional dependencies. You will be prompted for confirmation before the installation of packages. 

![image](https://github.com/user-attachments/assets/a0e177c6-e949-4ba6-bc0b-f6b371ee78da)

![image](https://github.com/user-attachments/assets/fcff183f-951f-462f-9187-cb51d1c78cbb)

### 1.3 Firmware Installation Procedure

The installer will guide you through the following steps:

#### Step 1: Configuration

1. Connect your ESP32 to your computer via USB
2. Set WiFi credentials:
   - SSID: Name for the ESP32's WiFi network
   - Password: Password for the WiFi network
3. Select hardware configuration:
   - Internal ADC: Uses the ESP32's built-in ADC (up to 600 kHz sampling)
   - External ADC: Requires external ADC hardware connected via SPI (up to 2.5 MHz sampling) (See hardware section for more details)
4. Select the appropriate serial port where your ESP32 is connected

![image](https://github.com/user-attachments/assets/caf92bdb-cc20-47d6-af50-c39f27161ab1)
![image](https://github.com/user-attachments/assets/bba3f29c-708b-4ff0-85be-f29c17240a43)

![image](https://github.com/user-attachments/assets/71ecd945-44c0-4020-8cf3-1fb1e62c1517)
![image](https://github.com/user-attachments/assets/76075e8a-1fd0-4102-bee8-c19d8aac4945)

#### Step 2: Installation Paths

The installer needs several directories for its components:

1. Firmware Path: Where the ARG_OSCI firmware source code will be stored
2. ESP-IDF Path: Where the ESP-IDF framework will be installed
3. ESP-IDF Tools Path: Where the compilation tools will be installed

The default locations should work for most users. If you already have ESP-IDF installed, you can use the "Find Existing ESP-IDF" button to locate your existing installation.

![image](https://github.com/user-attachments/assets/a68539c8-3a49-4343-8b97-81116c3c7fc5)

#### Step 3: Installation Process

Click the "Install" button to start the installation process. The installer will:

1. Download the ARG_OSCI firmware source code
2. Download and configure ESP-IDF (if not already installed)
3. Build the firmware with your selected configuration
4. Flash the firmware to your ESP32

This process may take 15-30 minutes depending on your internet connection and computer performance.

![image](https://github.com/user-attachments/assets/2b3a5958-8b96-416d-be2e-77d48699a81a)

### 1.4 Verifying the Installation

After successful installation:

1. The ESP32 will create a WiFi access point with the SSID you configured
2. The blue LED on the ESP32 should be lit
3. You can now connect to this WiFi network from the ARG_OSCI application

If you encounter errors during installation:

1. Check that your ESP32 is properly connected and recognized by your computer
2. Ensure you have sufficient disk space (at least 2GB required)
3. Verify that your user account has permission to access the selected serial port
4. On Linux systems, you may need to add your user to the "dialout" group

### 1.5 Firmware Update

To update the firmware to a newer version:

1. Run the installer again
2. Configure the same settings as before
3. Click "Install" to download and flash the latest firmware

If you only want to change configuration settings without downloading everything again, use the "Configure & Flash" button instead of "Install".
