# Latency/Delay issues

This page is to give some background and help regarding latency/delay issues some people have been reporting on 2.4GHz with Atheros cards. Starting with 1.6RC4 (soon to be released), there will be a dynamic bandwith reduction feature (as well as logging and graphing of the times this happens) that should further help mitigate the problem.

**_Before you continue to do anything, please make sure that:_**
- Wiring and power supply is good. Read and follow the (Wiring Instructions)[https://github.com/bortek/EZ-WifiBroadcast/wiki/Wiring]
- Cooling is good. The Raspberry Pi will reduce CPU clockspeed when the CPU temperature climbs above 80 degrees Celsius, this will not enough CPU speed to cope with the amount of data and thus delay the videostream.

_If you still experience delay issues after making sure power supply and wiring is good, check the following:_

- Check CPU usage and CPU temperature on both the transmitter and receiver
A Pi Zero or Pi1 as transmitter should show around 50-60% CPU usage with standard settings, Pi3 as receiver somewhere below 20%. In general, make sure that CPU usage never goes above 80-90%. Make sure temperature is below 70-75 degrees, as at 80 degrees C, the Pi will be slowed-down. Starting with 1.6RC4, CPU usage and temperatures are shown on the OSD and are also automatically logged and graphed.

- Make sure you are on a free channel
Although the wifi cards work in monitor mode, they still adhere to Wifi CSMA/CA channel access which tries to avoid collisions. This means that wifibroadcast will only use free 'timeslots' (they are not real timeslots like in TDMA systems) in the channel, if it senses other transmissions already on the air, it will 'yield' and not transmit until it senses a clear channel again. If there is too much other Wifi traffic (or other non-Wifi signals), available timeslots and thus available bandwidth will be lower than the bandwidth needed for the videostream which will lead to delays. 

Please also note, that this is highly dependent on actual channel usage and can vary a lot with time. Unlike analog video transmitters which when they are switched on transmit all the time (100% channel usage time), Wifi networks only occupy the channel when there is actually data to be transmitted. So it can well be that you wifibroadcast setup runs quite good with some wifi networks around. But this is only as long as nobody is generating a lot of traffic (i.e. reading emails or surfing forums), as soon as somebody starts a large download or watches a video over his wifi connection, the channel will be occupied and wifibroadcast traffic will get delayed.

_How to tell you are on a free channel:_

- Use the airodump wifi monitor feature (needs to be enabled in wifibroadcast-1.txt). It will scan for wifi network around and give you an idea of channel usage.
  Important: This wifi monitor will only show wifi traffic, so if you see a free channel, this is not a guarantee that it's really free, it just means there are no wifi networks transmitting on it.

- Use the automatic bitrate measuring feature (enabled by default). When the transmitter starts, it will measure the available bandwidth on the channel by sending dummy data as fast as it can. Since the wifi cards will 'yield' if there are already ongoing transmissions, measured bitrate will be considerably lower. With standard settings you should see around 6000kbit of bitrate displayed if on a free channel. If it's less than 5500kbit, try moving to another channel. Also try to start-up the transmitter several times, measured bitrate should be within ~5%, if you get highly varying results this is a sure sign for a used channel.

- Starting with 1.6RC4: Check the skipped FEC data display: If the transmitter senses that it cannot transmit because the available bandwidth is too low, it will skip FEC data (to instantly reduce transmitted amount of data and avoid delays). If you use EZ-Wifibroadcast with standard settings, this should not happen and is a clear sign for a used channel.


_If you cannot move to a free channel:_

Especially which a "bursty" type of channel usage (i.e. typical 2.4Ghz channels available with lots of wifi networks and other RF sources around) it's not easy to guarantee an error and latency free transmissions. In that case you, will have to tune wifi medium access settings as well as wifibroadcast FEC settings and bitrates.

In general, there are two options to solve this issue:
1) Reduce channel usage time for wifibroadcast. That is, either transmit "faster" (with a higher bitrate), or transmit less data. The "nice" and preferred way.

- Keep FEC and wifi bitrate settings the same, just reduce BITRATE_PERCENT. Problem with that is just, depending on the channel usage, you may need to reduce bitrate  quite a lot which will also reduce video quality.
- Keep FEC settings and BITRATE_PERCENT the same, but increase wifi bitrate. This way, the same amount of video data will be transferred, but with less channel usage due to the higher bitrate. Obviously, this will decrease range.

2) Don't reduce channel usage time, just transmit anyway, basically step over the other traffic. The "not-so-nice-way". Not preferred, as it only works with Atheros and obviously it will affect others more and also because it will also increase collisions (and thus glitches) for wifibroadcast transmission.
- Set thresh62 in /etc/modprobe.d/ath9k_hw.conf to a higher value, try 38. Set aifs=0 cwmin=0 cwmax=0.
If you do this, you will probably also notice increased packetloss and badblocks, you can counter-act this to an extent by increasing the FEC "window-size", try
12/6/1024 FEC for example.