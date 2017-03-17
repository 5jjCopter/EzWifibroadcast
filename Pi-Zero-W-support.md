## Pi Zero W support

Currently, with EZ-Wifibroadcast 1.4, the newly released Pi Zero W is not supported due to the firmware being too old. Support for EZ-Wifibroadcast version 1.5 is planned.

In the meantime, this can be fixed manually:

- Download the latest official Raspbian Image (which contains the latest Raspberry firmware with Zero W support)
- Copy the firmware files from that image over to your EZ-Wifibroadcast 1.4 image and replace the old files
- Replace all files ending with *.dat, *.dtb and *.elf