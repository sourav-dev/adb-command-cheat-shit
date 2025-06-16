# 🚀 Android Debug Bridge (ADB) Command Reference Guide

```ascii
    _    ____  ____    
   / \  |  _ \| __ )   
  / _ \ | | | |  _ \   
 / ___ \| |_| | |_) |  
/_/   \_\____/|____/   
```

> Your ultimate companion for Android device debugging and development 🛠️

## 📑 Table of Contents
1. [🎯 Introduction](#introduction)
2. [🔧 Basic Concepts](#basic-concepts)
3. [📱 Device Management](#device-management)
4. [🔒 Bootloader Operations](#bootloader-operations)
5. [⚡ Fastboot Commands](#fastboot-commands)
6. [🔨 AOSP Development](#aosp-development)
7. [📦 Application Management](#application-management)
8. [📂 File Operations](#file-operations)
9. [⚙️ System Operations](#system-operations)
10. [🔍 Debugging Tools](#debugging-tools)
11. [⌨️ Input Simulation](#input-simulation)
12. [🖥️ Screen Operations](#screen-operations)
13. [💾 Backup and Restore](#backup-and-restore)
14. [🔐 Permissions Management](#permissions-management)
15. [⚡ Shared Preferences](#shared-preferences)

## 🎯 Introduction
The Android Debug Bridge (ADB) is a versatile command-line tool that lets you communicate with a device. It facilitates various device operations, such as installing and debugging apps, and it provides access to a Unix shell that you can use to run a variety of commands on a device.

## 🔧 Basic Concepts
ADB consists of three main components:
- 🖥️ A client, which runs on your development machine
- 📱 A daemon (adbd), which runs as a background process on each device
- 🔄 A server, which manages communication between the client and the daemon

```bash
# Basic ADB Commands
$ adb version                    # Check ADB version
$ adb help                      # Show all commands
$ adb start-server              # Start ADB server
$ adb kill-server               # Stop ADB server
$ adb devices -l                # List devices with details
```

## 📱 Device Management
This section covers commands for:
- 🔌 Managing device connections
- 🔄 Rebooting devices
- ℹ️ Getting device information
- ⚡ Managing device state
- 🔗 Working with multiple devices

```bash
# Device Connection
$ adb devices                   # List connected devices
$ adb connect <IP:PORT>         # Connect to device over network
$ adb disconnect <IP:PORT>      # Disconnect from device
$ adb usb                       # Restart USB connection
$ adb tcpip 5555                # Restart TCP/IP connection

# Device Information
$ adb get-state                 # Get device state
$ adb get-serialno              # Get device serial number
$ adb shell getprop             # Get all device properties
$ adb shell getprop ro.build.version.release  # Get Android version
$ adb shell getprop ro.product.model         # Get device model

# Device Control
$ adb reboot                    # Reboot device
$ adb reboot bootloader         # Reboot to bootloader
$ adb reboot recovery           # Reboot to recovery
$ adb root                      # Restart adbd with root permissions
$ adb unroot                    # Restart adbd without root permissions
```

## 🔒 Bootloader Operations
Essential bootloader commands:
- 🔓 Unlocking bootloader
- 🔒 Locking bootloader
- 🔄 Rebooting to bootloader
- 📱 Rebooting to recovery
- ⚡ Rebooting to fastboot
- 🔍 Checking bootloader status

```bash
# Bootloader Commands
$ adb reboot bootloader         # Reboot to bootloader
$ adb reboot fastboot           # Reboot to fastboot
$ fastboot oem unlock           # Unlock bootloader
$ fastboot oem lock             # Lock bootloader
$ fastboot oem device-info      # Check bootloader status
$ fastboot flashing unlock      # Unlock bootloader (newer devices)
$ fastboot flashing lock        # Lock bootloader (newer devices)
```

## ⚡ Fastboot Commands
Common fastboot operations:
- 📥 Flashing partitions
- 🔄 Updating firmware
- 📱 Installing custom recovery
- 🔒 Locking/unlocking bootloader
- 📊 Getting device information
- 🔍 Verifying partitions

```bash
# Fastboot Basic Commands
$ fastboot devices              # List fastboot devices
$ fastboot getvar all           # Get all device variables
$ fastboot getvar product       # Get product name
$ fastboot getvar version-bootloader  # Get bootloader version

# Fastboot Flash Commands
$ fastboot flash recovery recovery.img    # Flash recovery
$ fastboot flash boot boot.img           # Flash boot
$ fastboot flash system system.img       # Flash system
$ fastboot flash vendor vendor.img       # Flash vendor
$ fastboot flash userdata userdata.img   # Flash userdata

# Fastboot Boot Commands
$ fastboot boot recovery.img    # Boot recovery without flashing
$ fastboot boot boot.img       # Boot kernel without flashing
$ fastboot boot system.img     # Boot system without flashing

# Fastboot Wipe Commands
$ fastboot erase recovery      # Erase recovery partition
$ fastboot erase boot         # Erase boot partition
$ fastboot erase system       # Erase system partition
$ fastboot erase userdata     # Erase userdata partition
$ fastboot erase cache        # Erase cache partition

# Fastboot OEM Commands
$ fastboot oem unlock          # Unlock bootloader
$ fastboot oem lock            # Lock bootloader
$ fastboot oem device-info     # Get device information
$ fastboot oem get_identifier_token  # Get identifier token
```

## 🔨 AOSP Development
Essential AOSP commands and operations:
- 📥 Building AOSP
- 🔄 Syncing source code
- 📱 Flashing AOSP builds
- 🔧 Debugging AOSP
- 📊 System tracing
- 🔍 Kernel debugging

```bash
# AOSP Build Commands
$ repo init -u https://android.googlesource.com/platform/manifest
$ repo sync
$ source build/envsetup.sh
$ lunch aosp_arm-eng
$ make -j8

# AOSP Debug Commands
$ adb root
$ adb remount
$ adb shell stop
$ adb shell start
$ adb shell dumpsys
$ adb shell dmesg

# AOSP System Tracing
$ atrace -t 10 -b 1024 -a com.android.systemui
$ systrace -t 10 -b 1024 -a com.android.systemui

# AOSP Kernel Debugging
$ adb shell cat /proc/kmsg
$ adb shell dmesg
$ adb shell cat /proc/last_kmsg

# AOSP Logging
$ adb logcat -b all -v threadtime
$ adb logcat -b radio
$ adb logcat -b events
$ adb logcat -b system
$ adb logcat -b crash
```

## 📦 Application Management
Learn how to:
- 📥 Install and uninstall applications
- 🔄 Update existing applications
- 🔐 Manage application permissions
- 🗑️ Clear application data
- 📋 List installed packages
- ℹ️ Get application information

```bash
# App Installation
$ adb install app.apk          # Install app
$ adb install -r app.apk       # Install app with replacement
$ adb install -d app.apk       # Install app with downgrade
$ adb install -g app.apk       # Install app with all permissions granted
$ adb install-multiple app1.apk app2.apk  # Install multiple apps

# App Uninstallation
$ adb uninstall com.package.name  # Uninstall app
$ adb uninstall -k com.package.name  # Uninstall app keeping data
$ adb shell pm clear com.package.name  # Clear app data

# App Management
$ adb shell pm list packages    # List all packages
$ adb shell pm list packages -f # List packages with paths
$ adb shell pm list packages -3 # List third-party packages
$ adb shell pm list packages -s # List system packages
$ adb shell pm path com.package.name  # Get app path
$ adb shell pm dump com.package.name  # Get app info

# App Permissions
$ adb shell pm list permissions  # List all permissions
$ adb shell pm list permissions -g  # List permission groups
$ adb shell pm grant com.package.name android.permission.CAMERA  # Grant permission
$ adb shell pm revoke com.package.name android.permission.CAMERA  # Revoke permission
```

## 📂 File Operations
Commands for:
- 📤 Transferring files between device and computer
- 📁 Managing device file system
- 🔍 Accessing application data
- 💾 Working with different storage locations

```bash
# File Transfer
$ adb push local_file /sdcard/remote_file  # Push file to device
$ adb pull /sdcard/remote_file local_file  # Pull file from device
$ adb sync                                 # Sync files between device and computer

# File System Navigation
$ adb shell ls                             # List files
$ adb shell ls -l                          # List files with details
$ adb shell ls -R                          # List files recursively
$ adb shell cd /sdcard                     # Change directory
$ adb shell pwd                            # Print working directory

# File Operations
$ adb shell mkdir /sdcard/new_folder       # Create directory
$ adb shell rm /sdcard/file                # Remove file
$ adb shell rm -r /sdcard/folder           # Remove directory
$ adb shell cp /sdcard/file1 /sdcard/file2 # Copy file
$ adb shell mv /sdcard/file1 /sdcard/file2 # Move file

# Storage Locations
$ adb shell ls /sdcard                     # External storage
$ adb shell ls /storage/emulated/0         # Internal storage
$ adb shell ls /data/data                  # App data directory
$ adb shell ls /system/app                 # System apps directory
```

## ⚙️ System Operations
Tools for:
- ⚡ Managing system settings
- 📊 Monitoring system resources
- 🔧 Controlling system services
- 🛠️ Managing device features
- 🔍 Working with system properties

```bash
# System Settings
$ adb shell settings put global airplane_mode_on 1  # Enable airplane mode
$ adb shell settings put global airplane_mode_on 0  # Disable airplane mode
$ adb shell settings put system screen_brightness 100  # Set brightness
$ adb shell settings put secure location_mode 3  # Enable location

# System Services
$ adb shell service list                    # List all services
$ adb shell dumpsys                         # Dump system info
$ adb shell dumpsys battery                 # Battery info
$ adb shell dumpsys wifi                    # WiFi info
$ adb shell dumpsys bluetooth               # Bluetooth info
$ adb shell dumpsys telephony.registry      # Telephony info

# System Properties
$ adb shell getprop                         # Get all properties
$ adb shell getprop ro.build.version.sdk    # Get SDK version
$ adb shell getprop ro.product.model       # Get device model
$ adb shell getprop ro.product.manufacturer # Get manufacturer
$ adb shell getprop ro.product.cpu.abi      # Get CPU architecture

# System Control
$ adb shell svc power stayon true          # Keep screen on
$ adb shell svc power stayon false         # Allow screen off
$ adb shell svc data enable                # Enable mobile data
$ adb shell svc data disable               # Disable mobile data
$ adb shell svc wifi enable                # Enable WiFi
$ adb shell svc wifi disable               # Disable WiFi
```

## 🔍 Debugging Tools
Essential debugging features:
- 📝 Logcat for viewing system logs
- 🐛 Bug report generation
- 📊 Process monitoring
- 🔍 Activity monitoring
- 📈 Performance analysis

```bash
# Logcat Commands
$ adb logcat                    # View all logs
$ adb logcat -c                 # Clear log buffer
$ adb logcat -d                 # Dump log and exit
$ adb logcat -f /sdcard/log.txt # Save log to file
$ adb logcat *:E                # Show only errors
$ adb logcat -v time            # Show timestamps
$ adb logcat -v threadtime      # Show thread time
$ adb logcat -v long            # Show long format

# Bug Reports
$ adb bugreport                 # Generate bug report
$ adb bugreport /sdcard/bug.zip # Save bug report
$ adb shell dumpsys > dump.txt  # Save system dump

# Process Monitoring
$ adb shell ps                  # List processes
$ adb shell top                 # Monitor processes
$ adb shell top -n 1            # One-time process list
$ adb shell procrank            # Process memory usage

# Activity Monitoring
$ adb shell dumpsys activity    # Activity manager info
$ adb shell dumpsys window      # Window manager info
$ adb shell dumpsys meminfo     # Memory info
$ adb shell dumpsys cpuinfo     # CPU info
$ adb shell dumpsys battery     # Battery info
```

## ⌨️ Input Simulation
Methods for:
- ⌨️ Simulating key events
- 📝 Inputting text
- 👆 Simulating touch events
- 🎮 Controlling device input

```bash
# Key Events
$ adb shell input keyevent KEYCODE_HOME    # Press home
$ adb shell input keyevent KEYCODE_BACK    # Press back
$ adb shell input keyevent KEYCODE_POWER   # Press power
$ adb shell input keyevent KEYCODE_VOLUME_UP    # Volume up
$ adb shell input keyevent KEYCODE_VOLUME_DOWN  # Volume down

# Text Input
$ adb shell input text "Hello World"       # Input text
$ adb shell input text "Hello\ World"      # Input text with space

# Touch Events
$ adb shell input tap x y                  # Tap at coordinates
$ adb shell input swipe x1 y1 x2 y2       # Swipe from point to point
$ adb shell input draganddrop x1 y1 x2 y2 # Drag and drop

# Input Control
$ adb shell input keyevent --longpress KEYCODE_POWER  # Long press
$ adb shell input keyevent --doubletap KEYCODE_POWER  # Double tap
$ adb shell input keyevent --repeat KEYCODE_VOLUME_UP # Repeat key
```

## 🖥️ Screen Operations
Features for:
- 📸 Capturing screenshots
- 🎥 Recording screen
- 🖼️ Managing display properties
- 📐 Controlling screen orientation
- 📏 Adjusting screen density

```bash
# Screenshot
$ adb shell screencap -p /sdcard/screen.png  # Take screenshot
$ adb pull /sdcard/screen.png                # Pull screenshot
$ adb shell screencap -p /sdcard/screen.png && adb pull /sdcard/screen.png  # One-liner

# Screen Recording
$ adb shell screenrecord /sdcard/video.mp4   # Record screen
$ adb shell screenrecord --size 1280x720 /sdcard/video.mp4  # Record with size
$ adb shell screenrecord --bit-rate 6000000 /sdcard/video.mp4  # Record with bitrate
$ adb shell screenrecord --time-limit 30 /sdcard/video.mp4  # Record with time limit

# Display Properties
$ adb shell wm size                          # Get screen size
$ adb shell wm size 1080x1920               # Set screen size
$ adb shell wm density                       # Get screen density
$ adb shell wm density 420                   # Set screen density
$ adb shell wm overscan 0,0,0,0             # Set overscan
$ adb shell wm scaling auto                  # Set scaling mode
```

## 💾 Backup and Restore
Tools for:
- 💾 Creating device backups
- 🔄 Restoring from backups
- 📦 Managing backup data
- 📥 Sideloading applications

```bash
# Backup Commands
$ adb backup -apk -all -f backup.ab         # Backup all apps and data
$ adb backup -apk -shared -all -f backup.ab # Backup all with shared storage
$ adb backup -apk -nosystem -all -f backup.ab # Backup non-system apps
$ adb backup -apk -f backup.ab com.package.name # Backup specific app

# Restore Commands
$ adb restore backup.ab                      # Restore from backup
$ adb restore -f backup.ab                   # Force restore

# Sideload Commands
$ adb sideload update.zip                    # Sideload update
$ adb sideload -s emulator-5554 update.zip   # Sideload to specific device
```

## 🔐 Permissions Management
Commands for:
- 🔑 Managing application permissions
- 👥 Viewing permission groups
- ✅ Granting and revoking permissions
- ⚡ Managing runtime permissions

```bash
# Permission Commands
$ adb shell pm list permissions              # List all permissions
$ adb shell pm list permissions -g           # List permission groups
$ adb shell pm list permissions -d           # List dangerous permissions
$ adb shell pm list permissions -f           # List permissions with flags

# Grant/Revoke Permissions
$ adb shell pm grant com.package.name android.permission.CAMERA
$ adb shell pm revoke com.package.name android.permission.CAMERA
$ adb shell pm reset-permissions -p com.package.name

# Runtime Permissions
$ adb shell pm list packages -g              # List packages with groups
$ adb shell pm list packages -f              # List packages with paths
$ adb shell pm list packages -d              # List packages with permissions
```

## ⚡ Shared Preferences
Operations for:
- ⚙️ Managing application preferences
- 📊 Working with different data types
- 🔄 Modifying preference values
- 🗑️ Clearing preferences

```bash
# Shared Preferences Commands
$ adb shell 'run-as com.package.name cat /data/data/com.package.name/shared_prefs/prefs.xml'
$ adb shell 'run-as com.package.name cat /data/data/com.package.name/shared_prefs/*.xml'

# Modify Preferences
$ adb shell 'run-as com.package.name echo "<?xml version='1.0' encoding='utf-8' standalone='yes' ?><map><string name='key'>value</string></map>" > /data/data/com.package.name/shared_prefs/prefs.xml'

# Clear Preferences
$ adb shell 'run-as com.package.name rm /data/data/com.package.name/shared_prefs/*.xml'
```

## 🚀 Best Practices
1. ✅ Always verify device connection before executing commands
2. 🎯 Use appropriate flags for specific device targeting
3. 🔄 Keep ADB tools updated
4. ⚠️ Use proper error handling
5. 🔒 Follow security best practices

## 🔧 Troubleshooting
Common issues and solutions:
- ❌ Device not recognized
- 🔌 Connection problems
- 🔒 Permission issues
- ⚠️ Command execution errors

## 📚 Additional Resources
- [📖 Official Android Developer Documentation](https://developer.android.com/studio/command-line/adb)
- [🔧 Android Debug Bridge Documentation](https://developer.android.com/tools/adb)
- [💻 Android Studio Documentation](https://developer.android.com/studio)

## 🤝 Contributing
Feel free to contribute to this guide by:
1. 🐛 Reporting issues
2. 💡 Suggesting improvements
3. ➕ Adding new sections
4. 📝 Updating existing content

## 📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

---
<div align="center">
Made with ❤️ by Android Developers
</div> 