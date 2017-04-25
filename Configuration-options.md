The wifibroadcast.txt configuration file is split-up into three sections:

1. Common settings: These settings must be kept in-sync for both TX and RX
2. RX Settings: These settings only affect the RX
3. TX Settings: These settings only affect the TX



### FREQ=

The following frequencies are supported:

2312, 2317, 2322, 2327, 2332, 2337, 2342, 2347, 2352, 2357, 2362, 2367, 2372, 2377, 2382, 2387, 2392, 2397, 2402, 2407

2412, 2417, 2422, 2427, 2432, 2437, 2442, 2447, 2452, 2457, 2462, 2467, 2472, 2484

2487, 2489, 2492, 2494, 2497, 2499, 2512, 2532, 2572, 2592, 2612, 2632, 2652, 2672, 2692, 2712

4920, 4940, 4960, 4980

5180, 5200, 5220, 5240, 5260, 5280, 5300, 5320

5500, 5520, 5540, 5560, 5580, 5600, 5620, 5640, 5660, 5680, 5700

5745, 5765, 5785, 5805, 5825


2.3Ghz and 2.5-2.7Ghz band only works with Atheros cards. 2.5-2.7Ghz is untested. 4.9Ghz band is only supported by CSL300Mbit Ralink 5572 dongles. Other Ralink cards may support these channels and also additional overlapping channels in the 5Ghz band, you may want to check with "iw list". Check your local regulations before using channels outside the 2.4Ghz band.

### FREQSCAN=
 Set to "Y" on the RX for auto-scanning. Frequency still has to be set on TX! **Feature might be buggy or not work at all!**



### TXMODE=
Set this to "single" for single TX wifi card, for dual TX wifi cards set "dual".
MAC addresses and frequency for the RX and TX wifi need to be set here when dual TX mode is enabled.


### MAC_TX[0]= / FREQ_TX[0]=
Wifi card MAC addresses and frequency for the TX wifi cards need to be set here when dual TX mode is enabled. Please note that counting starts with index 0. Maximum two cards supported for TX (Index 0-1)



### MAC_RX[0]= / FREQ_RX[0]=
Wifi card MAC addresses and frequency for the RX wifi cards need to be set here when dual TX mode is enabled. Please note that counting starts with index 0. Maximum four cards supported for RX (Index 0-3)


### VIDEO_BLOCKS= / VIDEO_FECS= / VIDEO_BLOCKLENGTH=
These parameters allow for a trade-off between link-resiliency, latency and achievable data rate (and thus quality).

See here for some in-depth explanation: https://befinitiv.wordpress.com/2015/07/19/forward-error-correction-for-wifibroadcast/

If using Pi2 or Pi3 as TX, you can try 12/6/768 or 16/8/512 (with about same latency as 8/4/1024) If latency doesn't matter for you, maybe try something like 24/12/768.

If using two TX cards in alternate mode, you can try 12/12/512 for fully redundant link (will allow for about 8Mbit video bitrate) or 12/6/768 for higher bandwidth link (will allow for about 11-12Mbit video bitrate)



### CTS_PROTECTION=
Set this to "Y" to enable CTS protection. Enable this in areas with lots of Wifi traffic and when using 
the Wifibroadcast R/C feature.

### BITRATE=
Video bitrate. Lower settings yield higher range and vice versa.
1=2.5Mbit, 2=4.5Mbit, 3=6Mbit, 4=8.5Mbit, 5=11.5Mbit

### FPS=
Choose between 30, 40, 48, 59.9

### TELEMETRY_TRANSMISSION=wbc
Telemetry transmission method:
wbc = use wifibroadcast as telemetry up/downlink
external = use external means as telemetry up/downlink (LRS or 3DR dongles)
if set to external, set serialport to which LRS or 3DR dongle is connected both on ground and air pi

### TELEMETRY_UPLINK=
Set to "disabled" or "mavlink" for Mavlink (Tower App, Missionplanner, etc.)

### ENABLE_RC=
Set this to "Y" to enable R/C over wifibroadcast. This is not much tested yet. Also see joyconfig.txt for other settings.

### WIDTH= / HEIGHT=
Camera image settings.
Maximum supported resolutions/FPS for V1 cam: 1280x720: 30fps, 48fps. 1920x1080: 30fps
Maximum supported resolutions/FPS for V2 cam: 1280x720: 30fps, 48fps, 59.9fps. 1640x922: 30fps, 40fps. 1920x1080: 30fps

For higher resolutions, you may also want to increase the bitrate, see BITRATE= option.


### KEYFRAMERATE=
Lower values mean faster glitch-recovery, but also lower video quality. With fps=48 and keyframerate=5, glitches will stay visible for around 100ms in worst case. Set this higher or lower according to your needs, for fast and low flying you may want a lower value to get faster gltich-recovery. Minimum value is 2.

### EXTRAPARAMS=
Set additional raspivid parameters here


### FC_RC_SERIALPORT=
Serialport to use on the TX Pi for the Multiwii serial protocol R/C connection. Set this to "/dev/serial0" for Pi onboard serial port or  "/dev/ttyUSB0" for USB-to-serial adapter.

### FC_RC_BAUDRATE=
Serial port and baudrate (19200 is minimum) to use for the R/C connection between air Pi and flight control

### FC_TELEMETRY_SERIALPORT=
### FC_TELEMETRY_BAUDRATE=
Serial port and baudrate to use for the telemetry connection between air Pi and flight control
Set this to "/dev/serial0" for Pi onboard serial port or  "/dev/ttyUSB0" for USB-to-serial adapter

### RC_TXMODE= / RC_NICS
TX Mode and wifi cards to use for sending RC, separated by a space when using alternate or duplicate tx mode

### WIFI_HOTSPOT=
Set this to "Y" to enable Wifi Hotspot. Default SSID is "EZ-Wifibroadcast", password is "wifibroadcast". See apconfig.txt for configuration. This will forward the received video and telemetry streams to an android device or computer connected to the RX Pi via WiFi. Please note, that you need atleast 120Mhz of space between the hotspot frequency and the video frequency used.


### WIFI_HOTSPOT_NIC=
Set to "internal" to use the interal Pi3 wifi chip or the MAC address of the USB card you want to use

### ETHERNET_HOTSPOT=
set this to "Y" to enable Ethernet hotspot. This will forward the received video and telemetry streams to another computer or other device connected to the Raspberry via Ethernet

### ENABLE_SCREENSHOTS=
Set to "Y" to enable periodic screenshots every 10 seconds

### VIDEO_TMP=
Set to "memory" to use RAMdisk for temporary video/screenshot/telemetry storage. This limits recording time to ~12-14 minutes, but is the safe way. If you need longer recording times, use "sdcard", to use the sdcard as the temporary video storage. Keep in mind though, that this might introduce video stutter and/or bad blocks. **TEST CAREFULLY BEFORE USING!**

### RELAY=
set this to "Y" to enable wifibroadcast relay mode. This will forward the received video and telemetry streams to another wifibroadcast RX. Note! Currently, the RSSI display you see on the RX behind the relay is not the RSSI between aircraft and ground, but between relay and rx on the ground!

### RELAY_NIC= / RELAY_FREQ= 
Wifi stick and frequency to use for the relay 

### QUIET=
Set this to "Y" to disable text messages about Display and Wifi card setup etc. to get a more "clean" display