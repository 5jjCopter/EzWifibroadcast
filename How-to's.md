## Setting up telemetry and OSD

### 1. configure general OSD and telemetry parameters in wifibroadcast-1.txt (both on TX and RX)

- Set the Pi's serial port baudrate to the same baudrate as the serial telemetry data stream coming from the flight control. E.g. `FC_TELEMETRY_BAUDRATE=57600` if your flightcontrol sends it's telemetry data using 57600 baud.

- For the onboard Pi serial port leave default `FC_TELEMETRY_SERIALPORT=/dev/serial0`, if using an external USB2Serial adapter, set `FC_TELEMETRY_SERIALPORT=/dev/ttyUSB0`

- If you want to connect your flight control to the TX Pi and use wifibroadcast for telemetry transmission, leave `TELEMETRY_TRANSMISSION=wbc`

- If you have some other means of transmitting the telemetry to the ground (e.g. an LRS with serial downlink or 3DR dongles) choose `TELEMETRY_TRANSMISSION=external` to receive the telemetry stream on the ground Pi serial port. If using external telemetry transmission, also configure `EXTERNAL_TELEMETRY_SERIALPORT_GROUND=` and `EXTERNAL_TELEMETRY_SERIALPORT_GROUND_BAUDRATE=`


### 2. Configure telemetry protocol and OSD options in osdconfig.txt (only on the RX)

- Choose the telemetry protocol used, Mavlink is default, other options supported are Mavlink and Lightweight telemetry (LTM). E.g.: `#define LTM`

- Choose graphical OSD options you would like to have enabled in osdconfig.txt. Should be self-explanatory.

Generally, try to configure your flight control so that it does not send out unnecessary large amounts of data to keep the packet rate as low as possible.

The received telemetry data stream will also be saved in text and raw form to an USB memory stick automatically for later review.


### 3. Wiring
- Connect the serial port TX pin of your flight control to the serial port RX pin on the Raspberry. _**WARNING:**_ The Pi uses 3.3V logic level on the serial ports, make sure your flight control also uses 3.3V. 5V might destroy the Pi serial port! (See https://pinout.xyz/ for pinout).

For Cleanflight/Betaflight/Inav/etc.: Do not send an inverted serial signal, the Pi doesn't support this. When using a Naze32 clone with softserial, disable this on the CLI with e.g. `set telemetry_inversion = OFF` (may differ depending on firmware used)

- Power the system up, you should see the received data and decoded data counters for telemetry (last two numbers in the RSSI display in the upper left corner) increasing. If the first number stays at zero, there is no telemetry being transmitted/received, re-check wiring, baudrate and flight control settings in that case. If the first number increases, but the second number stays at zero, there is data being received, but it cannot be decoded, usually this is caused by wrong baudrate settings or wrong telemetry protocol chosen.


## Setting up bi-directional mavlink telemetry

- Set `TELEMETRY_UPLINK=mavlink` in wifibroadcast-1.txt
- Connect Tower App, QGroundControl or Missionplanner etc. via USB-Tethering or Hotspot


## Using configuration profiles

To quickly change settings on the field, eight different configuration profiles selectable via GPIO pins are supported. This way, DIP switches, 3-way switches or jumpers can be used to change configuration, similar to analog gear.

3 GPIO pins give 8 possible combinations, from wifibroadcast-1.txt to wifibroadcast-8.txt. Just copy over the existing configfile with a new number and make desired changes (e.g. frequency, or camera settings) there. If you want to have a means to know which profile is selected on the TX, you can use the raspivid annotation parameters under EXTRAPARAMS to let raspivid insert the profile number or whatever text you would like into the video stream. On the RX there is currently no display which profile has been loaded.

The GPIO pins are being checked during boot-up, to select a different configuration, simply change the DIP-switch (and power-off and on again if the system was already running during the DIP switch change).


### Wiring:

GPIO7 | GPIO24 | GPIO23 | wifibroadcast-#.txt
  0        0       0        1
  0        0       1        2
  0        1       0        3
  0        1       1        4
  1        0       0        5
  1        0       1        6
  1        1       0        7
  1        1       1        8


0 = GPIO pin left open
1 = GPIO pin connected to GND

(Sorry for the screwed-up table, this Github markup language sucks, will fix that sometime else ...)


## Using the USB Tethering functionality

- Connect your android smartphone or tablet via USB to the RX Pi.
- Enable USB-Tethering in the options of your smartphone (note, some smartphones don't support this out-of-the box or seem to have this function disabled, you may need a 3rd party app to make USB-Tethering work with your device)
- Start FPV_VR app or other app (Tower App, QGroundcontrol etc.) on android device (don't forget to set `FORWARD_STREAM=raw` on the RX Pi when using FPV_VR app and to "rtp" when using the other apps)

If you also have a HDMI monitor connected to the RX, you should see a short message at the bottom of the screen when the android device has been detected.


## Using the Wifi-Hotspot functionality

- Set `WIFI_HOTSPOT=Y`in wifibroadcast-1.txt to enable the Wifi hotspot
- Leave `WIFI_HOTSPOT_NIC=internal` if you want to use the internal onboard Wifi adapter of the Pi3 or set it to the MAC address (all lower case, no spaces, dashes or colons) of the wifi adapter you want to use for the Hotspot.
- Configure SSID, password and channel in apconfig.txt if desired. Default SSID is "EZ-Wifibroadcast", default password is "wifibroadcast", channel is 1.
- Connect to the Wifi hotspot, if you also have a HDMI monitor connected, you should see a message that the device has been detected.

Note: To not interfere with each other, there must be about 130Mhz of "space" between Hotspot frequency and wifibroadcast video transmission frequency. The internal Pi3 wifi card only supports frequencies from 2412MHz to 2472Mhz, so if using the internal wifi card, it's not possible to use the 2.4G band for wifibroadcast transmission.

Other external cards have not been tested much, but Ralink based sticks seem to work for 5Ghz so far.

Please also note, that "normal" Wifi transmission is by far not as stable as wifibroadcast transmission, so be aware that there might be stuttering or badblocks, disconnects or other typical wifi issues when using the Wifi Hotspot. If you need a reliable video stream on the android device, consider using USB Tethering.


## Ground recording (Video/telemetry/screenshots)

EZ-Wifibroadcast automatically stores video and telemetry in a temporary storage while it is being received from the TX. Saving screenshots (in 10s intervals) is also possible by setting "ENABLE_SCREENSHOTS=Y" in wifibroadcast-1.txt.

To save video, telemetry and screenshots to a USB memory stick, simply plug the stick in after you are done flying. After a few seconds, a message should appear and the recorded video will start playing on the HDMI screen while being saved to USB. A message will appear when saving is done.

Currently, recording is limited to ~12 minutes due to the temporary storage being a ram disk. You can set `VIDEO_TMP=sdcard`to use the sdcard as temporary storage. Boot-up will take a little longer the first timeafter this option has been set, as the temporary storage on the sdcard needs to be prepared first.
**WARNING:** Due to issues with the linux kernel, this may lead to video stuttering badblocks or video freezing. Use a fast sdcard to mitigate this and test thoroughly before flying!

## Setting up R/C over Wifibroadcast with a Joystick

The R/C link from ground Pi to air Pi uses MSP (MultiWii Serial Protocol). This is also what is being output on the air Pi serial port. To use it with other protocols, you can use an Arduino with code by Anemostec to convert the R/C data from MSP to PPM for example.

Be careful, this feature has not been tested much, RTH or autopilot is recommended. Feature only works with Atheros cards!

### 1. Configure R/C general parameters in wifibroadcast-1.txt

On TX and RX Pi:
- set `ENABLE_RC=Y`
- set `CTS_PROTECTION=Y`

On TX Pi:
- For the onboard Pi serial port leave default `RC_FC_SERIALPORT=/dev/serial0`, if using an external USB2Serial adapter, set `RC_SERIALPORT=/dev/ttyUSB0`
- Set the `FC_RC_BAUDRATE=` parameter according to your flightcontrol. 19200 is the minimum required.

### 2. Configure joystick related settings in joyconfig.txt on RX Pi
- Axis mapping to ROLL, PITCH, THROTTLE, etc. may need to be changed.

- `#define AXIS0_INITIAL=`sets the initial values for the controls. This is necessary, as it is currently not possible to detect the stick positions until they have been moved. For yaw, roll, pitch you probably want 1500, for throttle 1000.

### 3. Enable R/C RSSI in osdconfig.txt on RX Pi
- uncomment the `#define RC_RSSI` line

### 4. Wiring
Connect the serial port RX pin of your flight control to the serial port TX pin on the Raspberry. The Pi uses 3.3V logic level on the serial ports, make sure your flight control also uses 3.3V, or it might not reliably detect the serial signal (See https://pinout.xyz/ for pinout).

### 5. Testing
- Connect Joystick or Taranis in Joystick mode (Taranis needs to be powered before connecting)
- Do a ground test for correct packet reception and signal:
    - increase distance to the aircraft until you are at the end of the video range. R/C control should now still work, you should _not_ see lots of Lost packets in the RSSI display in the upper right corner.
- If everything works as expected, fly. Be careful, this feature has not been tested much, RTH or autopilot is recommended


## Displaying the video stream on an android device, iPhone/iPad, Windows PC, Linux PC

Connect your device either via USB Tethering, Wifi-Hotspot or Ethernet-Hotspot to the Wifibroadcast RX.

### Android
[FPV_VR app](https://play.google.com/store/apps/details?id=com.constantin.wilson.FPV_VR
Usage information and source code: https://github.com/Consti10/FPV_VR)
Set `FORWARD_STREAM=raw` in wifibroadcast-1.txt to send a raw h264 stream to the FP_VR app.

[Tower app](https://play.google.com/store/apps/details?id=org.droidplanner.android)
Set `FORWARD_STREAM=rtp` in wifibroadcast-1.txt to send a RTP encapsulated h264 stream to the app.

[QGroundControl App](https://play.google.com/store/apps/details?id=org.mavlink.qgroundcontrol)
Set `FORWARD_STREAM=rtp` in wifibroadcast-1.txt to send use a RTP encapsulated h264 video stream to the app.



### iPhone/iPad:
Fishing FanCam app: https://itunes.apple.com/us/app/fishing-fancam/id1187600031

- Click on the eye icon (on the bottom right)
- Now a debug screen appears, select all on the upper bar, delete all parameters and set:

`udpsrc port=5000 ! h264parse ! avdec_h264 ! autovideosink sync=false`

Set `FORWARD_STREAM=raw` in wifibroadcast-1.txt to send a raw h264 stream

### Windows:
#### Gstreamer:
[Gstreamer 32-Bit Windows](https://gstreamer.freedesktop.org/data/pkg/windows/1.10.2/gstreamer-1.0-x86-1.10.2.msi)
[Gstreamer 64-Bit Windows](https://gstreamer.freedesktop.org/data/pkg/windows/1.10.2/gstreamer-1.0-x86_64-1.10.2.msi)

Use the following commandline:
`gst-launch-1.0.exe udpsrc port=5000 ! H264parse ! Avdec_h264 ! Autovideosink sync=False`

Set `FORWARD_STREAM=raw` in wifibroadcast-1.txt to send a raw h264 stream

Some people reported the necessity to add the gst-launch-1.0.exe application to their firewall exception list, see this video for more info: https://www.youtube.com/watch?v=eHCfyWhEAvI

#### GstreamerHUD:
Another Option is GStreamerHUD, see Github page here:
https://github.com/MovLab2/GStreamerHUD

Setup Download:
https://www.dropbox.com/sh/5ys4jbvdgxg09cb/AABCm-OIjh5NI4WTDnr6KNw4a?dl=0&preview=GStreamerHUD.msi

In case you get an error message that "api-ms-win-crt-runtime-l1-1-0.dll" is missing see here:
https://support.microsoft.com/en-ph/help/2999226/update-for-universal-c-runtime-in-windows
and here:
https://answers.microsoft.com/en-us/windows/forum/windows8_1-performance/error-message-api-ms-win-crt-runtime-l1-10dll-is/3a72ff02-cf73-4536-baf7-bdfd2f132a9e

See here for a video: https://www.youtube.com/watch?v=eHCfyWhEAvI

### Linux:
Install gstreamer using the package management system of your linux distribution

Use the following commandline:

`gst-launch-1.0 udpsrc port=5000 ! h264parse ! avdec_h264 ! autovideosink sync=false`