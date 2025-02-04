---
layout: rom
title: LineageOS 18.1 (Android 11)
subtitle: for Raspberry Pi 4
date: 2021-07-20
tags: [rpi4, LineageOS, LOS18]
social-share: true
comments: true
---

Here's my build of LineageOS 18.1 for Raspberry Pi 4 Model B, Pi 400, and Compute Module 4. It is unofficial and unsupported by the LineageOS team. It's for **advanced users** only. Pi 4 model with at least 2GB of RAM is required to run this build.

<span style="color:#FF0000;">Important!</span> This image includes parts that are licensed under non-commercial license ([Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International](http://creativecommons.org/licenses/by-nc-sa/4.0/)). You may use this build freely in personal/educational/etc use. Commercial use is not allowed with this build!

![screenshot]({{ site.url }}/img/rpi4/LineageOS18/Screenshot_20210104-104810_Settings.png)

<span style="color:#FF0000;">Do not mirror my builds!</span> Please post a link to this page instead.

**lineage-18.1-20210720-UNOFFICIAL-KonstaKANG-rpi4.zip**  
[https://www.androidfilehost.com/?fid=14943124697586370965](https://www.androidfilehost.com/?fid=14943124697586370965)  
md5:2458b154b56df2add28ddd27c024d2c1

**Working:**

- Audio (HDMI, 3.5mm jack, USB microphones, bluetooth speakers/headsets, etc)
- Audio DAC (using GPIO DACs e.g. Hifiberry DAC+)
- Bluetooth
- Camera (using official Pi camera modules & UVC USB webcams)
- GPIO
- GPS (using external USB modules e.g. U-Blox 7)
- Ethernet
- Hardware accelerated graphics (V3D)
- HDMI display
- I2C
- IR remotes (using external GPIO IR modules e.g. TSOP4838)
- RTC (using external GPIO I2C modules e.g. DS3231)
- Sensors (using external GPIO I2C modules e.g. MPU6050, LSM6DS3 & LSM303DLHC accelerometer/gyroscope/magnetometer)
- Serial console (using external GPIO serial console adapters e.g. PL2303)
- SPI
- Touchscreen/multi-touch (USB touchscreens, Waveshare SPI touchscreens)
- USB (mouse, keyboard, storage, etc)
- USB-C (ADB, MTP, PTP, USB-tethering)
- Wifi
- Wifi tethering

**Not working:**

- Hardware video decoding & encoding (software decoding & encoding works)

**Issues:**

- Stock camera app is not working - many third party camera apps seem to work
- SELinux is in permissive mode
- and more...

**Sources:**

- [kernel](https://github.com/lineage-rpi/android_kernel_brcm_rpi/tree/lineage-18.1)

**Thanks:**

- Peter Yoon and everyone who has contributed to android-rpi
- Roman Stratiienko and GloDroid project for graphics fixes
- brobwind for bluetooth fixes
- Eric Anholt for V3D graphics driver
- Maxime Ripard for Pi 4 KMS driver
- Android-x86 project
- LineageOS team & everyone who has contributed to LineageOS 18.1

----

**How to install:**

1. Follow the official Raspberry Pi instructions for writing the image to the SD card ([Linux](https://www.raspberrypi.org/documentation/installation/installing-images/linux.md), [Mac](https://www.raspberrypi.org/documentation/installation/installing-images/mac.md), [Windows](https://www.raspberrypi.org/documentation/installation/installing-images/windows.md)).

**FAQ:**

Q: How to enable developer options?  
*A: Settings -> About tablet -> Click 'Build number' several times.*

Q: How to enable root access?  
*A: LineageOS no longer has built-in root management for applications. You can have root access via ADB after enabling Settings -> System -> Developer options -> Rooted debugging, SSH (see FAQ below), or serial console.*

*I have also created a separate TWRP flashable [su add-on](https://www.androidfilehost.com/?fid=17248734326145736362). After installing the add-on you can enable root access under Settings -> System -> Developer options -> Root access. You should keep this option disabled at all times when you are not using an app that explicitly requires root access.*

Q: How to enable advanced reboot options?  
*A: Settings -> System -> Gestures -> Power menu -> Advanced restart*

Q: How to find several Raspberry Pi specific settings options?  
*A: Settings -> System -> Advanced settings*

*Most options in this menu require you to reboot your device for the setting to take effect.*

Q: My display is not working. I can only see the rainbow screen but no Android boot animation. What should I do?  
*A: This build only supports HDMI displays that report supported resolutions using EDID. See [this page](https://www.raspberrypi.org/documentation/configuration/config-txt/video.md) under 'Which values are valid for my monitor?' to see how to check in Raspberry Pi OS which resolutions your display supports. 1920x1080 resolution is used by default with this build. You can try changing value in /boot/resolution.txt to use a different resolution that your display supports. Removing /boot/resolution.txt will try to use the preferred resolution for your display.*

Q: Settings -> Storage shows total system size of 7 GB. There's unallocated space on my sdcard. What should I do?  
*A: This is a 7 GB image, remaining space on your sdcard will remain unallocated. Easiest way to extend /data partition is to simply flash my [resize](https://www.androidfilehost.com/?fid=17248734326145708983) zip in TWRP.*

*Alternative option is to use e.g. GParted and extend /data partition (/dev/block/mmcblk0p4) to cover the unallocated space. Resizing the partition manually will break support for encrypting /data. Format /data in TWRP recovery (Wipe -> Format data) after resizing to leave required space for crypto footer.*

Q: Raspberry Pi doesn't have a power button. How to power off/reboot device?  
*A: Following keyboard keys work as Android buttons: F1 = Home, F2 = Back, F3 = Multi-tasking, F4 = Menu, F5 = Power, F11 = Volume down, and F12 = Volume up. You can also use one of many third party reboot applications.*

Q: How to create a DIY hardware power button?  
*A: You can send power button events by connecting GPIO21 to ground.*

![fritzing]({{ site.url }}/img/rpi4/LineageOS18/powerbutton.png)

*You can enable the feature by using a settings option found in Settings -> System -> Advanced settings -> Power button.*

*You can also use the DIY power button to boot the device to TWRP recovery. Press and hold the button while powering on the device until you see the TWRP screen.*

Q: How to enable audio through 3.5mm jack?  
*A: You can enable the feature by using a settings option found in Settings -> System -> Advanced settings -> Audio device.*

Q: How to use IR remote?  
*A: You can enable the feature by using a settings option found in Settings -> System -> Advanced settings -> Infrared remote.*

*You can place a keymap for your remote as /boot/rc_keymap.txt to be automatically loaded on boot (see [available keymaps](https://github.com/lineage-rpi/android_external_ir-keytable/tree/lineage-18.1/rc_keymaps) for reference).*

Q: How to use RTC?  
*A: You can enable the feature by using a settings option found in Settings -> System -> Advanced settings -> Real time clock.*

*System time is automatically read and set from the RTC on boot once you've enabled the feature. You need to write the system time you want to use to the RTC in rooted shell:*

```
hwclock -w -f /dev/rtc0
```

Q: How to use SSH?  
*A: You can start/stop the built-in SSH server by using a settings option found in Settings -> System -> Advanced settings -> SSH.*

*Android doesn't have user accounts with passwords so key based authentication is used with SSH instead. Necessary keys are generated on the first boot and you need to pull the private key to your computer (or alternatively you can push your own previously generated keys to the device). See Settings -> About tablet -> IP address for your device's IP address (192.168.0.100 is assumed here). Enable Android debugging & Rooted debugging under Settings -> System -> Developer options.*

```
adb connect 192.168.0.100
adb root
adb pull /data/ssh/ssh_host_rsa_key my_private_key
```

```
ssh -i my_private_key root@192.168.0.100
```

*It's recommended to disable adb after this.*

Q: How to boot from USB device?  
*A: <span style="color:#FF0000;">Warning</span>, this is still an experimental feature. Especially TWRP seems to have some issues with USB boot.*

1. Install EEPROM that supports booting from USB
2. Write image to your USB device as above
3. Mount the USB device on your computer and make following changes to /boot/config.txt under 'Boot device' section:
```
#dtoverlay=android-sdcard
dtoverlay=android-usb
```
4. Plug in the USB device to your Raspberry Pi, remove any sdcard, and boot

Q: How to boot to TWRP recovery?  
*A: You can boot to TWRP by selecting recovery option in Android power menu after enabling advanced restart options.*

*If mouse cursor doesn't appear, try replugging your mouse.*

Q: How to boot out of TWRP recovery?  
*A: You can boot out of recovery by simply selecting reboot to system option in TWRP.*

Q: How to update from previous LineageOS 18.1 build without losing data?  
*A:*

1. Boot to TWRP recovery with the build you want to keep the data (see FAQ)
2. Plug in an external USB storage device and select 'Backup'
3. Use 'Select Storage' to choose the USB device and 'Swipe to backup' (it's only necessary to backup the data partition so you can uncheck other partitions to speed up the process)
4. Write new LineageOS 18.1 image to the sdcard following installation instructions
5. Boot to TWRP recovery with the new build (see FAQ)
6. Select 'Restore' and find the backup you created from the USB device ('Select Storage')
7. Make sure you only have data selected as partitions to restore (uncheck other partitions if available) and select 'Swipe to Restore'
8. (Flash Google apps package/other add-ons you had previously installed)
9. Boot out of recovery (see FAQ)

Q: How to install Google apps?  
*A:*

1. Download [open_gapps-arm-11.0-pico-xxxxxxxx.zip](https://opengapps.org/?arch=arm&api=11.0&variant=pico) and save it to your device's internal storage or use an external USB drive
2. Boot to TWRP recovery (see FAQ)
3. Install open_gapps-arm-11.0-pico-xxxxxxxx.zip from your selected storage
4. Wipe -> Factory reset!
5. Boot out of recovery (see FAQ)

----

[Merged commits](https://review.lineageos.org/#/q/status:merged++branch:lineage-18.1+-project:%255E.*device.*+-project:%255E.*kernel.*,n,z) not mentioned in the changelog.

**20.7. changelog:**

- switch to using HDMI-CEC HAL
- update to Mesa 21.1.5
- update to Linux 5.4.132 kernel and patch known vulnerabilities (CVE-xxxx-xxxx, and more)
- Android security patch level: 5 July 2021 (merged)

**11.4. changelog:**

- add initial support for HDMI-CEC
- add built-in VNC server
- update to Mesa 21.0.2
- update to Linux 5.4.111 kernel and patch known vulnerabilities (CVE-xxxx-xxxx, and more)
- Android security patch level: 5 April 2021 (merged)

**14.2. changelog:**

- add support for LSM303DLHC accelerometer & magnetometer sensor
- add separate TWRP flashable su add-on (see FAQ)
- allow switching display off with power button
- add support for USB-C (ADB, MTP, PTP, USB-tethering)
- enable bluetooth tethering
- add settings option for mouse back button feature
- update to TWRP 3.5.0_9-0-KonstaKANG
- update to Mesa 20.3.4
- update to Linux 5.4.98 kernel and patch known vulnerabilities (CVE-xxxx-xxxx, and more)
- Android security patch level: 5 February 2021 (merged)

**4.1. changelog:**

- initial LineageOS 18.1 build
- add support for sensors (LSM6DS3 & MPU6050 accelerometer & gyroscope on I2C)
- add support for more serial USB GPS devices
- drop support for SwiftShader software renderer which also means dropping support for the official 7" touchscreen for now
- update to Mesa 20.3.2
- add option to switch between gbm and minigbm gralloc
- update to TWRP 3.4.0-2
- update to Linux 5.4.86 kernel and patch known vulnerabilities (CVE-xxxx-xxxx, and more)
- Android security patch level: 5 December 2020 (merged)

----

**Previous builds:**

- [AndroidFileHost](https://www.androidfilehost.com/?w=files&flid=321633)

----
