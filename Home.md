## Welcome to the EZ-WifiBroadcast wiki!  
**Read through this page before you start asking questions on the forum. **

### Download
These are direct download links to images.  

Latest version: v1.2 [EZ-wifibroadcast-1.2.zip](https://googledrive.com/host/0B8ke2EKPqvORMFAtSU1RbmxENHM/EZ-wifibroadcast-1.2.zip) Release notes and Changelog [is here](https://github.com/bortek/EZ-WifiBroadcast/wiki/v1.2-Release-Note)

Previous versions: v1.0 [ez-wifibroadcast-1.0.zip](https://googledrive.com/host/0B8ke2EKPqvORMFAtSU1RbmxENHM/ez-wifibroadcast-1.0.zip)


### Installation / Setup
- Download the image and unzip it
- Write it onto two (minimum 1GB) SD Cards. One for Transmitter part and another for Receiver part. See instructions on [this page](https://www.raspberrypi.org/documentation/installation/installing-images/) on how to write .img file on SD card.
- Insert each SD card into each Raspberry Pi and boot them up.


###Configuration
- Put SD Card in Windows computer or anything that has a text editor (Tablet, Smartphone) and edit wifibroadcast.txt


###Ground Recording
- USB Stick must contain a folder called "video"
- Plug USB stick to ground Pi before powering on
- Before disconnecting power, disconnect all USB sticks and wait a few seconds for the recording to be stopped, then power off


###Features
- Supports all Raspberry Pi models including Pi3, Pi Zero and also Odroid-W
- Supports the new Pi V2 cam
- Configuration can be done from Windows, no Linux knowledge required
- Support for 2.4Ghz band (incl. Channel 14) and all three 5Ghz bands on Ralink and Atheros cards
- Support for 2.3Ghz band on Atheros cards
- TXPower increased (and verified) for both Atheros and Ralink cards
- 2x transmit diversity support
- 6x receive diversity support using 3 cards (more should also be possible, just haven't tested that yet)
- Live RSSI display per card and defective blocks display
- Ground recording to USB stick
- Startup time reduced, now about 10-15 seconds depending on Pi model and Wifi cards used
- SD card reliability and general robustness tweaks (read-only filesystem, syslogging to SD disabled, etc.)

### Wifi cards and doungles
There is a list of Wifi cards and doungles on [this Wiki page](https://github.com/bortek/EZ-WifiBroadcast/wiki/Lis-of-Wifi-cards-and-doungles)

###Tested Raspberry Pi Hardware
- Pi 1 B+, Pi2 B+, Pi3 B+, Pi Zero 1.3, Odroid-W
- Official Pi V1 Cam ("V1.3" on the PCB), official Pi V2 Cam ("V2.1" on the PCB)

Take a look [at the images](https://github.com/bortek/EZ-WifiBroadcast/wiki/Images) of the hardware and their weights.

### Notes

TX: The CPUs on the Raspberry Pi 1 and Pi Zero are more or less maxxed out with standard settings (720p, 4.5Mbit bitrate, 8/4/1024 FEC). Two TX dongles, higher resolution/bitrate, or more error correction or smaller packet sizes will not work. Even if it seems to be working on first look, it can happen that latency suddenly raises if the CPU is loaded to much (in situations with high bitrate, like fast scene changes). I'd recommend a Pi2 or 3 as a TX because of this, it has enough headroom to not be worried about CPU usage at all.


RX: Raspberry Pi1 and Pi Zero have just about enough CPU power for one RX dongle, that's it. Multiple RX dongles, OSD, and/or ground-recording to memory stick will not work reliably. Get atleast a Pi2.

### References
- Discussion forum on rcgroups for this project [can be found here](http://www.rcgroups.com/forums/showthread.php?t=2664393)
- Here's a [long thread](http://www.rcgroups.com/forums/showthread.php?t=2454052) with more infos and experiences about befinitiv's (original) Wifibroadcast image.  
