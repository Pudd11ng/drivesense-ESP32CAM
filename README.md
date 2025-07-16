# DriveSense ESP32-CAM - Driver Face Monitoring Module

<div align="center">
  <img src="https://raw.githubusercontent.com/Pudd11ng/drivesense/main/assets/drivesense_logo.png" alt="DriveSense Logo" width="200"/>

  <img src="https://img.shields.io/badge/DriveSense-ESP32CAM-blue.svg" alt="DriveSense ESP32-CAM"/>
  <img src="https://img.shields.io/badge/ESP--IDF-v5.0-orange.svg" alt="ESP-IDF"/>
  <img src="https://img.shields.io/badge/Video-Streaming-green.svg" alt="Video Streaming"/>
  <img src="https://img.shields.io/badge/WiFi-AP%20Mode-red.svg" alt="WiFi AP"/>
  <img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="MIT License"/>
</div>

A specialized ESP32-CAM firmware module designed for the **DriveSense - Intelligent Driver Safety Assistant** system. This module streams real-time video of the driver's face to the DriveSense Flutter mobile application for AI-powered behavior analysis and safety monitoring.

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [DriveSense Ecosystem](#-drivesense-ecosystem)
- [Integration with DriveSense App](#integration-with-drivesense-app)
- [Key Features](#key-features)
- [Technical Specifications](#technical-specifications)
- [Hardware Requirements](#-hardware-requirements)
- [Software Prerequisites](#-software-prerequisites)
- [Project Setup and Installation](#-project-setup-and-installation)
- [DriveSense App Integration](#-drivesense-app-integration)
- [Manual Testing & Development](#-manual-testing--development)
- [Configuration Options](#-configuration-options)
- [Troubleshooting](#-troubleshooting)
- [Advanced Configuration](#-advanced-configuration)
- [API Endpoints](#-api-endpoints)
- [Contributing](#-contributing)
- [License](#-license)
- [Acknowledgments](#-acknowledgments)

## 🎯 Project Overview

**DriveSense ESP32-CAM** is the hardware component of the comprehensive DriveSense driver safety system. It captures and streams live video feed of the driver's face to the DriveSense mobile application, which uses YOLO-based AI/ML models to detect risky behaviors such as drowsiness, phone usage, distraction, and intoxication.

### 🔗 DriveSense Ecosystem

This ESP32-CAM module is part of the larger DriveSense project:

- **🚗 Main App**: [drivesense](https://github.com/Pudd11ng/drivesense) - Flutter mobile application with AI behavior detection
- **🔧 Backend API**: [drivesense-backend](https://github.com/Pudd11ng/drivesense-backend) - Node.js server for data processing
- **📹 ESP32-CAM**: **This repository** - Camera module firmware for driver face streaming

### Key Technologies
- **Hardware**: ESP32-CAM with optimized camera streaming firmware
- **Connectivity**: WiFi Access Point mode for dedicated video streaming
- **Video Processing**: MJPEG streaming at 20 FPS for real-time AI analysis
- **AI Integration**: Stream format optimized for YOLO object detection
- **Power Management**: Optimized for 12V vehicle power systems
- **Multi-Platform**: Compatible with various ESP32-CAM board types

### Integration with DriveSense App

The ESP32-CAM module works seamlessly with the DriveSense Flutter app:

1. **Video Streaming**: Provides real-time MJPEG stream of driver's face (SVGA 800x600 @ 20fps)
2. **AI Processing**: Stream is processed by YOLOv11 models in the Flutter app
3. **Behavior Detection**: Detects drowsiness, phone usage, distraction, and intoxication
4. **Safety Alerts**: Triggers customized audio alerts with 120-second cooldown system
5. **Data Analytics**: Contributes to driving behavior analysis and safety scoring
6. **Emergency Features**: Supports accident detection and emergency contact notifications

### Key Features

- **Driver Face Streaming**: Optimized for capturing driver's facial expressions and head movements
- **DriveSense Integration**: Seamlessly connects with DriveSense Flutter app for AI behavior analysis
- **WiFi Access Point Mode**: Creates dedicated network for reliable video streaming
- **Real-time MJPEG Streaming**: High-quality video feed at up to 20 FPS for accurate AI detection
- **Multi-client Support**: Supports DriveSense app plus additional monitoring devices (up to 4 total)
- **Optimized Performance**: Dual-core ESP32 optimization for stable video streaming
- **Multiple Board Support**: Compatible with various ESP32-CAM development boards
- **Easy Integration**: Simple HTTP endpoint for Flutter app video consumption

### Technical Specifications

- **Primary Use**: Driver face monitoring for DriveSense safety system
- **Resolution**: SVGA (800x600) JPEG format - optimal for AI face detection
- **Frame Rate**: Up to 20 FPS with automatic frame rate control
- **WiFi**: 802.11 b/g/n Access Point mode for dedicated streaming
- **IP Address**: Fixed at 192.168.4.1 for consistent app connectivity
- **Port**: HTTP server on port 80 with MJPEG streaming endpoint
- **Compression**: JPEG quality level 5 (balanced quality/performance for AI processing)
- **AI Compatibility**: Stream format optimized for YOLO object detection models

## 🔧 Hardware Requirements

### Supported ESP32-CAM Boards

- **AiThinker ESP32-CAM** (Default configuration)
- **Freenove ESP32-WROVER CAM**
- **Espressif ESP-EYE**
- **TTGO T-Journal ESP32 Camera**

### Additional Hardware

- **ESP32-CAM development board** (primary component)
- **Car mount/dashboard holder** for optimal driver face positioning
- **USB-to-Serial converter** (for programming and debugging)
- **12V to 5V car adapter** for vehicle power supply
- **Jumper wires** for initial setup and programming
- **MicroSD card** (optional, for future expansion/logging)

### DriveSense App Requirements

- **Android device** with DriveSense Flutter app installed
- **WiFi capability** to connect to ESP32-CAM network (`drivesense_camera_ds000001`)
- **Network credentials**: Password `password123` for ESP32-CAM connection
- **Internet connection** for AI model updates and backend communication
- **Camera permissions** for supplementary monitoring features
- **App environment**: Configured with `DEVICE_VIDEO_URL='http://192.168.4.1'`

## 📋 Software Prerequisites

### Required Tools

1. **ESP-IDF Framework** (v4.4 or later)
   - Download from: https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/
   
2. **Python 3.6+** (included with ESP-IDF)

3. **Git** (for cloning repositories)

### Development Environment Setup

#### Windows Setup
```powershell
# Install ESP-IDF using the installer
# Download from: https://dl.espressif.com/dl/esp-idf/
# Or use the command line method:

# Clone ESP-IDF
git clone --recursive https://github.com/espressif/esp-idf.git
cd esp-idf
git checkout v5.0

# Install ESP-IDF
./install.bat

# Set up environment variables
./export.bat
```

#### Linux/macOS Setup
```bash
# Install prerequisites
sudo apt-get update
sudo apt-get install git wget flex bison gperf python3 python3-pip python3-setuptools cmake ninja-build ccache libffi-dev libssl-dev dfu-util libusb-1.0-0

# Clone ESP-IDF
git clone --recursive https://github.com/espressif/esp-idf.git
cd esp-idf
git checkout v5.0

# Install ESP-IDF
./install.sh

# Set up environment variables
source ./export.sh
```

## 🚀 Project Setup and Installation

### 1. Clone the Repository
```powershell
git clone https://github.com/Pudd11ng/drivesense-ESP32CAM.git
cd drivesense-ESP32CAM
```

### 2. Configure the Project

#### Set Target Device
```powershell
idf.py set-target esp32
```

#### Configure Board Type and Settings
```powershell
idf.py menuconfig
```

Navigate to:
- **Application Configuration > Select Board** → Choose your ESP32-CAM board type

> **Note**: Default settings are optimized for DriveSense app integration. Only modify if you have specific requirements.

### 3. Hardware Configuration

#### For Programming (using USB-to-Serial converter):
```
ESP32-CAM    USB-to-Serial
GND      →   GND
5V       →   5V
U0T      →   RX
U0R      →   TX
IO0      →   GND (for programming mode)
```

#### For Normal Operation:
- Remove the IO0 to GND connection
- Power the board with 5V supply

### 4. Build and Flash

#### Build the Project
```powershell
idf.py build
```

#### Flash to Device
```powershell
idf.py -p COM3 flash  # Replace COM3 with your serial port
```

#### Monitor Output
```powershell
idf.py -p COM3 monitor
```

> **Tip**: Use `idf.py -p COM3 flash monitor` to flash and monitor in one command.

### 5. Verify Installation

#### Check Serial Output
After flashing, you should see output similar to:
```
I (XXX) esp32-cam Webserver: WiFi SoftAP started with SSID:drivesense_camera_ds000001
I (XXX) esp32-cam Webserver: SoftAP IP address: 192.168.4.1
I (XXX) esp32-cam Webserver: HTTP server started
I (XXX) esp32-cam Webserver: ESP32 CAM Web Server is up and running
```

#### Test Camera Stream
```powershell
# Connect to the ESP32-CAM WiFi network first, then:
curl http://192.168.4.1/
# or
Invoke-WebRequest -Uri "http://192.168.4.1/" -Method GET
```

## 🚗 DriveSense App Integration

### 1. Setup ESP32-CAM in Vehicle
- **Position**: Mount ESP32-CAM on dashboard facing the driver
- **Angle**: Ensure camera captures driver's face clearly (eye level recommended)
- **Power**: Connect to 12V car adapter (with 5V conversion)
- **Distance**: Optimal distance 30-50cm from driver's face

### 2. Connect DriveSense App
- **Install**: Download DriveSense app on Android device
- **WiFi Connection**: Connect to ESP32-CAM network
  - **Network Name**: `drivesense_camera_ds000001`
  - **Password**: `password123`
  - **Stream URL**: `http://192.168.4.1`
- **Integration**: App automatically discovers camera stream
- **Verification**: Check connection status in app settings

### 3. Start Driver Monitoring
- **Launch**: Open DriveSense app and start monitoring session
- **Stream Connection**: App connects to camera stream at `http://192.168.4.1`
- **AI Processing**: YOLOv11 models analyze driver behavior in real-time
- **Video Quality**: SVGA (800x600) resolution at 20 FPS for optimal AI detection
- **Alert System**: Audio alerts with 120-second cooldown for detected behaviors

### 4. Behavior Detection Features
- **😴 Drowsiness**: Detects eye closure patterns and yawning using YOLOv11
- **📱 Phone Usage**: Identifies when driver is using mobile device
- **👀 Distraction**: Monitors driver attention and head position
- **🍺 Intoxication**: Analyzes facial expressions and behavior patterns

### 5. Integration with DriveSense Ecosystem
- **Authentication**: Works with Google Sign-In from main app
- **Cloud Messaging**: Supports Firebase Cloud Messaging for alerts
- **Backend Integration**: Connects to Node.js backend for data processing
- **Emergency Features**: Supports accident detection and emergency contact notifications

## 🖥️ Manual Testing & Development

### Browser-Based Testing
For development and testing purposes, you can also view the camera stream directly:

### 1. Power Up the Device
- Connect 5V power supply to the ESP32-CAM
- Wait for the device to boot (check serial monitor for status)

### 2. Connect to WiFi Network
- Look for WiFi network: `drivesense_camera_ds000001`
- Password: `password123`
- Connect your device (phone, laptop, tablet)

### 3. Access Camera Stream
- Open web browser
- Navigate to: `http://192.168.4.1`
- Live camera feed will start automatically

### 4. Development Testing
- Multiple devices can connect simultaneously (up to 4 total)
- Use for testing camera positioning and video quality
- Monitor serial output for debugging information

## ⚙️ Configuration Options

### WiFi Settings (in main.c)
```c
#define ESP_WIFI_SSID "drivesense_camera_ds000001"  // Network name
#define ESP_WIFI_PASS "password123"                 // Password
#define ESP_WIFI_CHANNEL 1                          // WiFi channel
#define MAX_STA_CONN 4                              // Max connections
```

### Camera Settings (Optimized for DriveSense)
```c
#define CONFIG_XCLK_FREQ 20000000      // Camera clock frequency
.jpeg_quality = 5                      // JPEG quality (1-63, lower = better)
.frame_size = FRAMESIZE_SVGA          // Resolution (800x600 - optimal for AI)
const int FRAME_INTERVAL_MS = 50      // Frame rate control (50ms = 20fps)
```

### AI-Optimized Settings
```c
.pixel_format = PIXFORMAT_JPEG        // JPEG format for efficient streaming
.grab_mode = CAMERA_GRAB_LATEST      // Latest frame for real-time processing
.fb_count = 1                        // Single frame buffer for low latency
```

> **Important**: These settings are optimized for DriveSense AI processing. Modifications may affect detection accuracy.

### Server Optimization
```c
config.task_priority = tskIDLE_PRIORITY + 5;  // Server priority
config.stack_size = 4096;                     // Stack size
config.core_id = 1;                           // CPU core assignment
```

## 🔧 Troubleshooting

### Common Issues

1. **DriveSense App Cannot Connect**
   - Ensure ESP32-CAM is powered and WiFi network is visible
   - Check if `drivesense_camera_ds000001` network appears in WiFi list
   - Verify password: `password123`
   - Try restarting both ESP32-CAM and mobile device

2. **Camera not detected**
   - Check board type in menuconfig matches your hardware
   - Verify power supply (use 5V, not 3.3V)
   - Check camera module connection to ESP32-CAM board
   - Ensure camera ribbon cable is properly seated

3. **Video quality issues in DriveSense app**
   - Adjust camera positioning for better face capture
   - Check lighting conditions (avoid backlighting)
   - Ensure stable 5V power supply
   - Try different JPEG quality settings

4. **AI detection accuracy problems**
   - Verify camera is at eye level with driver
   - Ensure 30-50cm distance from driver's face
   - Check for proper lighting (avoid direct sunlight)
   - Confirm SVGA resolution is maintained

5. **Connection drops during driving**
   - Use quality 12V to 5V car adapter
   - Ensure solid mounting to reduce vibration
   - Check for electromagnetic interference from car electronics

4. **Build errors**
   - Update ESP-IDF to latest version
   - Clean build: `idf.py clean && idf.py build`
   - Check serial port permissions

### Serial Monitor Output
```
I (1234) esp32-cam Webserver: WiFi SoftAP started with SSID:drivesense_camera_ds000001
I (1245) esp32-cam Webserver: SoftAP IP address: 192.168.4.1
I (1256) esp32-cam Webserver: HTTP server started
I (1267) esp32-cam Webserver: ESP32 CAM Web Server is up and running
I (1278) esp32-cam Webserver: DriveSense integration ready
```

### DriveSense App Connection Test
```powershell
# Test ESP32-CAM connectivity
Test-NetConnection -ComputerName 192.168.4.1 -Port 80

# Verify video stream endpoint
Invoke-WebRequest -Uri "http://192.168.4.1/" -Method GET

# Check WiFi network availability
netsh wlan show profiles | Select-String "drivesense_camera_ds000001"

# Test network connectivity
ping 192.168.4.1
```

### DriveSense App Environment Check
```powershell
# Verify app environment configuration
# Check .env file contains:
# DEVICE_VIDEO_URL='http://192.168.4.1'
# Network: drivesense_camera_ds000001
# Password: password123
```

## 🛠️ Advanced Configuration

### DriveSense-Specific Optimizations
```c
// Frame rate optimized for AI processing
const int FRAME_INTERVAL_MS = 50;      // 20fps - optimal for YOLO detection

// Resolution optimized for face detection
.frame_size = FRAMESIZE_SVGA;          // 800x600 - best balance for AI accuracy

// JPEG quality for AI processing
.jpeg_quality = 5;                     // Balanced quality/performance for detection
```

### Custom Network Settings
To change WiFi credentials for your specific deployment:
```c
#define ESP_WIFI_SSID "your_drivesense_network"
#define ESP_WIFI_PASS "your_secure_password"
```

### Performance Tuning for AI Integration
- **Higher FPS**: Reduce `FRAME_INTERVAL_MS` (minimum ~33ms for 30fps)
  - Note: Higher FPS may impact AI processing performance
- **Better AI Accuracy**: Decrease `jpeg_quality` value (1-5 recommended)
- **Lower Latency**: Keep `FRAMESIZE_SVGA` for optimal AI detection balance
- **Stable Connection**: Ensure `MAX_STA_CONN` accommodates DriveSense app + backup devices

### Board-Specific Configuration
Each board type has different pin configurations in `camera_pins.h`. The project automatically selects the correct pins based on your menuconfig selection.

## 📡 API Endpoints

### DriveSense App Integration
- **GET /**: Main camera stream endpoint for DriveSense app
- **Stream Format**: MJPEG (multipart/x-mixed-replace)
- **Content-Type**: `multipart/x-mixed-replace;boundary=123456789000000000000987654321`
- **Resolution**: 800x600 (SVGA) optimized for AI face detection
- **Frame Rate**: Up to 20 FPS with consistent timing

### Flutter App Integration
The DriveSense Flutter app connects to this endpoint using:
```dart
String videoUrl = "http://192.168.4.1/";
// App processes MJPEG stream for YOLO-based behavior detection
```

## 🤝 Contributing

We welcome contributions to improve the DriveSense ESP32-CAM module! Please follow these guidelines:

1. Fork the repository from [drivesense-ESP32CAM](https://github.com/Pudd11ng/drivesense-ESP32CAM)
2. Create feature branch (`git checkout -b feature/camera-improvement`)
3. Make your changes with proper testing
4. Commit changes (`git commit -m 'Improve camera streaming for AI detection'`)
5. Push to branch (`git push origin feature/camera-improvement`)
6. Open Pull Request

### Development Guidelines
- Test with actual DriveSense Flutter app integration
- Ensure changes don't break AI detection accuracy
- Follow ESP-IDF coding conventions
- Add comprehensive comments for hardware-specific code
- Test with multiple ESP32-CAM board types

### Reporting Issues
- Use GitHub Issues for bug reports
- Include serial monitor output
- Specify ESP32-CAM board type
- Describe DriveSense app integration problems

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **DriveSense Project**: Part of the comprehensive driver safety ecosystem
- **YOLOv11**: For object detection framework enabling behavior recognition
- **ESP-IDF Framework**: By Espressif Systems for ESP32 development
- **ESP32-CAM Community**: For hardware support and contributions
- **Flutter Community**: For mobile app integration capabilities
- **Firebase**: For cloud messaging services
- **Freesound**: For audio alert resources
- **Original Tutorial**: https://esp32tutorials.com/esp32-cam-esp-idf-live-streaming-web-server/

---

<div align="center">
  <p><strong>🚗 DriveSense ESP32-CAM - Making Roads Safer Through AI</strong></p>
  <p>This ESP32-CAM module is specifically designed to work with the DriveSense Flutter app</p>
  <p>for real-time driver behavior monitoring and safety alerts.</p>
  <br>
  <p>📱 <strong>Main App</strong>: <a href="https://github.com/Pudd11ng/drivesense">drivesense</a></p>
  <p>🔧 <strong>Backend</strong>: <a href="https://github.com/Pudd11ng/drivesense-backend">drivesense-backend</a></p>
  <p>📹 <strong>Camera Module</strong>: <a href="https://github.com/Pudd11ng/drivesense-ESP32CAM">drivesense-ESP32CAM</a></p>
  <br>
  <p>© 2025 DriveSense Project. Built with ❤️ for road safety.</p>
</div>