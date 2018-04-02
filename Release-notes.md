## Release notes

### 2018-04-02 EZ-Wifibroadcast 1.6 RC6 (release candidate)
- Added warning message when using unsupported or experimental wifi chipsets
- Uplink RSSI info transmission robustness improved
- Bugfix: Wrong size for memcpy in rx_rc_telemetry (thanks dino_de)
- Bugfix: MT7601 chipset support
- Bugfix: Telemetry uplink "external" (for 433mhz mavlink radios or LRS mavlink uplink) should work now
- Bugfix: OSD did not start when disabling "SYS" display in config
- Bugfix: OSD did not start when selecting LTM or FRSKY telemetry
- Bugfix: OSD did not re-appear after saving video to USB memory stick
- OSD: Smartport telemetry protocl support added (thanks markus1234)
- OSD: Higher rendering speed, less CPU utilization and custom fonts due to Paeryn's OpenVG library
- OSD: Correct text and graphics scaling for all display resolutions from 640x480-1920x1080, 4:3,5:4,16:9,16:10
- OSD: 50+ different TrueType fonts to choose from, custom fonts can be added
- OSD: Fill- and outline-color can be configured as well as transparency
- OSD: Outline thickness can be configured
- OSD: Configurable global scaling as well as scaling of every element
- OSD: Element text replaced by symbols
- OSD: RSSI display changes: Smoother/less "quirky" display of RSSI
- OSD: RSSI display changes: Display now shows lowest value (easier to detect end of range, more safe)
- ODS: Uplink and R/C RSSI/packetloss display combined
- OSD: Packetloss counters get reset with TX restart
- OSD: Graphical packetloss/FEC display
- OSD: Armed/disarmed state integrated into flight mode display
- OSD: Elements now show red/green status (e.g. home symbol is red and turns green when home location is set)
- OSD: Heading data source for compass and home arrow configurable (GPS/course-over-ground or magnetometer)
- OSD: LTM home position taken from LTM O-Frame
- OSD: Various smaller changes
- OSD: Various code cleanups


### 2018-02-12 EZ-Wifibroadcast 1.6 RC5 (release candidate)
- Bugfix: Telemetry TX/RX in 1.6RC4 stopped after 65535 packets
- Bugfix OSD: Home arrow pointing in wrong direction
- OSD: Position of all OSD elements can be configured
- OSD: Text positioning/scaling improved for lower resolutions
- OSD: Smoother AHI, compass, speed/alt ladders and home arrow
- OSD: Home direction indicator added to compass ladder
- OSD: Mavlink RC RSSI display added
- OSD: Mavlink disarm/arm display added
- OSD: Mavlink flightmode display added
- OSD: Mavlink airspeed, baroalt and climb m/s display added
(Thanks to basti, schs, fritzwalter123)


### 2018-02-11 EZ-Wifibroadcast 1.6 RC4 (release candidate)
- Live CPU load and temperature display for both TX and RX Pi
- Live display of injection time and errors
- Telemetry rx efficiency and robustnuss improvements
- Transmit power configuration simplified
- RSSI/packetloss and CPU load/temperature forwarding for FPV_VR 2018 app added (experimental, not complete yet)
- Bugfix: Missing mavlink messages due to outdated Mavlink library
- Bugfix: RTL8812 cards did not work for Wifihotspot in 1.6RC3 due to missing driver
- Bugfix: Mediatek MT7601 cards did not work in 1.6RC1-1.6RC3 due to missing driver
- Moved settings in Wifibroadcast-1.txt to the correct section (TX/RX/COMMON)
- SPI userspace device modules added to kernel (for experimenting)
- Debug log feature for TX (writes debug.txt to sdcard)
- More telemetry debug logging
- Undervoltage warnings for RX added, warnings improved for TX
- Measured kbitrate display moved to OSD to keep video stream clean
- Various smaller code and script cleanups

### 2017-12-27 EZ-Wifibroadcast 1.6 RC3 (release candidate)
- New feature: RSSI/packetloss graphing and logging
- New feature: integrated airodump-ng wifi scanner
- Increased wifibroadcast-1.txt GPIO config combinations from 8 to 16
- Reverted back to stty serialport initialisation to fix issue with heartbeats getting lost
- Rewritten telemetry rx: Should fix out-of-order delivery and packetloss for telemetry
- Changed manual bitrate setting to kbit/s instead of bit/s
- Measured bitrate display in video stream can be disabled in wifibroadcast-1.txt
- Added debug option to wifibroadcast-1.txt
- Removed confusing bitrate display during startup on RX
- Changed txpower for Atheros back to 58 (was 56 accidentally in 1.6RC1 and RC2)
- Changed Atheros Thresh62 parameter to 26
- Added configurable mavlink forwarder: cmavnode or mavlink-routerd
- cmavnode.conf moved to boot partition for easier access
- Display error message in case of syntax errors in osdconfig.txt
- Added various USB webcam drivers to the kernel (for experimenting)
- raspivid default intrarefresh changed to "-if both"



### EZ-Wifibroadcast 1.6 RC2 (release candidate)
- telemetry downlink fixes
- replaced cmavnode with mavlink-routerd (supports UDP and TCP)
- more debug logging
- Version on boot-up and in readme.txt updated to reflect rc status



### EZ-Wifibroadcast 1.6 RC1 (release candidate)
- Kernel, Pi firmware and Pi userland updated (Kernel 4.9.35, Raspbian 2017-07-05, Pi0W should work out-of-the-box)
- Latency lowered slightly (Kernel 4.9.35 improves scheduling and jitter, wbc rx -d 1 works again)
- Mavlink R/C support (thanks dino_de!)
- Graupner/JR SUMD R/C support
- Flysky IBUS R/C support
- Multiplex SRXL / XBUS Mode B R/C support
- Support for RTL8192CU cards added (only RX, not tested, for experimenting)
- Support for RTL8812AU cards added (only RX, not tested, for experimenting)
- Bitrate measuring on TX, simplifies FEC and bitrate settings, allows for higher bitrates
- Bitrate display on RX, shows bitrate set on TX as well as live received bitrate on RX
- New downlink and Uplink tx/rx should improve telemetry down- and uplink considerably
- Frame header format optimized for minimum overhead (makes the frame format incompatible with v1.5)
- OSD renders only (and instantly) when receiving attitude frames, artificial horizon is smoother and causes less CPU/GPU load
- More efficient tx_rawsock using raw sockets instead of libpcap injection, higher bitrates possible with Pi0/1
- CPU clock lowered to 900Mhz and overvoltage lowered to "3" for less heat and power consumption
- Atheros short preamble mode: Improves CTS protection and R/C link, allows to use 11 Mbit datarate "long-range" mode
- Atheros medium access parameter THRESH62 lowered from 28 to 24: should improves R/C link
- Atheros medium access parameters SIFS, AIFS, CWMIN, CWMAX, etc. are configurable now
- Increased max. framesize, Atheros wbc payload 1550 bytes, Ralink wbc payload 2278 bytes
- Support for 802.11b 11mbit and 5.5mbit modes added (lower quality/higher range)
- Support for CDC ACM added (for Pixhawk USB port)
- Support for BCM2385 I2C and Toshiba TC358743 added (not tested, for B101 experimenting)
- Made video UDP port configurable (for Missionplanner)
- Cosmetic fix: cat write error message removed when ramdisk full
- Cosmetic fix: socat init messages removed
- Cosmetic fix: German "O" for "Ost" in OSD compass changed to english "E" for "East" 
- Cosmetic fix: OSD RC_RSSI option re-named to WBC_RC_RSSI
- Bug fix: Serial telemetry data corruption due to wrong stty settings
- Bug fix: Pi1A+ turned out not to be 100% stable at 1000MHz CPU clock
- Bug fix: serial port (for telemetry) did not work on the new Pi0W


### EZ-Wifibroadcast 1.5
- New feature: Bi-directional Mavlink telemetry support (both over wbc and external devices e.g. 3DR dongles or LRS with telemetry) (untested!)
- New feature: Telemetry output on Rx Pi serialport for antenna tracker etc.
- New feature: RSSI forwarding to FP_VR android app
- New feature: RTP video stream forwarding to allow video display in Tower app and QGroundControl app
- New feature: R/C RSSI and lost packets display added to OSD
- New feature: CTS protection mode (only for Atheros), improves link quality in environments with wifi interference
- New feature: Telemetry logging to textfile for later review and debugging
- New feature: OSD text size can be scaled now, outlines can be disabled for better readability on low-res displays
- New feature: OSD: GPS/Baro altitude and groundspeed/airspeed can be configured (untested!)
- New feature: Transmit power for Atheros cards can be set in /etc/modprobe.d/ath9k_hw.conf now (thanks to eosbandi)
- Bugfix: Typo in OSD frsky telemetry parser
- Bugfix: Wifihotspot would not work when USB memory stick plugged during boot-up
- Bugfix: Wifihotspot 2.4GHz Channels 12 and 13 did not work
- Cleaned up OSD/telemetry configuration, no more configuring blocksize etc.
- Uplink, dual tx mode and R/C link functionality re-written and improved (untested!)
- Configuration file clean-up, less options, easier to configure
- Wifi medium access timing changed (less agressive, may behave better in environments with wifi interference, untested though)


### EZ-Wifibroadcast 1.4
- Display of good/lost packets to OSD for easier identification of interference
- dbm display now grows/shrinks depending on signal strength
- Default wifi bitrate reduced to 18mbit for ~3db higher sensitivity
- Default video bitrate increased to 6Mbit for higher video quality
- Default transmit power for Ralink cards is increased by 1db because of 18mbit wifi bitrate
- added 802.11n and 802.11b bitrates for Atheros cards
- Selectable configuration profiles via GPIO jumpers/switches
- lots of changes to the scripts to allow for fully automatic and dynamic detection of secondary display devices
- Forwarding of video stream and telemetry data to 2nd display via: USB Tethering, Wifi Hotspot, Ethernet, Wifibroadcast relay mode
- Bugfix: Some USB memory sticks were not correctly detected
- Bugfix: Video is now saved with correct fps if not using 48fps default setting
- Bugfix: With two or three Atheros cards, one wouldn't come up or receive no packets sometimes, should work stable now for up to three cards
- Bugfix: Ralink drivers caused a badblock every 10-20 seconds with Alfa AWUS051NH/052NH and other RT3572 based cards
- Disabled LED blinking on Atheros cards to avoid potential stability issues
- Raspberry Firmware upgraded to latest Raspbian release version
- RX overtemperature and undervoltage are now displayed with meaningful symbols
- Debug logs and screenshot will be saved to sdcard in case of errors
- Long recording times possible again. Use with caution, may lead to video stuttering or freeze!
- Recorded video will be played back while saving to USB
- Cosmetic fixes and quiet mode

### EZ-Wifibroadcast 1.3 beta
- Startup scripts completely rewritten. They run on TTY1-TTY10 now and show if transmission/reception of video and telemetry is running, status info on wifi cards, memory sticks and android device, etc. etc. (not perfect yet, but should work)
- 2.5-2.7Ghz support for Atheros cards (Untested. Check which frequencies are allowed in your country and use some common-sense!)
- New raspberry firmware which fixes OSD freeze-up
- support for 2 TX cards for bullet-proof video link (tested, but needs more testing)
- Included mmormota's stutter-free hello_video.bin versions (seems to work great, the -sleep versions need testing though)
- USB tethering supported for display on android device (untested, but should work)
- Made Rangarid's OSD configurable (see osdconfig.txt)
- Added support for receiving telemetry data on RX serial port (for people with UHF telemetry transmission for example)
- Added support for serial data uplink (untested, may need manual fixing)
- Added support for RC over wifibroadcast via Joystick (tested, but needs more testing)
- Added screenshot support on RX
- Added dbm and packet/block display for video and telemetry data streams to OSD
- Re-written USB memory stick logic completely to fix stuttering issue when recording:
Video/Screenshots/Telemetry will now be saved to USB stick by simply plugging in the
memory stick _after_ flight
- OSD can be made translucent
- OSD update interval configurable
- Linux timer frequency increased to 1000Hz for less jitter and less badblocks in cases when one adapter has bad reception
- Fixed DNS resolv.conf not being updated by dhcp
- Login cleaned-up, no need to cancel stuff running on the console etc.
- Give error message and refuse to run when unsupported frequency is configured instead of silently falling back to the
lowest supported channel (to make sure users don't accidently use an undesired frequency)
- Check_alive function added which automatically restarts hello_video.bin in case it should crash

### EZ-Wifibroadcast 1.2
- Befi's and Rangarid's OSD integrated
- Raspbian Update to Kernel 4.11 and latest Raspberry Firmware / Userland (Pi Zero/V2 Cam)
- Display of configured Frequency and FEC-Parameters at the bottom of the screen
- Ralink: Different bitrates for video and telemetry possible
- Ralink: Wifi bitrate can be configured via wifibroadcast.txt
- Atheros: Wifi bitrate can be configured via module parameter
- Ralink: TXPower can be configured via module parameter
- Supports V2 Cam 1280x720 up to 75fps, 1640x922 up to 48fps
- AIFS/Backoff parameters tweaked, Atheros chipsets now give about 10-15% more throughput, Ralink about 3%
- Atheros LED behaviour tweaked, blinks faster now, is "more sensitive"
- CPU/GPU/RAM overclocked and force_turbo activated for less/more stable Latency and higher possible bitrate on Pi1/Zero
- USB Ethernet Tethering support activated in Kernel (for smartphones)
- DHCP enabled on Ethernet interfac (system will contact the DHCP server with "wifibroadcast-tx" or "wifibroadcast-rx" hostname)
- Bash-prompt shows ro/rw status of the filesystem, macros ("rw","ro") added for quick switching
- Reduced TXPower for Atheros chipsets slightly (just to be on the safe side)
- Reduced TXPower for Ralink chipsets to default level
- Patched Atheros Firmware for additional Atheros Chipsets (AR9287, e.g. TPLink 822N V2)
- TX shows some status infos after startup
- video.c changed to 240fps for less latency/jitter
- addedd fflush to rx prozess (just to make sure ...)
- disabled Systemd journal daemon (used up CPU ...)
- Kept software, tools and libs etc. in the image, should make modifying or adding own features to the image easier
- Support for two TX wifi dongles. Experimental right now, not in the config file, has to be configured manually in Linux
- Bugfix: Potential rapidly raising latency, stuttering image on Pi1/Zero in some cases: overclocked CPU/GPU/RAM, force_turbo=1, enabled performance governoer, reduced bitrate to 4.5Mbit, video.c patched to 240fps, added fflush in RX process, removed systemd-journald
- Bugfix: AWUSH051NH and 052NH did not work cleanly as TX on 5Ghz band: Reduced TXPower for Ralink chipsets

### Anemos-EZ-Wifibroadcast 1.2 beta
 - This new BETA image contains the following changes made by user anemostec from rcgroups. It is technically a fork and is based on Stable v1.2 image.
- kernel recompiled with full joystick support and 1000Hz interrupt modification suggested by rodizio
- befinitiv wifibroadcast code heavily revised to optimize serial communication
- RC command joystick support added with PPM frame support and almost zero latency (not measured yet but far below 100ms). compatible with almost every flight controler in the market
- USB tethering configuration activated by default 
 - For all serial communication, we have to use the new wifibroadcast library instead of the old tx and rx utility, an exemple has been provided with the joystick_send_command.c file. The pipe communication has been removed in order to further reduce the latency.
 - The PPM frame generation is made by an external arduino connected by usb to the raspeberry pi, the source code of it is available in the rc_landing directory
 - The default password of this new distribution is anemos