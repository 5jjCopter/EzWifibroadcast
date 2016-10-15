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