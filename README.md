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

```bash
# Example of ADB in action
$ adb devices
List of devices attached
emulator-5554    device
```

## 🔧 Basic Concepts
ADB consists of three main components:
- 🖥️ A client, which runs on your development machine
- 📱 A daemon (adbd), which runs as a background process on each device
- 🔄 A server, which manages communication between the client and the daemon

## 📱 Device Management
This section covers commands for:
- 🔌 Managing device connections
- 🔄 Rebooting devices
- ℹ️ Getting device information
- ⚡ Managing device state
- 🔗 Working with multiple devices

## 🔒 Bootloader Operations
Essential bootloader commands:
- 🔓 Unlocking bootloader
- 🔒 Locking bootloader
- 🔄 Rebooting to bootloader
- 📱 Rebooting to recovery
- ⚡ Rebooting to fastboot
- 🔍 Checking bootloader status

```bash
# Example bootloader commands
$ adb reboot bootloader
$ adb reboot recovery
$ adb reboot fastboot
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
# Example fastboot commands
$ fastboot devices
$ fastboot flash recovery recovery.img
$ fastboot oem unlock
$ fastboot boot recovery.img
$ fastboot getvar all
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

## 📂 File Operations
Commands for:
- 📤 Transferring files between device and computer
- 📁 Managing device file system
- 🔍 Accessing application data
- 💾 Working with different storage locations

## ⚙️ System Operations
Tools for:
- ⚡ Managing system settings
- 📊 Monitoring system resources
- 🔧 Controlling system services
- 🛠️ Managing device features
- 🔍 Working with system properties

## 🔍 Debugging Tools
Essential debugging features:
- 📝 Logcat for viewing system logs
- 🐛 Bug report generation
- 📊 Process monitoring
- 🔍 Activity monitoring
- 📈 Performance analysis

## ⌨️ Input Simulation
Methods for:
- ⌨️ Simulating key events
- 📝 Inputting text
- 👆 Simulating touch events
- 🎮 Controlling device input

## 🖥️ Screen Operations
Features for:
- 📸 Capturing screenshots
- 🎥 Recording screen
- 🖼️ Managing display properties
- 📐 Controlling screen orientation
- 📏 Adjusting screen density

## 💾 Backup and Restore
Tools for:
- 💾 Creating device backups
- 🔄 Restoring from backups
- 📦 Managing backup data
- 📥 Sideloading applications

## 🔐 Permissions Management
Commands for:
- 🔑 Managing application permissions
- 👥 Viewing permission groups
- ✅ Granting and revoking permissions
- ⚡ Managing runtime permissions

## ⚡ Shared Preferences
Operations for:
- ⚙️ Managing application preferences
- 📊 Working with different data types
- 🔄 Modifying preference values
- 🗑️ Clearing preferences

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