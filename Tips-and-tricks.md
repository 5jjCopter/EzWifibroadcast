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

if you want to setup your internal wifi as AP, please proceed as following :   

 * sudo su
 * rw
 * apt-get update
 * apt-get install isc-dhcp-server
 * apt-get install hostapd
 * wget https://raw.githubusercontent.com/bortek/EZ-WifiBroadcast/master/Patches/ap.tar.gz
 * tar zxpvf ap.tar.gz
 * reboot
  
you're done, it will install you an AP named Anemos_AP with the following password anemostec

### enable the tethering connection between the RX raspberry pi and your android phone

on your RX pi issue the following commands
  * sudo su
  * rw
  * systemctl enable urandom
  * systemctl enable networking
  * nano /etc/network/interfaces
  * add the following lines \:   

allow-hotplug usb0  
iface usb0 inet dhcp

  * save and exit the nano editor
  * nano wifibroadcast_fpv_scripts/rx.sh
  * add the following lines after the sleep 3 line \:

\# wait for tethering to be done   
while \! (ifconfig | grep usb0 > /dev/null);  do echo "waiting for smartphone..."; sleep 1; done

change the DISPLAY_PROGRAM line to be as follow \:   
DISPLAY_PROGRAM="socat -b 1024 - UDP4-SENDTO:192.168.42.129:5000"

  * save the exit nano editor
  * reboot

when rebooted, on your android phone go to parameters => More => internet connexion sharing => share via usb
The usb wifi dongle will start blinking
Then use the mymediacodec_fpv player app : https://github.com/Consti10/myMediaCodecPlayer-for-FPV
and test the connection, you should receive NALU frames.

you're done
