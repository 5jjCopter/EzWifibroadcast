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


2.3Ghz and 2.5-2.7Ghz band only works with Atheros cards. Frequencies above 2512MHz are not recommended as the output power and sensitivity is greatly reduced, only useable for short-range applications. 4.9Ghz band is only supported by CSL300Mbit Ralink 5572 dongles. Check your local regulations and laws before setting frequencies!

### FREQSCAN=
Set to "Y" on the RX for auto-scanning. Frequency still has to be set on TX! **Feature might be buggy or not work at all!**



### TXMODE=
Set this to "single" for single TX wifi card, for dual TX wifi cards set "dual".
MAC addresses and frequency for the RX and TX wifi need to be set here when dual TX mode is enabled.


### MAC_TX[0]= / FREQ_TX[0]=
Wifi card MAC addresses and frequency for the TX wifi cards need to be set here when dual TX mode is enabled. Please note that counting starts with index 0. Maximum two cards supported for TX (Index 0-1)



### MAC_RX[0]= / FREQ_RX[0]=
Wifi card MAC addresses and frequency for the RX wifi cards need to be set here when dual TX mode is enabled. Please note that counting starts with index 0. Maximum four cards supported for RX (Index 0-3)

### DATARATE=
Wifi Datarate. Lower settings yield higher range and vice versa. Default is "4" which gives about 6Mbit video bitrate with default settings and no CTS protection. For long-range application, use "2" or "1", if you want higher quality use "5" or "6".
1=5.5Mbit, 2=11Mbit, 3=12Mbit, 4=19.5Mbit/18Mbit, 5=24Mbit, 6=36Mbit


### VIDEO_BLOCKS= / VIDEO_FECS= / VIDEO_BLOCKLENGTH=
These parameters allow for a trade-off between link-resiliency, latency and achievable data rate (and thus quality).

See here for some in-depth explanation: https://befinitiv.wordpress.com/2015/07/19/forward-error-correction-for-wifibroadcast/

If using Pi2 or Pi3 as TX, you can try 12/6/768 or 16/8/512 (with about same latency as 8/4/1024) for higher resiliency against interference. If latency doesn't matter for you, maybe try something like 24/12/768.


### FPS=
Choose between 30, 40, 48, 59.9

### TELEMETRY_TRANSMISSION=wbc
Telemetry transmission method:
"wbc" = use wifibroadcast as telemetry up/downlink
"external" = use external means as telemetry up/downlink (LRS or 3DR dongles)
If set to "external", set serialport to which LRS or 3DR dongle is connected on ground Pi, see options below

### EXTERNAL_TELEMETRY_SERIALPORT_GROUND=, EXTERNAL_TELEMETRY_SERIALPORT_GROUND_BAUDRATE=
Serial port and baudrate on the Ground Pi when using TELEMETRY_TRANSMISSION=external. Default /dev/serial0 for on-board Pi serialport, or set to "/dev/ttyUSB0" for external USB-to-serial adapter.

### ENABLE_SERIAL_TELEMETRY_OUTPUT=N
Set to "Y" to enable output of telemetry to serialport on ground Pi (for antenna tracker etc.)

### TELEMETRY_OUTPUT_SERIALPORT_GROUND=, TELEMETRY_OUTPUT_SERIALPORT_GROUND_BAUDRATE=
Serial port and baudrate on the Ground Pi when using ENABLE_SERIAL_TELEMETRY_OUTPUT=N. Default /dev/serial0 for on-board Pi serialport, or set to "/dev/ttyUSB0" for external USB-to-serial adapter.

### TELEMETRY_UPLINK=
Set to "disabled" or "mavlink" for Mavlink (Tower App, Missionplanner, etc.). Please note: Feature might not work correctly with all GCS Software and/or Flight Control Firmware, will be fixed in the future.

### ENABLE_RC=
Set this to "mavlink" to enable R/C over wifibroadcast using mavlink protocol, "msp" for MSP protocol, "sumd" for Graupner SUMD, "ibus" for Flysky IBUS, "srxl" for Multiplex SRXL / XBUS Mode B. Set to "disabled" to disable
Also see joyconfig.txt for other settings.


### VIDEO_BITRATE=
Default setting "auto" for automatic video bitrate measuring is recommended. Only set manual bitrate if you know what you are doing.


### BITRATE_PERCENT=65
if VIDEO_BITRATE above is set to "auto" the videobitrate will be determined by measuring the available bitrate and multiplying it with BITRATE_PERCENT. Depending on channel utilization by other wifi networks you may need to set this to a lower value like 60% to avoid a delayed video stream. On free channels you may set this to a higher value like 70% to get a higher bitrate and thus image quality. Values above 75% are not recommended as this will most certainly delay the videostream in case bitrate fluctuates due to lighting/scene changes.


### CTS_PROTECTION=
Default settings is "AUTO" which will automatically determine if wifi traffic is around. Set this to "Y" to enable CTS protection, "N" to disable. Set this to "Y" in areas with lots of Wifi traffic and when using the Wifibroadcast R/C feature.

### WIDTH= / HEIGHT=
Camera image settings.
Maximum supported resolutions/FPS for V1 cam: 1280x720: 30fps, 48fps. 1920x1080: 30fps
Maximum supported resolutions/FPS for V2 cam: 1280x720: 30fps, 48fps, 59.9fps. 1640x922: 30fps, 40fps. 1920x1080: 30fps


### KEYFRAMERATE=
Lower values mean faster glitch-recovery, but also lower video quality. With fps=48 and keyframerate=5, glitches will stay visible for around 100ms in worst case. Set this higher or lower according to your needs, for fast and low flying you may want a lower value to get faster glitch-recovery (minimum value is 2). For high and slow flying you can set higher values like 10 or 20 to get better video quality.

### EXTRAPARAMS=
Set additional raspivid parameters here, see https://github.com/bortek/EZ-WifiBroadcast/wiki/Raspivid-camera-settings-and-parametrs for more info.


### FC_RC_SERIALPORT=
Serialport to use on the TX Pi for the Multiwii serial protocol R/C connection. Set this to "/dev/serial0" for Pi onboard serial port or  "/dev/ttyUSB0" for USB-to-serial adapter.

### FC_RC_BAUDRATE=
Serial port and baudrate (19200 is minimum) to use for the R/C connection between air Pi and flight control

### FC_TELEMETRY_SERIALPORT=, FC_TELEMETRY_BAUDRATE=
Serial port and baudrate to use for the telemetry connection between air Pi and flight control
Set this to "/dev/serial0" for Pi onboard serial port or  "/dev/ttyUSB0" for USB-to-serial adapter


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
set this to "Y" to enable wifibroadcast relay mode. This will forward the received video and telemetry streams to another wifibroadcast RX. Note! Currently, the RSSI display you see on the RX behind the relay is not the RSSI between aircraft and ground, but between relay and rx on the ground! Feature is not much tested and may not work correctly!

### RELAY_NIC= / RELAY_FREQ= 
Wifi stick and frequency to use for the relay 

### AIRODUMP=
Set to "Y" to scan for wifi networks with airodump-ng before starting RX. This will give you an overview of Wifi networks around. Feature is not much tested and may not work correctly!

### AIRODUMP_SECONDS=
Number of seconds wifi scanner is shown. Minimum recommended scanning time is 25 seconds.

### QUIET=
Set this to "Y" to disable text messages about Display and Wifi card setup etc. to get a more "clean" display

### FORWARD_STREAM=
Set this to "raw" to forward a raw h264 stream to 2nd display devices (for FPV_VR app), to "rtp" to forward RTP h264 stream (for Tower app and gstreamer etc.).

### VIDEO_UDP_PORT=
UDP port to send video stream to, default 5600.

### MAVLINK_FORWARDER=
Mavlink forwarder to use. Default "mavlink-routerd", you may want to try "cmavnode" if mavlink telemetry doesn't work correctly for you.

### DEBUG=
St this to "Y" to enable collection of extra debug logs. If you experience any issues, please reproduce them with debug set to "Y" and plug a USB memory stick afterwards, you will find the debug logs on the memory stick.