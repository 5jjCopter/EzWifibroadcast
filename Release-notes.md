## Release notes

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