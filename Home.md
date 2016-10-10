## Welcome to the EZ-WifiBroadcast wiki!  
**Read through this page and [FAQ page ](https://github.com/bortek/EZ-WifiBroadcast/wiki/FAQ)before you start asking questions on the forum.**

### Download
These are direct download links to images.  

BETA version: v1.3 [EZ-Wifibroadcast-1.3beta.zip](https://docs.google.com/uc?id=0B8ke2EKPqvORazlSb3hxS0hOOTA&export=download) Changelog [is here](https://github.com/bortek/EZ-WifiBroadcast/wiki/v1.3BETA-Changelog)

Stable version: v1.2 [EZ-wifibroadcast-1.2.zip](https://drive.google.com/uc?id=0B8ke2EKPqvORRmdUenJ0WmtFc1U&export=download) Release notes and Changelog [is here](https://github.com/bortek/EZ-WifiBroadcast/wiki/v1.2-Release-Note)

Previous version: v1.0 [ez-wifibroadcast-1.0.zip](https://docs.google.com/uc?id=0B8ke2EKPqvORQU5RYi1EbEpQMUE&export=download)

BETA version (anesmos fork based on Stable v1.2): [EZ_wbc_anemos_modified.v1.2beta.zip](https://docs.google.com/uc?id=0Bw6zbFkDkAtKcFNUOENqNzQ3SEk&export=download) Release notes and Changelog [is here](https://github.com/bortek/EZ-WifiBroadcast/wiki/v1.2beta-anemos-Release-Note)


### Installation / Setup
- Download the image and unzip it
- Write it onto two (minimum 2GB) SD Cards. One for Transmitter part and another for Receiver part. See instructions on [this page](https://www.raspberrypi.org/documentation/installation/installing-images/) on how to write .img file on SD card.
- Insert each SD card into each Raspberry Pi and boot them up.


###Configuration
- Put SD Card in Windows computer or anything that has a text editor (Tablet, Smartphone) and edit wifibroadcast.txt and osdconfig.txt to suit your needs.


###Ground Recording
- USB Stick must contain a folder called "video"
- Plug USB stick to ground Pi before powering on
- Before disconnecting power, disconnect all USB sticks and wait a few seconds for the recording to be stopped, then power off

Handling has changed from Version 1.3 on (Video will be temporarily saved to RAM disk during flight, this limits recording time to around 15 minutes)
- Fly (Do _not_ plug in USB memory stick before)
- Land
- Plug USB memory stick
- Wait until video, screenshots and telemetry is saved (Message "safe to remove USB memory stick" appears)


###Features
- Supports all Raspberry Pi models including Pi3, Pi Zero and also Odroid-W (Older Raspi A+ models untested though)
- Supports the new Pi V2 cam
- Configuration can be done from Windows, no Linux knowledge required
- Support for 2.4Ghz band (incl. Channel 14) and all three 5Ghz bands on Ralink and Atheros cards
- Support for 2.3Ghz band on Atheros cards
- TXPower increased (and verified) for both Atheros and Ralink cards
- 2x transmit diversity support
- 6x receive diversity support using 3 cards (more should also be possible, just not tested yet)
- Live RSSI display and defective blocks display per card
- Video Ground recording to USB stick
- Screenshot recording on the ground
- Startup time reduced, about 10-15 seconds depending on Pi model and Wifi cards used
- SD card reliability and general robustness tweaks (read-only filesystem, syslogging to SD disabled, etc.)


### Wifi cards and doungles
There is a list of Wifi cards and doungles on [this Wiki page](https://github.com/bortek/EZ-WifiBroadcast/wiki/List-of-Wifi-cards-and-doungles)

### Screens Monitor
Virtually any screen/monitor connected to the HDMI port on your Pi should work. Besides that the following displays have been tested and work:
 - Samsung 32 inch TV connected via HDMI to Pi.
 - Pi Official Screen connected to CSI port on your Pi. Resolution 800x480.
 - An LCD module from old 17 inch laptop with eBay driver [(for example this)](http://www.ebay.com/itm/HDMI-VGA-2AV-Lcd-controller-Board-VS-TY2662-V1-for-LCD-panel-Only-driver-board-/181596796562?hash=item2a48033692:g:TGEAAOSwQJhUdwFZ) using 1920x1080 to HDMI on Pi. Default FPS.
- Goggles One 1080p display (needs to be set to fixed 1080p resolution in config.txt)
- Headplay HD

###Tested Raspberry Pi Hardware
- Pi 1 B+, Pi2 B+, Pi3 B+, Pi Zero 1.3, Odroid-W
- Official Pi V1 Cam ("V1.3" on the PCB), official Pi V2 Cam ("V2.1" on the PCB)

Take a look [at the pictures](https://github.com/bortek/EZ-WifiBroadcast/wiki/Pictures) of the hardware and their weights.

### Notes

TX: The CPUs on the Raspberry Pi 1 and Pi Zero are more or less maxxed out with standard settings (720p, 5.5Mbit bitrate, 8/4/1024 FEC). Two TX dongles, higher resolution/bitrate, or more error correction or smaller packet sizes will most likely not work. Even if it seems to be working on first look, it can happen that latency suddenly raises if the CPU is loaded to much (in situations with high bitrate, like fast scene changes). Although many people successfully use a Pi Zero as a TX, if space and weight is no issue, a Pi2 or 3 is recommended.


RX: Raspberry Pi1 and Pi Zero have just about enough CPU power for one RX dongle, that's it. Multiple RX dongles, OSD, and/or ground-recording to memory stick will not work reliably. A Pi2 or Pi3 is recommend.

### References
- Discussion forum on rcgroups for this project [can be found here](http://www.rcgroups.com/forums/showthread.php?t=2664393)
- Here's a [long thread](http://www.rcgroups.com/forums/showthread.php?t=2454052) with more infos and experiences about befinitiv's (original) Wifibroadcast image.  
