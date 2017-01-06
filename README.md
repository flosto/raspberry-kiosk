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
* Connect the Raspberry Pi to a wifi or ethernet network
* Update the operating system (OS) by opening terminal and prompting:
```
sudo apt-get update
sudo apt-get dist-upgrade
```
* Reboot
* Done

## Set up Huawei SurfStick
* Unconnect your wifi or ethernet network 
* Plug in a SIM card
* Connect the SurfStick to any USB port of your Raspberry Pi
* The os detects the stick automatically
* Open Chromium and enter '192.168.1.1' to proceed to the setup panel
* Enter your PIN code and deactivate PIN request in settings
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
### Google Slides
* A suitable way to quickly design your reception screen is to use Google Slides (as a part of Google Docs), to publish the file to the web and to open in in Chromium on your Raspberry Pi
* Go to https://docs.google.com/presentation, login with your Google credentials and start creating
* Manually set up the page to the resolution of your screen (1920x1080 in landscape mode or 1080x1920 in portrait mode) at "File -> Page setup..."
* Select "File -> Publish to the web" to create an unique link (copy this one) to your slides and configure auto-advance and a restart as well

### Configure autostart of chromium at launch
* To automatically start your kiosk screen at Raspberry's launch edit the autostart settings in ```home/pi/.config/lxsession/LXDE-pi/autostart``` (if "pi" is your default user) as follows
* Open terminal and enter ```sudo nano ~/.config/lxsession/LXDE-pi/autostart```
* Add ```@chromium-browser --noerrdialogs --disable-session-crashed-bubble --disable-infobars --kiosk http://your.url```
* Set the copied link to Google Slides instead of "http://your.url"
* Save the file
* Reboot
* Done

### Auto-Refresh Chromium
* When you set your own website as kisko screen in Chromium, just add an autorefresh command like ```<meta http-equiv=”refresh” content=”1800”>``` to the html source code
* If you run external content (like Google Slides) and don't want to build a html site with an inline frame, just install the smart plugin [Super auto Refresh](https://chrome.google.com/webstore/detail/super-auto-refresh/kkhjakkgopekjlempoplnjclgedabddk) to your Chromium browser
* Open the target page in Chromium and set your default refresh interval, "Super Auto Refresh" will remember this setting

## No Sleep Setting
* To avoid any screen blanking disable the screensaver and power saving settings in autostart settings ```home/pi/.config/lxsession/LXDE-pi/autostart``` (if "pi" is your default user)
* Open terminal and enter ```sudo nano ~/.config/lxsession/LXDE-pi/autostart```
* Uncomment the screensaver setting by adding a ```#``` in front of ```@xscreensaver -no-splash```
* Add the following commands
```
@xset s off
@xset -dpms
@xset s noblank
```
* Save the file
* Reboot
* Done

## Hide Cursor
* Your kiosk screen looks even better without the disturbing mouse cursor
* Install "Unclutter"
* Open terminal and enter ```sudo apt-get install unclutter```, the installation starts automatically
* Open terminal and enter ```sudo nano ~/.config/lxsession/LXDE-pi/autostart```
* Add ```@unclutter -idle 0.1 -root```
* Save the file
* Reboot
* Done

## Auto Shutdown
* To shut down your Raspberry Pi automatically add a short cronjob command
* Open terminal and enter ```sudo crontab -e```
* Add ```@reboot /sbin/shutdown -h 19:00``` to shutdown your Raspberry Pi at 7 p.m.
* Set your preferred time in 24 hour format 
* Save the file
* Reboot
* Done
* **Hint:** Most displays provide an auto-off setting, so your screen will also turn off automatically after several minutes when the HDMI input is switched off

## Sources
* https://www.raspberrypi.org/blog/introducing-pixel/
* https://www.danpurdy.co.uk/web-development/raspberry-pi-kiosk-screen-tutorial/
* https://github.com/basdegroot/raspberry-pi-kiosk
* http://www.opentechguides.com/how-to/article/raspberry-pi/28/raspi-display-setting.html
* https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=52759
* http://tutorials-raspberrypi.de/raspberry-pi-gsm-modul-mobiles-internet/
* https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=61745
