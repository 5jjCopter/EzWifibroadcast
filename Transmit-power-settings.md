Important: Except for low-power Ralink dongles (see below), there is no need to increase transmit power! If you have range problems, check your wiring, power supply, antennas etc. and make sure you are on a free channel.


- Alfa AWUS036NHA: Card is set near maximum power, another 1-2db could be gained, but at the expense of wider signal shoulders and uncleaner signal

- Alfa 051/052NH: Card is set to maximum power, do not increase, you _will_ get badblocks if you do.

- TPlink 722N (and other low-power AR9271 dongles): Card is set to maximum power, no need to increase.

- CSL 300Mbit stick (and other low-power Ralink dongles): Increase txpower to +4 for maximum output.

- Ubiquiti WifiStation USB: For these cards, transmit power needs to be decreased. Maximum txpower setting is not yet known, probably somewhere between 46 and 54. Start with 46 to be on the safe side.



### Setting transmit power
- Login to the linux console
- type "rw" to make the filesystem writeable

Atheros: 
- Type "mcedit /etc/modprobe.d/ath9k_hw.conf" or "nano /etc/modprobe.d/ath9k_hw.conf" (whichever editor you may prefer)

Change the "txpower" parameter. Maximum value is 63, default is 58.

Ralink:
- Type "mcedit /etc/modprobe.d/rt2800usb.conf" or "nano /etc/modprobe.d/rt2800usb.conf" (whichever editor you may prefer)

Change the txpower parameter. 0 is default, maximum value is 4 (+4db), minimum value is -4 (-4db)


### Determining the maximum transmit power settings for yet unknown wifi dongles
- First, make sure wiring and power supply is good, if not, you _will_ get problems and badblocks
- Start with a low value, -2 for Ralink and 36 for Atheros
- Find a free channel. This is important. On 2.4Ghz, finding a free channel can be next to impossible. In that case, you can 'simulate' a free channel by removing the antennas on the RX and keepint the TX right next to the RX
- Test if everything works correctly. Let it run for an hour, you should get near zero packetloss.
- Increase transmit power, then rinse and repeat until you find the spot where further increasing transmit power leads to badblocks
- Decrease transmit power again until you see no more badblocks and then decrease it a little more to be on the safe side
- Test again, let it run for an hour, you should see almost zero packetloss