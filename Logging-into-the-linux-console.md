## Logging into the Linux console

To log into the Linux console, there are three ways:

### 1. Local login (via a keyboard and monitor connected to the Pi)
- Connect keyboard and monitor to the Pi
- Press alt-F12 to switch to TTY12


### 2. Remote login via SSH over ethernet hotspot or wifi hotspot (RX Pi only!)
- Enable ETHERNET_HOTSPOT and/or WIFI_HOTSPOT in wifibroadcast-1.txt config file
- Connect a computer via Ethernet or Wifi
- Use your favorite SSH client in your favorite OS (e.g. PuTTY for Windows)
- Connect to IP 192.168.1.1 using Ethernet hotspot or 192.168.2.1 for Wifi hotspot
- Username: root
- Password: raspberry


### 3. Remote login with the Pi as Ethernet DHCP client
- Connect the Pi to your router before powering it up
- To determine the IP, either watch the HDMI screen, you will see a message showing the IP the Pi has aqcuired, or:
- Look into your router's webinterface, you will see the Pi with hostname "wifibrdcast-rx" or "wifibrdcast-tx"
- Use your favorite SSH client in your favorite OS (e.g. PuTTY for Windows) to connect to that IP
- Username: root
- Password: raspberry


Note: The filesystem is read-only when nobody is logged in and will be automatically switched to read-write when logging in.