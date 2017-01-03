## Welcome to the EZ-WifiBroadcast wiki!  
**Read through this page and other sub-pages before you start asking questions on the forum.**

### Download
These are direct download links to images.  

Stable version: v1.4 [EZ-Wifibroadcast-1.4.zip](https://drive.google.com/open?id=0BxyIDQpjwq9YWk9mLWR1b0JENDg) Release notes [is here](https://github.com/bortek/EZ-WifiBroadcast/wiki/Release-notes)


BETA version: v1.3 [EZ-Wifibroadcast-1.3beta.zip](https://docs.google.com/uc?id=0B8ke2EKPqvORazlSb3hxS0hOOTA&export=download) Release notes [is here](https://github.com/bortek/EZ-WifiBroadcast/wiki/Release-notes#ez-wifibroadcast-13-beta)

Stable version: v1.2 [EZ-wifibroadcast-1.2.zip](https://drive.google.com/uc?id=0B8ke2EKPqvORRmdUenJ0WmtFc1U&export=download) Release notes [is here](https://github.com/bortek/EZ-WifiBroadcast/wiki/Release-notes#ez-wifibroadcast-12)

Stable version: v1.0 [ez-wifibroadcast-1.0.zip](https://docs.google.com/uc?id=0B8ke2EKPqvORQU5RYi1EbEpQMUE&export=download)

BETA version (anemos fork based on Stable v1.2): [EZ_wbc_anemos_modified.v1.2beta.zip](https://docs.google.com/uc?id=0Bw6zbFkDkAtKcFNUOENqNzQ3SEk&export=download) Release notes and Changelog [is here](https://github.com/bortek/EZ-WifiBroadcast/wiki/v1.2beta-anemos-Release-Note)


### Installation / Setup
- Download the image and unzip it
- Write it onto two (minimum 2GB) SD Cards. One for transmitter Pi and another for Receiver Pi. See instructions on [this page](https://www.raspberrypi.org/documentation/installation/installing-images/) on how to write .img file on SD card.
- Insert each SD card into each Raspberry Pi and boot them up.


###Configuration
- Put SD Card in Windows computer or anything that has a text editor (Tablet, Smartphone) and edit wifibroadcast.txt and osdconfig.txt to suit your needs. For firt tests, do not change anything but frequency.


###Ground Recording
- Fly (Do _not_ plug in USB memory stick before)
- Plug-in USB memory stick after flight - recorded video will be shown and video/screenshots/telemetry will be saved
- Video recording time is limited to around 13mins with ramdisk temporary video storage. Longer recording times are possible with sdcard temporary storage, but this can currently cause video stuttering. Use a fast sdcard.


###Features
(applicable to the latest release)
- Supports Pi1B+, Pi2B+, Pi3B+, Pi Zero, Odroid-W, Pi V1 and V2 cam (RX Pi needs to be atleast a Pi2)
- max. possible resolutions (depending on cam used):
1280x720p 60fps
1296x972p 42fps
1640x922p 40fps
1920x1080p 30fps
- max. possible video bitrate about 12Mbit
- Latency ~140ms with 720p 48fps default settings, minimum possible latency roughly around 110ms
- Support for 2.3/2.4/2.5Ghz bands and 5.2Ghz to 5.8Ghz bands
- 2.4Ghz on 3dbi omni antennas: ~1km range with ~70mw wifi sticks, about 2km with ~300mW high-power cards
- 5Ghz on 3dbi omni antennas: ~250m range with 25mW wifi sticks, ~1km range with ~300mW high-power cards
- Configuration can be done from Windows, no Linux knowledge required
- Supports different configuration profiles selectable on the field via jumpers or DIP switches
- Forwarding of video stream and telemetry data to 2nd display via: USB Tethering, Wifi Hotspot, Ethernet, Wifibroadcast relay mode
- Fully dynamic and automatic detection of 2nd display, just plug it in or connect via Hotspot and it'll work
- 2 wifi sticks transmit diversity on two different frequencies supported for bulletproof video link
- 3 wifi sticks receive diversity support for Atheros, 5 wifi sticks receive diversity support for Ralink
- Integrated OSD with support for Mavlink (not bi-directional), Frsky, LTM, NMEA GPS
- .AVI Ground recording and .PNG screenshots automatically saved to USB stick
- Quick startup, about 10 seconds until video is shown
- No issues as with standard wifi, no disconnection, video freeze etc.
- Graceful handling of signal degradation, no sudden loss of video
- Live and responsive RSSI display with defective blocks and packetloss display
- Handling similar to analog gear, just switch on and fly
- Smooth and stutter-free video (thanks, mmormota)
- Video reception is very stable even in difficult multipathing environments, no constant glitching like with analog
- No expensive and large circular antennas required
- OSD overlay rendered on the receiver will stay clear and functional even if video is too bad to fly
- SD card reliability and general robustness tweaks (read-only filesystem, syslogging to SD disabled, etc.)
- Debug logs and screenshot will be saved to sdcard in case of errors
- RC over wifibroadcast via Joystick (not much tested yet)


### Wifi cards and dongles
There is a list of Wifi cards and dongles on [this Wiki page](https://github.com/bortek/EZ-WifiBroadcast/wiki/List-of-Wifi-cards-and-doungles)

### Screens/Monitor
Virtually any screen/monitor connected to the HDMI port on your Pi should work. Besides that the following displays have been tested and work:
 - Samsung 32 inch TV connected via HDMI to Pi.
 - Pi Official Screen connected to CSI port on your Pi. Resolution 800x480.
 - An LCD module from old 17 inch laptop with eBay driver [(for example this)](http://www.ebay.com/itm/HDMI-VGA-2AV-Lcd-controller-Board-VS-TY2662-V1-for-LCD-panel-Only-driver-board-/181596796562?hash=item2a48033692:g:TGEAAOSwQJhUdwFZ) using 1920x1080 to HDMI on Pi. Default FPS.
 - Goggles One 1080p display (needs to be set to fixed 1080p resolution in config.txt)
 - Headplay HD

Please note that the monitor has to be connected and powered before the Pi is powered because the auto-detection only works at start-up. You can define you monitor resolution in config.txt statically though to be able to plug you monitor after the Pi is already running.

###Tested Raspberry Pi Hardware
- Pi 1 B+, Pi2 B+, Pi3 B+, Pi Zero 1.3, Odroid-W
- Official Pi V1 Cam ("V1.3" on the PCB), official Pi V2 Cam ("V2.1" on the PCB)

Take a look [at the pictures](https://github.com/bortek/EZ-WifiBroadcast/wiki/Pictures) of the hardware and their weights.

### Notes
TX: The CPUs on the Raspberry Pi 1 and Pi Zero are more or less maxxed out with standard settings (6Mbit bitrate, 8/4/1024 FEC). Two TX dongles, higher resolution/bitrate, or more error correction or smaller packet sizes will most likely not work. Even if it seems to be working on first look, it can happen that latency suddenly raises if the CPU is loaded to much (in situations with high bitrate, like fast scene changes). Although many people successfully use a Pi Zero as a TX, if space and weight is no issue, a Pi2 or 3 is recommended.


RX: Raspberry Pi1 and Pi Zero are not supported anymore from version 1.3 on. Use a Pi2 or Pi3.

### References
- Discussion forum on rcgroups for this project [can be found here](http://www.rcgroups.com/forums/showthread.php?t=2664393)
- Here's a [long thread](http://www.rcgroups.com/forums/showthread.php?t=2454052) with more infos and experiences about befinitiv's (original) Wifibroadcast image.  
