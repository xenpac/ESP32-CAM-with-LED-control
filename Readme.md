# Camera Webserver ESP32-CAM ESP32-WROVER-B AI-THINKER Board with LED control

## Overview

This a stripped down version of the esp-who camera web server example at: http://github.com/espressif/esp-who
I added the control of the onboard high-power LED to be used as flash for snapshots or illumination for streaming.
It does not use a PWM, so its ON or OFF.
The changes are all in app_http.c

Hardware: ESP32-CAM AI-THINKER Board with OV2640, that nice little CAM board sold everywhere.

**Removed:**
- face recognition, also removed related code in source (app_httpd.c).  
- set Release Version in Menuconfig for max optimize. (debug info still output on serial).

**Added:**
- LED control via "Facedetection" Control. (On/Off)
- Flash control for snapshot via "Face Recognition" Control. ie. both must be active, LED will turn off and only flash on snapshot.

corrected an error at line:88 in app_httpd.c, filter changes to filter->values  .

Future work will be to integrate the camera as a cheap webcam to be used with linux motion.

It looks, the camera is working stable now.

The default stream-resolution can be specified in app_camera.c, line 69.


## Camera Web interfaces via http:

Webpage with config settings: 192.168.1.4   (this is an example ip on the LAN)

The following 2 interfaces only work, if not enabled in the webpage at the same time. So only one instance can be running!!

- jpeg Streaming interface (resolution asto settings on Webpage) : 192.168.1.4:81/stream

- single jpeg capture image: 192.168.1.4/capture    (now supports optional flash!)


## Project:

It is assumed you are familiar with setting up and using the esp32 environment.

You need ESP-IDF  from: https://github.com/espressif/esp-idf
The crosscompiler from: https://dl.espressif.com/dl/xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar.gz

I compiled the project using Ubuntu with crosscompiler and make.

Goto cam_server directory and edit the sdkconfig file to update your wifi AP settings.

Then type "make" to compile the project.

It also possible to use the Arduino IDE.

The compressed webpage is in:..cam_server/cam_server/main/include/camera_index.h


