Important: Except for low-power Ralink dongles (see below), there is no need to increase transmit power! If you have range problems, check your wiring, power supply, antennas etc. and make sure you are on a free channel.


- Alfa AWUS036NHA: Card is set near maximum power, another 1-2db could be gained, but at the expense of wider signal shoulders and uncleaner signal

- Alfa 051/052NH: Card is set to maximum power, do not increase, you _will_ get badblocks if you do.

- TPlink 722N (and other low-power AR9271 dongles): Card is set to maximum power, no need to increase.

- CSL 300Mbit stick (and other low-power Ralink dongles): Increase txpower to +4 for maximum output.

- Ubiquiti WifiStation USB: For these cards, transmit power needs to be decreased. Maximum txpower setting is not yet known, probably somewhere between 46 and 54. Start with 46 to be on the safe side.

