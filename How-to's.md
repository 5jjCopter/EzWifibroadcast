## Setting up the OSD


1. configure general OSD and telemetry parameters in wifibroadcast-1.txt:

- Enable OSD in wifibroadcast-1.txt (already enabled by default)
`OSD=Y`

- Set the Pi's serial port baudrate to the same baudrate as the serial telemetry data stream coming from the flight control 
`OSD_BAUDRATE=9600`

- **_Optional_**: If using an external USB2Serial adapter instead of the Pi on-board serial port:
`OSD_SERIALPORT=/dev/ttyUSB0`


- If you want to connect your flight control to the TX Pi, leave `TELEMETRY_INPUT=tx`, if you have some other means of transmitting the telemetry to the ground (e.g. an LRS with telemetry downlink) choose `TELEMETRY_INPUT=rx` to receive the telemetry stream on the ground Pi serial port.


In case you want to use the OSD included in the Android FP_VR app, also choose the appropriate UDP port to which the telemetry stream will be forwarded with OSD_UDP_PORT=5002 (See in the FPV_VR settings which port is the right one for your telemetry protocol).



2. Configure telemetry protocol and OSD options in osdconfig.txt

- Remove the "//" characters in front of the OSD_RSSI and OSD_RSSI_DETAILED options to enable an RSSI and packets display for the OSD data in the upper right side of the screen. This way, you can see easily check if data is being received.

`#define OSD_RSSI`
`#define OSD_RSSI_DETAILED`


- Choose the telemetry protocol used, Frsky is default, other options supported are Mavlink, Lightweight telemetry (LTM), NMEA GPS.
`#define FRSKY`



Generally, try to configure your flight control so that it does not send out Unnecessary large amounts of data to keep the packet rate as low as possible.


Depending on the amount of data your flight control sends, you may want to increase OSD_BLOCKLENGTH=64 to something larger like 256 to reduce the amount of telemetry packets. Compare the amount of packets of the video stream (on the upper left side) to the amount of packets of the telemetry stream (upper right) to get an idea. The number of OSD packets should be not more than 10% of the number of video packets.

