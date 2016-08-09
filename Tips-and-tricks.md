## This page will help you customize your ez wifibroadcast distribution to better feet your needs

### Partition expansion
To expand your tiny filesystem to fit all your sd card
type the following commands 
* sudo su
* rw
* raspi-config
* expand filesystem
* reboot    
after reboot & relogin
* sudo su
* rw
* resize2fs /dev/mmcblk0p2
* reboot

### Use the rpi 3 internal wifi card
type the following commands
* sudo su
* rw
* nano /etc/modprobe.d/brcmfmac-blacklist.conf    
comment the two lines present, your file should look like the following :      
\# blacklist the Raspberry Pi3 onboard wifi chip   
\#blacklist brcmfmac   
\#blacklist brcmutil

type in CTRL+O and CTRL+X to save and exit
reboot
(after reboot)
type the following commands
* sudo su
* rw
* nano /home/pi/wifibroadcast_fpv_scripts/rx.sh
instead of NICS=`ls /sys/class/net | grep wlan`    
put    
NICS=`ls /sys/class/net | grep wlan | grep -v wlan0`   
save file and exist, reboot, you're done

### compile new kernel with 5/10 MHz bandwidth atheros support

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