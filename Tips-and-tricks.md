## This page will help you customize your ez wifibroadcast distribution to better suit your needs

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
