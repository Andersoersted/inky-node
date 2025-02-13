# rpiinky Display App

The **rpiinky Display App** is a Flask-based application designed to remotely control an Inky e-ink display on a Raspberry Pi. It allows you to upload images to the display, view real-time system metrics, and perform administrative functions (such as system updates, backups, and application updates) through both a web interface and API endpoints.

The hub for controlling multiple nodes is available at [inkydocker](https://github.com/Andersoersted/inkydocker).

---

## Table of Contents

- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
  - [Web Interface](#web-interface)
  - [API Endpoints & CURL Examples](#api-endpoints--curl-examples)

---

## Features

- **Display Management**
  - Automatically displays a startup image (with IP, domain, and hostname information) on first boot.
  - Upload and display images on the Inky display.
  - Preview the current image being shown on the dashboard.

- **Display Settings**
  - View display information (model, resolution, rotation, colour).
  - Change display orientation (horizontal/vertical).

- **System Administration**
  - Perform a system update/upgrade (which reboots the device).
  - Create a compressed backup of the SD card.
  - Update the application via a Git pull and reboot.

- **Real-Time Metrics**
  - Stream real-time system metrics (CPU, memory, disk usage) via Server-Sent Events (SSE).

- **User Interface Enhancements**
  - Responsive, modern dashboard.
  - Theme toggle (light/dark mode).

---

## Requirements

- **Operating System:** 64-bit Raspberry Pi OS Lite
- **Python:** 3.x (e.g., Python 3.11)
- **Python Packages:** Flask, Pillow, pillow-heif, inky, psutil
- **System Configuration:** SPI and I2C interfaces must be enabled

---

## Installation

1. **Write the 64-bit Raspberry Pi OS Lite image** to your SD card.

2. **Clone the rpiinky repository:**

   ```bash
   git clone https://github.com/Andersoersted/rpiinky

	3.	Change to the rpiinky directory:

cd rpiinky


	4.	Run the installation script:

sudo bash install.sh

This script will:
	•	Update and upgrade system packages.
	•	Enable the I2C and SPI interfaces.
	•	Create the application directory and Python virtual environment.
	•	Install all required Python dependencies (including psutil).
	•	Create and enable a systemd service for the rpiinky Display App.
	•	Reboot the system once installation is complete.

Usage

Web Interface

After installation and reboot, access the dashboard by navigating to your device’s IP address (for example, http://192.168.x.x) in your web browser. The dashboard displays:
	•	A preview of the current display image.
	•	Display information (model, resolution, rotation, colour).
	•	Real-time system metrics.
	•	Forms to upload a new image, change orientation, and perform administrative tasks.
	•	A theme toggle button for switching between light and dark modes.

API Endpoints & CURL Examples

Replace <IP_ADDRESS> with your device’s IP address in the following examples.

Upload an Image

Upload an image to display on the e-ink screen:

curl -F "file=@/path/to/your/image.jpg" http://<IP_ADDRESS>/send_image

Set Display Orientation

Set the display orientation to either “horizontal” or “vertical”:

curl -X POST -d "orientation=vertical" http://<IP_ADDRESS>/set_orientation

Get Display Information

Retrieve display information in JSON format:

curl http://<IP_ADDRESS>/display_info

Perform System Update

Trigger a system update and upgrade (which will reboot the device):

curl -X POST http://<IP_ADDRESS>/system_update

Create Disk Backup

Create a compressed backup of the SD card and download it:

curl -X POST http://<IP_ADDRESS>/backup --output backup.img.gz

Update Application

Perform a Git pull to update the application and reboot the device:

curl -X POST http://<IP_ADDRESS>/update

Connect to the Metrics Stream (SSE)

Connect to the SSE stream to receive real-time system metrics:

curl http://<IP_ADDRESS>/stream

This documentation provides complete instructions for installation and usage of the rpiinky Display App. For multi-node control, please refer to the inkydocker repository.

