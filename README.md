# Reception Screen with Raspberry Pi
How to set up a reception screen with Raspbian Pixel on a Raspberry pi

## Hardware
* [Raspberry Pi Model 3 B Starter Kit](https://www.amazon.de/Vilros-Raspberry-Pi-Complete-Kit-Enthalt/dp/B01DC6MKAQ/ref=sr_1_5?s=computers&ie=UTF8&qid=1483031731&sr=1-5&keywords=raspberry+pi+3), containing
 * Raspberry Pi 3 Model B
 * Raspberry Pi Enclosure Case (Clear)
 * 16GB Sandisk class 10 Micro Sd Card Preloaded with NOOBS 
 * SD card Adapter 
 * 2500 mA EU Micro USB Power Supply 
 * High Quality HDMI Cable 
 * Heatsink for Raspberry Pi - Set of 2 Heat Sink 
* USB Keyboard and Mouse of your choice
* [Huawei E3531 SurfStick (HSPA+, USB, HSUPA, EDGE/GPRS)](https://www.amazon.de/Huawei-E3531-SurfStick-HSPA-HSUPA-Weiß/dp/B00L64LSWS?th=1)
* Full HD Screen of your choice (HDMI, resolution 1920x1080)

## Software
* [Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/)

## Set up Raspberry Pi
* Due to the Starter Kit, the Raspberry Pi is ready to use
* Just insert the preloaded sd card, plug in the keyboard and mouse, connect the HDMI cable to the screen and the power supply to the outlet
* Follow the onscreen instructions until all parameters have been configured
* Connect the Raspberry Pi to a wifi network
* Update the operating system (OS) by opening terminal and prompting:
```
sudo apt-get update
sudo apt-get dist-upgrade
```
* Reboot
* Done

## Rotate screen
* To run your reception screen in vertical position (portrait mode), rotate the screen by editing the file ```/boot/config.txt```
* Open terminal and enter ```sudo nano /boot/config.txt```
* Add one of the following extensions at the bottom:

| Command        | Effect       |
| ------------- |:-------------:|
| ```display_rotate=1``` | rotates  90 degrees |
| ```display_rotate=2``` | rotates 180 degrees |
| ```display_rotate=3``` | rotates 270 degrees |

* Save the file
* Reboot
* Done

## Remove black borders
* Due to a black frame around the content of the screen, it's helpful to remove those borders (overscan signal)
* Edit the file ```/boot/config.txt```
* Open terminal and enter ```sudo nano /boot/config.txt```
* Remove ```#``` in ```#disable_overscan=1``` to uncomment
* Add ```#``` in front of ```overscan_left=10```, ```overscan_right=10```, ```overscan_top=15``` and ```overscan_bottom=15``` if necessary
* Save the file
* Reboot
* Done

## Content for the screen
### Google Sheets
* https://docs.google.com/presentation
* Page set up to resolution of screen (1920x1080 or 1080x1920)
* design your screen
* publish to the web, copy link

## Configure autostart of chromium at launch


## Auto-Refresh Chromium


## No Sleep Setting

## Hide Cursor

## Open Tasks
* [ ] Set up SurfStick
