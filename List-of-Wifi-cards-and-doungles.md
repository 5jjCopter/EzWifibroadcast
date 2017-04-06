## Wifi Cards:
The following Atheros chipsets should work:
- Atheros AR9271, Atheros AR9280, Atheros AR9287

The following Ralink chipsets should work:
 - RT2070, RT2770, RT2870, RT3070, RT3071, RT3072, RT3370, RT3572, RT5370, RT5372, RT5572

However, there might be whatever small issues that prevent some cards from working, so if you want to play it safe, choose one of the cards that have been tested by different people and definitely work:

- CSL 300Mbit Stick (2.4/5Ghz, Diversity, RT5572 chipset)
- Alfa AWUS036NHA (2.3/2.4Ghz, high power, Atheros AR9271 chipset)
- TPLink TL-WN722N (2.3/2.4Ghz, Atheros AR9271 chipset)
- ALFA AWUS051NH v2 (2.4Ghz/5Ghz, high power, Ralink RT3572 chipset)
- ALFA AWUS052NH v2 (2.4Ghz/5Ghz, Diversity, high power, Ralink chipset)
- TP-Link-TL-WDN3200 (2.4/5Ghz, Diversity, RT5572 chipset) 
- Ralink RT5572 (2.4/5Ghz, Diversity???, RT5572 chipset) 

On the other hand, if everybody gets the same cards, we'll never find out which other ones work. There are also very small and lightweight RT5370 cards available in china shops for under 4$. Aliexpress for example has a lot of cheap wifi cards in general. It would be nice if you report back your findings in case you tried a wifi card that is not listed here.


**AWUS036NHA**
This adapter will provide around 280mW output power. Ranges of several kilometers have been reported (with directional antennas though).



**TL-WN722N**
This adapter will provide around 60mW output power. Range should be roughly around 800-1000m with 2.1dbi stock antennas.
_**IMPORTANT:**_ Under certain circumstances, the second antenna on the PCB causes bad reception. Please disconnect the antenna by removing the white PCB component on the back of the PCB like shown below (in the picture, the component was soldered to the upper pad to be able to reverse the mod if needed)

![722N](https://raw.githubusercontent.com/bortek/EZ-WifiBroadcast/master/wiki-content/722n-mod.jpg)


**CSL 300Mbit stick**
This adapter provides around 30mw output power. Range on 5Ghz is not very high, around 200-300m. Stock antennas are not usable on 5Ghz, as they are simple 2.4Ghz 2.1dbi sleeved-dipole antennas.

When used as an Rx dongle, bad blocks can occur when the received signal strength is higher than -20dbm. This can be worked-around by using more than one adapter and pointing antennas in different directions / polarizations.



**AWUS051NH**
This adapter will provide around 330mw output power. Range on 5Ghz is around 800-1000m. Stock antenna is not recommended because they have 5dbi gain, which will give a too-flat radiation pattern.



**AWUS052NH**
This adapter will provide around 330mw output power. This is the same adapter as the 051NH, but with two TX chains. Stock antennas are not recommended because they have 5dbi gain, which will give a too-flat radiation pattern.



**TL-WN822N V2**
This adapter will provide around 60mw output power. Currently, there is an issue with injection when there are other signals present on the 2.4G band, not recommended as TX adapter.