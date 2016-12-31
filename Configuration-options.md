The wifibroadcast.txt configuration file is split-up into three sections:

1. Common settings: These settings must be kept in-sync for both TX and RX
2. RX Settings: These settings only affect the RX
3. TX Settings: These settings only affect the TX


## Common settings

### FREQ=

The following frequencies are supported:

2312, 2317, 2322, 2327, 2332, 2337, 2342, 2347, 2352, 2357, 2362, 2367, 2372, 2377, 2382, 2387, 2392, 2397, 2402, 2407

2412, 2417, 2422, 2427, 2432, 2437, 2442, 2447, 2452, 2457, 2462, 2467, 2472, 2484

2487, 2489, 2492, 2494, 2497, 2499, 2512, 2532, 2572, 2592, 2612, 2632, 2652, 2672, 2692, 2712

4920, 4940, 4960, 4980

5180, 5200, 5220, 5240, 5260, 5280, 5300, 5320

5500, 5520, 5540, 5560, 5580, 5600, 5620, 5640, 5660, 5680, 5700

5745, 5765, 5785, 5805, 5825


2.3Ghz and 2.5-2.7Ghz band only works with Atheros cards. 2.5-2.7Ghz is untested. 4.9Ghz band is only supported by CSL300Mbit Ralink 5572 dongles. Other Ralink cards may support these channels and also additional overlapping channels in the 5Ghz band, you may want to check with "iw list"

### FREQSCAN=
 Set to "Y" on the RX for auto-scanning. Frequency still has to be set on TX! **Feature might be buggy or not work at all!**



### TXMODE=

Set this to "single" for single TX wifi card, for dual TX wifi cards set "alternate" or "duplicate". 

Alternate mode will treat both tx cards as one logical channel with twice the bandwidth by sending out packets on both  interfaces in an alternating pattern. This is the preferred dual TX mode.

Duplicate mode wil send _the same_ packets on both cards, i.e. it will simply duplicate the packets. This seems less optimal in terms of link resiliency, but lowers CPU usage significantly 



### MAC_TX[0]= / FREQ_TX[0]=
Wifi card MAC addresses and frequency for the TX wifi cards need to be set here when dual TX mode is enabled. Please note that counting starts with index 0. Maximum two cards supported for TX (Index 0-1)



### MAC_RX[0]= / FREQ_RX[0]=
Wifi card MAC addresses and frequency for the RX wifi cards need to be set here when dual TX mode is enabled. Please note that counting starts with index 0. Maximum four cards supported for RX (Index 0-3)


### VIDEO_BLOCKS= / VIDEO_FECS= / VIDEO_BLOCKLENGTH=
These parameters allow for a trade-off between link-resiliency, latency and achievable data rate (and thus quality).

See here for some in-depth explanation: https://befinitiv.wordpress.com/2015/07/19/forward-error-correction-for-wifibroadcast/

If using Pi2 or Pi3 as TX, you can try 12/6/768 or 16/8/512 (with about same latency as 8/4/1024) If latency doesn't matter for you, maybe try something like 24/12/768.

If using two TX cards in alternate mode, you can try 12/12/512 for fully redundant link (will allow for about 8Mbit video bitrate) or 12/6/768 for higher bandwidth link (will allow for about 11-12Mbit video bitrate)

### OSD=
Set to "Y" to enable OSD, "N" to disable

### OSD_BLOCKS= / OSD_FECS= / OSD_BLOCKLENGTH=
FEC settings for telemetry data. OSD_BLOCKS and OSD_FECS is best left at 1 and 0. OSD_BLOCKLENGTH is dependent on the telemetry protocol used, may need manual optimization.

### OSD_BAUDRATE=
Set this to the baudrate of your flight control

### OSD_STTY_OPTIONS=
Serial port configuration options, leave them as is for now.

### OSD_SERIALPORT=
This is the serialport that should be used for receiving telemetry data. Set this to "/dev/serial0" for Pi onboard serial port or "/dev/ttyUSB0" for an external USB-to-serial adapter

### TELEMETRY_INPUT=
Set this to "tx" if you want to connect the serial port on the TX Pi. In this case, the telemetry data stream will be sent down to the ground via wifibroadcast. Set to "rx" if you have some other means of getting the telemetry stream to the ground (e.g. UHF System with telemetry support or 433Mhz mavlink telemetry dongles) and want to connect the telemetry at the RX serial port.

### ENABLE_RC=
Set this to "Y" to enable R/C over wifibroadcast. This is not much tested yet, make sure you understand how it works before using it. Check if everything works as expected (failsafe etc.). Also see joyconfig.txt for other settings, default settings work for Taranis in USB Joystick mode

### RC_BLOCKS= / RC_FECS=
FEC transmission parameters for the R/C connection.


### WIDTH= / HEIGHT= / FPS= / BITRATE=
Camera image settings.
Maximum supported resolutions/FPS for V1 cam: 1280x720: 30fps, 48fps. 1920x1080: 30fps
Maximum supported resolutions/FPS for V2 cam: 1280x720: 30fps, 48fps, 59.9fps. 1640x922: 30fps, 40fps. 1920x1080: 30fps

Possible bitrates are dependent on wifi_bitrates and FEC settings, see below.