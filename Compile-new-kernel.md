### Compiling new kernel with 5/10 MHz bandwidth atheros support

Be sure your are on a raspberry pi 2 or 3 platform, otherwise the compilation time would be awfully long.  

type the following commands:  
* sudo su
* rw
* wget https://raw.githubusercontent.com/notro/rpi-source/master/rpi-source -O /usr/bin/rpi-source && sudo chmod +x /usr/bin/rpi-source && /usr/bin/rpi-source -q --tag-update
* rpi-source
* cd /root/
* wget https://raw.githubusercontent.com/bortek/EZ-WifiBroadcast/master/Patches/patch-global.patch
* cd linux
* patch -p1 < ../patch-global.patch
* KERNEL=kernel7
* make bcm2709_defconfig
* make -j4 zImage modules dtbs
* make modules_install
* cp arch/arm/boot/dts/\*.dtb /boot/
* cp arch/arm/boot/dts/overlays/\*.dtb\* /boot/overlays/
* cp arch/arm/boot/dts/overlays/README /boot/overlays/
* scripts/mkknlimg arch/arm/boot/zImage /boot/$KERNEL.img
* reboot  
you're done