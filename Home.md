## Welcome to the EZ-WifiBroadcast wiki!  

### Download
These are direct download links to images.  

Latest version: v1.2 [EZ-wifibroadcast-1.2.zip](https://googledrive.com/host/0B8ke2EKPqvORMFAtSU1RbmxENHM/EZ-wifibroadcast-1.2.zip)

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


###Wifi Cards:
You have a lot of choice. All wifi cards with one of the following chipsets should work:

Atheros AR9271, Atheros AR9280, Atheros AR9287

The following Ralink cards supported: 
 - RT2070, RT2770, RT2870, RT3070, RT3071, RT3072, RT3370, RT3572, RT5370, RT5372, RT5572

However, there might be whatever small issues that prevent those cards from working, so if you want to play it safe, choose one of the cards that have been tested by different people and definitely work:

- CSL 300Mbit Stick (2.4/5Ghz, Diversity, RT5572 chipset)
- Alfa AWUS036NHA (2.3/2.4Ghz, high power, Atheros AR9271 chipset)
- TPLink TL-WN722N (2.3/2.4Ghz, Atheros AR9271 chipset)
- ALFA AWUS051NH v2 (2.4Ghz/5Ghz, high power, Ralink RT3572 chipset)

This ones also looks promising for high power needs:
- Alfa AWUS052NH (2.4Ghz/5Ghz, Diversity, high power, RT3572 chipset)

On the other hand, if everybody gets the same cards, we'll never find out which other ones work. There are also very small and lightweight RT5370 cards available in china shops for under 4$. Aliexpress for example has a lot of cheap wifi cards in general. It would be nice if you report back your findings in case you tried a wifi card that is not listed here.


Here's a [long thread](http://www.rcgroups.com/forums/showthread.php?t=2454052) with more infos and experiences with Wifibroadcast: