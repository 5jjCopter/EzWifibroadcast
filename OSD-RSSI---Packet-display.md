# OSD RSSI and packet display

![OSD](https://github.com/bortek/EZ-WifiBroadcast/blob/master/wiki-content/OSD-1.6RC3.png)

- The large dbm display in the upper left corner is the best signal strength received from all cards (in the example above, card Rx1 has the best signal strength)

- Below that you find packet statistics. First number is badblocks, i.e. errors that could not be corrected by the FEC, these lead to visible glitches. Obviously, you want to keep that number as low as possible. Second number is lost packets. Too many lost packets will lead to badblocks and thus visible glitches. If this number is constantly counting up you have either interference, bad wiring or (only with Ralink RX cards) have the transmitter too near to the receiver. Third number is number of received packets. The two numbers in parenthes show received and decoded telemetry packets.


- Below that, you find signal strength and number of received packets for the individual RX cards.


- The two dbm and "Lost" displays in the upper right corner show signalstrength and packetloss for R/C and telemetry uplink.


- The upper bitrate display shows the bitrate that raspivid has been set to. Number in parentheses is the maximum available bitrate that was measured. With default settings, this should show something around 6000 (9500) kbit. The lower bitrate display is the actual measured bitrate at the RX.
