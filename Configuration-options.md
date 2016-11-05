## Wifibroadcast.txt

The wifibroadcast.txt configuration file is split-up into three sections:

1. Common settings: These settings must be kept in-sync for both TX and RX
2. RX Settings: These settings only affect the RX
3. TX Settings: These settings only affect the TX


### Common settings

FREQ=

The following frequencies are supported:

2312, 2317, 2322, 2327, 2332, 2337, 2342, 2347, 2352, 2357, 2362, 2367, 2372, 2377, 2382, 2387, 2392, 2397, 2402, 2407

2412, 2417, 2422, 2427, 2432, 2437, 2442, 2447, 2452, 2457, 2462, 2467, 2472, 2484

2487, 2489, 2492, 2494, 2497, 2499, 2512, 2532, 2572, 2592, 2612, 2632, 2652, 2672, 2692, 2712

4920, 4940, 4960, 4980

5180, 5200, 5220, 5240, 5260, 5280, 5300, 5320

5500, 5520, 5540, 5560, 5580, 5600, 5620, 5640, 5660, 5680, 5700

5745, 5765, 5785, 5805, 5825


2.3Ghz and 2.5-2.7Ghz band only works with Atheros cards. 2.5-2.7Ghz is untested. 4.9Ghz band is only supported by CSL300Mbit Ralink 5572 dongles. Other Ralink cards may support these channels and also additional overlapping channels in the 5Ghz band, you may want to check with "iw list"



TXMODE=

Set this to "single" for single TX wifi card, for dual TX wifi cards set "alternate" or "duplicate". 

Alternate mode will treat both tx cards as one logical channel with twice the bandwidth by sending out packets on both  interfaces in an alternating pattern. This is the preferred dual TX mode.

Duplicate mode wil send _the same_ packets on both cards, i.e. it will simply duplicate the packets. This seems less optimal in terms of link resiliency, but lowers CPU usage significantly 



MAC_RX[0]=
FREQ_RX[0]=

MAC_TX[0]=
FREQ_TX[0]=

MAC addresses and frequency for the RX and TX wifi need to be set here when dual TX mode is enabled. Please note that counting starts with index 0. Maximum two cards supported for TX, maximum four cards supported for RX (Index 0-3).

