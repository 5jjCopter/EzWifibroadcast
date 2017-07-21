## This page will help you customize your ez wifibroadcast distribution to better suit your needs

### Tuning the latency
One of the users have spend some time and effort on tuning his setup for low latency. You can read more about his setup and findings in [this Issue](https://github.com/bortek/EZ-WifiBroadcast/issues/27).

### Partition expansion
To expand your tiny filesystem to fit all your sd card
type the following commands 
* rw
* raspi-config
* expand filesystem
* reboot    
after reboot & relogin
* rw
* resize2fs /dev/mmcblk0p2
* reboot



### Compiling kernel from source / making changes
Be sure your are on a raspberry pi 2 or 3 platform, otherwise the compilation time would be awfully long. During compilation the Pi can get hot, make sure cooling is adequate or reduce overclocking (force_turbo=0 and gpu_freq=300 in config.txt).

For Raspberry Pi2/3:
* cd /usr/src/v7-kernel
* make menuconfig
* make -j4 zImage modules dtbs
* make modules_install
* ./copy7.sh
* reboot



For Raspberry Pi1/Zero/Odroid-W:
* cd /usr/src/v6-kernel
* make menuconfig
* make -j4 zImage modules dtbs
* make modules_install
* ./copy6.sh
* reboot

### Extending range and reception quality
Here are various setups that might help you extend the range and/or reception quality.

* All TL-WN722N cards setup, one on the transmitter and three on the receiver Note: With Pi Zero on the tx side, you are limited to one tx card.

* The dual TX function is not much tested yet and there may be timing issues which can lead to badblocks. Therefore try at first single TX stick and make sure that everything works as expected. You need at least about 120Mhz of "space" between the two different frequencies when using two TX sticks. For example one combination would be 1x CSL and 1x WN722N cards both on TX (Note, Pi Zero is not supported for multiple TX setup). Then RX side with the CSL sticks set to something like 2484Mhz and the 722n sticks to something below around 2360Mhz.

* Since WN722N has more power than CSL, use one of that for TX and the one WN722N + 2 CSL sticks for RX. That should give you about 1km of stable range with stock antennas. Keep in mind though, the CSL sticks only work on 2412-2484, so you are limited to that frequency range when mixing Atheros and Ralink on the RX.