## Setting up the OSD


### 1. configure general OSD and telemetry parameters in wifibroadcast-1.txt (both on TX and RX)

- Set `OSD=Y` (already enabled by default)

- Set the Pi's serial port baudrate to the same baudrate as the serial telemetry data stream coming from the flight control. E.g. `OSD_BAUDRATE=57600` if your flightcontrol sends it's telemetry data using 57600 baud.

- For the onboard Pi serial port leave default `OSD_SERIALPORT=/dev/serial0`, if using an external USB2Serial adapter, set `OSD_SERIALPORT=/dev/ttyUSB0`

- If you want to connect your flight control to the TX Pi, leave `TELEMETRY_INPUT=tx`, if you have some other means of transmitting the telemetry to the ground (e.g. an LRS with telemetry downlink) choose `TELEMETRY_INPUT=rx` to receive the telemetry stream on the ground Pi serial port.

- In case you want to use the OSD included in the Android FP_VR app, also choose the appropriate UDP port to which the telemetry stream will be forwarded by setting e.g. `OSD_UDP_PORT=5002` (See in the FPV_VR settings which port is the right one for your telemetry protocol).



### 2. Configure telemetry protocol and OSD options in osdconfig.txt (only on the RX)

- Remove the "//" characters in front of the `#OSD_RSSI` and `#OSD_RSSI_DETAILED` options to enable an RSSI and packets display for the OSD data in the upper right side of the screen. This way, you can see easily check if data is being received. E.g.: `#define OSD_RSSI` and `#define OSD_RSSI_DETAILED`

- Choose the telemetry protocol used, Frsky is default, other options supported are Mavlink and Lightweight telemetry (LTM). E.g.: `#define FRSKY`

- Choose graphical OSD options you would like to have enabled in osdconfig.txt. Should be self-explanatory.

- Chose an appropriate update interval for the OSD. 50ms = 20 updates per seconds should be okay for most, if you don't use the artificial horizon or other features that require a high update rate to be smooth, you can increase it. If you feel the OSD is not smooth enough, try decreasing it. Do not go below 20ms. E.g. `#define UPDATE_INTERVAL 30`

Generally, try to configure your flight control so that it does not send out unnecessary large amounts of data to keep the packet rate as low as possible.

Depending on the amount of data your flight control sends, you may want to increase `OSD_BLOCKLENGTH=64` to something larger like 256 to reduce the amount of telemetry packets. Compare the amount of packets of the video stream (on the upper left side) to the amount of packets of the telemetry stream (upper right) to get an idea. The number of OSD packets should not be more than 10% of the number of video packets.

The received telemetry data stream will also be saved to an USB memory stick automatically.


### 3. Wiring
- Connect the serial port TX pin of your flight control to the serial port RX pin on the Raspberry. _**WARNING:**_ The Pi uses 3.3V logic level on the serial ports, make sure your flight control also uses 3.3V. 5V might destroy the Pi serial port! (See https://pinout.xyz/ for pinout).

For Naze32 and clones: Do not send an inverted serial signal, the Pi doesn't support this. When using a Naze32 with softserial, disable this on the Cleanflight CLI with `set telemetry_inversion = OFF`

- Power the system up, you should see the received packets counter for telemetry data in the upper right corner increasing. If it stays at zero, there is no telemetry being transmitted/received, re-check wiring, baudrate and flight control settings in that case.



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
- Start FPV_VR app on android device

If you also have a HDMI monitor connected to the RX, you should see a short message at the bottom of the screen when the android device has been detected.


## Using the Wifi-Hotspot functionality

- Set `WIFI_HOTSPOT=Y`in wifibroadcast-1.txt to enable the Wifi hotspot
- Leave `WIFI_HOTSPOT_NIC=internal` if you want to use the internal onboard Wifi adapter of the Pi3 or set it to the MAC address (all lower case, no spaces, dashes or colons) of the wifi adapter you want to use for the Hotspot.
- Configure SSID, password and channel in apconfig.txt if desired. Default SSID is "EZ-Wifibroadcast", default password is "wifibroadcast", channel is 1.
- Connect to the Wifi hotspot, if you also have a HDMI monitor connected, you should see a message that the device has been detected.

Note: To not interfere with each other, there must be about 130Mhz of "space" between Hotspot frequency and wifibroadcast video transmission frequency. The internal Pi3 wifi card only supports frequencies from 2.412MHz to 2472Mhz, so if using the internal wifi card, it's not possible to use the 2.4G band for wifibroadcast transmission.

Other external cards have not been tested much, but Ralink based sticks seem to work for 5Ghz so far.

Please also note, that "normal" Wifi transmission is by far not as stable as wifibroadcast transmission, so be aware that there might be stuttering or badblocks, disconnects or other typical wifi issues when using the Wifi Hotspot. If you need a reliable video stream on the android device, consider using USB Tethering.


## Ground recording (Video/telemetry/screenshots)

EZ-Wifibroadcast automatically stores video and telemetry in a temporary storage while it is being received from the TX. Saving screenshots (in 10s intervals) is also possible by setting "ENABLE_SCREENSHOTS=Y" in wifibroadcast-1.txt.

To save video, telemetry and screenshots to a USB memory stick, simply plug the stick in. After a few seconds, a message should appear and the recorded video will start playing on the HDMI screen while being saved to USB. A message will appear when saving is done.

Currently, recording is limited to ~13 minutes due to the temporary storage being a ram disk. You can set `VIDEO_TMP=sdcard`to use the sdcard as temporary storage. Boot-up will take a little longer the first timeafter this option has been set, as the temporary storage on the sdcard needs to be prepared first.
**WARNING:** Due to issues with the linux kernel, this may lead to video stuttering badblocks or video freezing. Use a fast sdcard to mitigate this and test thoroughly before flying!

## Setting up R/C over Wifibroadcast with a Joystick

The R/C link from ground Pi to air Pi uses MSP (MultiWii Serial Protocol). This is also what is being output on the air Pi serial port. To use it with other protocols, you can use an Arduino with code by Anemostec to convert the R/C data from MSP to PPM for example.

Obviously, to get the same R/C range as video range, you need the same transmit power on both sides, so using a high-power card on the aircraft and only low-power cards on the ground won't make much sense, as the control range will be shorter than the video range.

Currently, there is no RSSI display for the R/C connection on the RX OSD, so you have to make sure, that R/C range is greater than video range. This is achieved by three things:

- R/C control is sent with lower bitrate, yielding slightly higher sensitivity and thus more range than the video link
- R/C control is sent with a rate of 100 packets per seconds or to say it differently, the stick positions are updated every 10ms. This allows for quite high packetloss rates (as long as there are not too many consecutive packets lost) since even with a packetloss rate of 50%, we'd still receive 50 stick positions per seconds which should still be sufficient for control. The video link however, will not tolerate 50% packetloss, so the R/C link should be more robust than the video link
- R/C control uses shorter packets (MSP is only 26bytes payload compared to the 1024 bytes used for the video link), this reduces the probability of collisions and thus packetloss

Be careful, this feature has not been tested much, RTH or autopilot is recommended

### 1. Configure R/C general parameters in wifibroadcast-1.txt (both on TX and RX)

- set `ENABLE_RC=Y`
- For the onboard Pi serial port leave default `RC_SERIALPORT=/dev/serial0`, if using an external USB2Serial adapter, set `RC_SERIALPORT=/dev/ttyUSB0`
- Choose the mode in which the R/C packets are to be transmitted:
  `RC_TXMODE=single` uses a single wifi card on the RX for transmitting R/C packets
  `RC_TXMODE=alternate` uses two cards on the RX for transmitting R/C packets in an alternating pattern (i.e. packet 1 on card1, packet2 on card2, packet3 on card1, packet4 on card2 and so forth)
  `RC_TXMODE=duplicate` also uses two cards, but sends each R/C packet out twice, one on each interface.
- Chose which cards on the RX you want to use for transmitting R/C packets by setting `RC_NICS` to the MAC address of these cards, e.g. `RC_NICS="24050f0f4175"`
- If you are using Atheros cards, login to the linux system on the _RX_, then:
  - type `rw` to make filesystem writeable
  - type `nano /etc/modprobe.d/ath9k_htc.conf`
  - inside that file, change `fw_bitrate=18` to `fw_bitrate=12`
  - Hit `CTRL-X`to exit the editor, answer `Y` to save the file
  - typ `reboot`to re-start and apply the bitrate change

###2. Configure joystick related settings in joyconfig.txt
- Axis mapping to ROLL, PITCH, etc. is pre-configured for a Taranis in USB mode, if you use something else, you need to change numbers so that they match the corresponding controls.

- `#define AXIS0_INITIAL=`sets the initial values for the controls. This is necessary, as it is currently not possible to detect the stick positions until they have been moved. For yaw, roll, pitch you probably want 1500, for throttle 1000.

For a Taranis in Joystick mode, This should do:

`#define AXIS0_INITIAL 1500`

`#define AXIS1_INITIAL 1500`

`#define AXIS2_INITIAL 1000`

`#define AXIS3_INITIAL 1500`

###3. Wiring
Connect the serial port RX pin of your flight control to the serial port TX pin on the Raspberry. The Pi uses 3.3V logic level on the serial ports, make sure your flight control also uses 3.3V, or it might not reliably detect the serial signal (See https://pinout.xyz/ for pinout).

###4. Testing
- Connect a monitor (either HDMI or composite, if composite, uncomment `sdtv_mode=2` in config.txt) to the _TX_ Pi
- Start up both TX and RX Pi
- Connect Joystick or Taranis in Joystick mode (Taranis needs to be powered before connecting)
- Do a ground test for correct packet reception and signal on the _TX_ monitor:
  - in the uppermost line, you will see dbm and blocks info, it should be counting up and should not show any badblocks
  - increase distance to the aircraft until you are at the end of the video range. R/C control should now still work, you should _not_ see lots of badblocks on the TX monitor in the uppermost line.
- If everything works as expected, fly. Be careful, this feature has not been tested much, RTH or autopilot is recommended