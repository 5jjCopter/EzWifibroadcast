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

### Use the rpi internal wifi card
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
