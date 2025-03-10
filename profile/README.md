# ARG_OSCI User Manual

## Introduction

ARG_OSCI is an open-source oscilloscope project that transforms an ESP32 microcontroller into a digital signal acquisition device. The complete system consists of:

1. **ESP32 Firmware** - Software that enables the ESP32 to acquire analog signals and transmit them wirelessly
2. **Desktop/Mobile Application** - Interface for visualizing and analyzing the acquired signals
3. **Hardware Add-ons** - Signal conditioning circuits and optional external ADC for higher sampling frequency

This manual covers the setup, operation, and maintenance of the ARG_OSCI system.

## 1. Installing the Firmware

### 1.1 Requirements

Before installing the ARG_OSCI firmware, ensure you have:

- ESP32 development board
- Micro USB cable
- Computer with Internet connection

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

![image](https://github.com/user-attachments/assets/8ba4c352-2ec9-4a2a-8371-be57e5e5a09a)

![image](https://github.com/user-attachments/assets/6423c2d7-1d26-4147-a150-b7970a1e7b9d)

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
4. On Linux systems, you may need to add your user to the "dialout" group:
   ```bash
   sudo usermod -a -G dialout $USER
   ```
   After running this command, you'll need to log out and log back in for the changes to take effect.
   If you still have problems accessing the port, try:
   ```bash
   sudo chmod 666 /dev/ttyUSB0
   ```
   (Replace ttyUSB0 with your actual port name)

### 1.5 Firmware Update

To update the firmware to a newer version:

1. Run the installer again
2. Configure the same settings as before
3. Click "Install" to download and flash the latest firmware

If you only want to change configuration settings without downloading everything again, use the "Configure & Flash" button instead of "Install".

# 2. App Software Installation & Usage

## 2.1 Requirements

Before installing the ARG_OSCI application, ensure you have:

- A device running one of the supported operating systems:
  - Windows
  - Linux
  - Android
- ESP32 with ARG_OSCI firmware installed (see Section 1)
- Stable internet connection (for installation only)

## 2.2 Installing the Application

### 2.2.1 Windows Installation

1. Download the latest Windows package from the [official releases page](https://github.com/ArgOsciProyect/ARG_OSCI_APP/releases)
2. Extract the `windows-release.zip` file to a folder of your choice
3. Run the `arg_osci_app.exe` executable

**Note**: Windows SmartScreen may show a warning. This is normal for applications without a digital signature. Click "More information" and then "Run anyway".

<!-- IMAGE: Screenshot of Windows SmartScreen warning dialog with "More info" option highlighted -->

### 2.2.2 Linux Installation

Three installation methods are available for Linux:

#### AppImage (Recommended)

1. Download the `.AppImage` file from the [official releases page](https://github.com/ArgOsciProyect/ARG_OSCI_APP/releases)
2. Make the file executable:
   ```bash
   chmod +x arg-osci-*.AppImage
   ```
3. Run the AppImage:
   ```bash
   ./arg-osci-*.AppImage
   ```

#### Debian/Ubuntu (.deb)

1. Download the `.deb` package from the [official releases page](https://github.com/ArgOsciProyect/ARG_OSCI_APP/releases)
2. Install with:
   ```bash
   sudo dpkg -i arg-osci-*.deb
   ```
   or
   ```bash
   sudo apt install ./arg-osci-*.deb
   ```
3. Launch from your applications menu or run `arg-osci` in terminal

#### RPM-based Distributions (Fedora, RHEL, etc.)

1. Download the `.rpm` package from the [official releases page](https://github.com/ArgOsciProyect/ARG_OSCI_APP/releases)
2. Install with:
   ```bash
   sudo rpm -i arg-osci-*.rpm
   ```
   or
   ```bash
   sudo dnf install ./arg-osci-*.rpm
   ```
3. Launch from your applications menu or run `arg-osci` in terminal

### 2.2.3 Android Installation

1. Download the `.apk` file from the [official releases page](https://github.com/ArgOsciProyect/ARG_OSCI_APP/releases)
2. Enable "Install from Unknown Sources" in your device settings if not already enabled
   - Navigate to Settings > Security > Install Unknown Apps
   - Select the browser or file manager you'll use to open the APK
   - Toggle "Allow from this source"
3. Open the downloaded APK file and follow the installation prompts
4. Once installed, open the ARG_OSCI app from your app drawer

<!-- IMAGE: Screenshot showing Android "Install unknown apps" settings screen -->

## 2.3 Initial Connection Setup

When you first launch the ARG_OSCI app, you'll need to establish a connection with your ESP32 device.

### 2.3.1 AP Mode Selection

1. On the initial setup screen, tap the "Select AP Mode" button

<!-- IMAGE: Screenshot of the app's initial screen with "Select AP Mode" button -->

2. The app will attempt to connect to the ESP32's access point
3. Once connected, you'll be presented with two options:
   - **Local AP**: Use the ESP32's own WiFi network (recommended for direct connections)
   - **External AP**: Connect the ESP32 to your existing WiFi network (recommended for long-term usage)

<!-- IMAGE: Screenshot of the AP Mode selection dialog showing both options -->

### 2.3.2 Local AP Mode

If you selected "Local AP":

1. The app will maintain connection to the ESP32's WiFi network
2. You'll be taken directly to the Mode Selection screen
3. Your device will remain connected to the ESP32 WiFi network while using the app

**Note**: In this mode, your device won't have internet access while connected to the ESP32.

### 2.3.3 External AP Mode

If you selected "External AP":

1. The app will scan for available WiFi networks
2. Select your home/office WiFi network from the list

<!-- IMAGE: Screenshot of WiFi network scanning/selection dialog -->

3. Enter the password for the selected network

<!-- IMAGE: Screenshot of WiFi password entry dialog -->

4. The app will configure the ESP32 to connect to your WiFi network
5. Your mobile device will automatically switch to the same WiFi network
6. Once connected, you'll be taken to the Mode Selection screen

**Note**: If the connection fails, you'll see error options to retry or exit. Ensure your WiFi credentials are correct and the network is accessible.

## 2.4 Common Signal Processing Settings

### 2.4.1 Sampling Frequency

The sampling frequency determines the rate at which the ESP32 captures signals and directly affects both visualization modes:

- The maximum frequency that can be correctly visualized is half the sampling frequency (Nyquist theorem)
- The sampling frequency is set in the ESP32 firmware
- The application automatically adapts to the configured sampling frequency

The current sampling frequency is displayed in the information panel and affects both the oscilloscope's time resolution and the maximum detectable frequency in the spectrum analyzer.

<!-- IMAGE: Screenshot showing the sampling frequency display in the information panel -->

### 2.4.2 Voltage Scale

Select the appropriate voltage scale based on your input signal:

- Available ranges: ±400V, ±2V, ±1V, ±500mV, ±200mV, ±100mV
- Smaller voltage ranges provide higher resolution for low-voltage signals
- Ensure your signal doesn't exceed the selected range to avoid clipping

<!-- IMAGE: Screenshot of voltage scale dropdown with options visible -->

### 2.4.3 Trigger Settings

Triggers determine when the oscilloscope begins a trace, helping to stabilize repetitive waveforms:

- **Trigger Level**: The voltage level at which the trigger activates
  - Adjust using the slider or enter a specific value
- **Trigger Edge**: Choose between:
  - **Positive**: Triggers when signal crosses trigger level from low to high
  - **Negative**: Triggers when signal crosses trigger level from high to low
- **Trigger Mode**:
  - **Normal**: Continuously captures data when trigger conditions are met
  - **Single**: Captures a single trace when trigger conditions are met, then pauses

<!-- IMAGE: Screenshot of trigger settings section with labels -->

### 2.4.4 Filter Settings

Filters can help clean up noisy signals in both visualization modes:

- **Filter Type**:
  - **None**: No filtering applied
  - **Moving Average**: Smooths the signal by averaging nearby samples
  - **Exponential**: Applies exponential smoothing
  - **Low Pass**: Removes high-frequency components
- **Filter Parameters** (vary by filter type):
  - Window Size: Number of samples to consider for averaging
  - Alpha: Smoothing factor for exponential filter
  - Cutoff Frequency: Threshold frequency for low-pass filter

<!-- IMAGE: Screenshot of filter settings section -->

### 2.4.5 Advanced Controls

- **Double Filtering**: When enabled, applies the filter twice for stronger smoothing
- **Hysteresis**: Prevents multiple triggers from noise around the trigger level

## 2.5 Using the Oscilloscope Mode

### 2.5.1 Understanding the Interface

The Oscilloscope mode interface consists of:

<!-- IMAGE: Labeled screenshot of Oscilloscope interface with main components marked -->

1. **Main chart area**: Displays the waveform
2. **Control panel**: Contains playback and view controls
3. **Information bar**: Shows frequency and other measurements

### 2.5.2 Basic Controls

- **Play/Pause**: Controls whether the display updates with new data
- **Zoom controls**: Adjust the time scale (X-axis) and voltage scale (Y-axis)
- **Pan controls**: Move the view horizontally and vertically
- **Autoset**: Automatically adjusts scales to optimize the displayed waveform

### 2.5.3 Special Features

- **Waveform viewing**: Real-time display of voltage over time
- **Time measurements**: Measure time intervals between signal features
- **Amplitude measurements**: Measure peak-to-peak and other voltage values
- **Frequency calculation**: Real-time calculation of signal frequency

## 2.6 Using the Spectrum Analyzer Mode

### 2.6.1 Understanding the Interface

The Spectrum Analyzer interface consists of:

<!-- IMAGE: Labeled screenshot of Spectrum Analyzer interface with main components marked -->

1. **Main chart area**: Displays the frequency spectrum
2. **Control panel**: Contains playback and view controls
3. **Information bar**: Shows dominant frequency and other measurements

### 2.6.2 Basic Controls

- **Play/Pause**: Controls whether the display updates with new data
- **Zoom controls**: Adjust the frequency scale (X-axis) and amplitude scale (Y-axis)
- **Pan controls**: Move the view horizontally and vertically
- **Autoset**: Automatically adjusts scales to show the most relevant frequency content

### 2.6.3 Interpreting the Display

- **X-axis**: Frequency in Hz, kHz, or MHz
- **Y-axis**: Signal magnitude in dB
- **Peaks**: Represent strong frequency components in the signal
- **Dominant Frequency**: The frequency with the highest magnitude, displayed in the information section

<!-- IMAGE: Screenshot of FFT display with labels pointing to peaks and axes -->

### 2.6.4 Special Features

- **Frequency domain analysis**: Visualize the spectral components of your signal
- **Dominant frequency detection**: Automatically identify the strongest frequency component
- **Logarithmic amplitude scale**: Better visualization of wide dynamic range signals
- **Adjustable frequency resolution**: Zoom in to distinguish closely spaced frequency components

## 2.7 Troubleshooting

### 2.7.1 Connection Issues

| Problem | Possible Solutions |
|---------|-------------------|
| Cannot find ESP32 WiFi network | • Ensure ESP32 is powered on<br>• Verify firmware installation<br>• Restart ESP32<br>• Reset WiFi settings |
| Connection timeout | • Move closer to ESP32<br>• Reduce WiFi interference<br>• Restart ESP32 and app |
| Cannot connect to external WiFi | • Verify WiFi credentials<br>• Ensure network is in range<br>• Check if network requires portal authentication |

### 2.7.2 Display Issues

| Problem | Possible Solutions |
|---------|-------------------|
| No waveform displayed | • Check signal connections<br>• Try to restart the ESP32<br>• Adjust trigger settings |
| Unstable waveform | • Adjust trigger level<br>• Change trigger edge<br>• Apply filters to reduce noise<br>• Ensure signal is consistent |
| Clipped waveform | • Select a larger voltage scale<br>• Reduce input signal amplitude |
| Display freezes | • Pause and resume acquisition<br>• Restart the app<br>• Restart the ESP32 |

## 2.9 Updating the Application

To update the ARG_OSCI app:

1. Visit the [official releases page](https://github.com/ArgOsciProyect/ARG_OSCI_APP/releases)
2. Download the latest version for your platform
3. Install following the same procedure as the initial installation
   - For Windows and Linux, you can replace the existing files
   - For Android, install the new APK

Configuration settings will be preserved across updates.
