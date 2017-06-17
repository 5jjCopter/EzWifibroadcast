## Pi Zero W support

Currently, with EZ-Wifibroadcast 1.5, the newly released Pi Zero W is not supported due to the firmware being too old. As it turned out, the firmware in the pi0-firmware directory on the sdcard image does **_not_** work due to compatibility issues with the current kernel used.

To make EZ-Wifibroadcast work with your Pi0 W:

- Download the Raspberry 2017-03-03 firmware from [here](http://downloads.raspberrypi.org/raspbian/archive/2017-03-03-17:49/boot.tar.xz)

- Replace the original _start_x.elf_ file on the sdcard with the one from the above archive (.xz archives can be unpacked with WinRAR or 7-Zip)


