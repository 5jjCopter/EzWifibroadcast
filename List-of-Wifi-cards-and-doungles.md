In general, the following chipsets should work:

- Atheros AR9271
- Ralink RT2070, RT2770, RT2870, RT3070, RT3071, RT3072, RT3370, RT3572, RT5370, RT5372, RT3573, RT5572
- MediaTek MT7601


Examples:
- CSL 300Mbit Stick (2.4/5Ghz, Diversity, RT5572 chipset)
- Alfa AWUS036NHA (2.3/2.4Ghz, high power, Atheros AR9271 chipset)
- Ubiquiti Wifistation USB (2.3/2.4Ghz, high power, Atheros AR9271 chipset)
- TPLink TL-WN722N V1 (2.3/2.4Ghz, Atheros AR9271 chipset)
- ALFA AWUS051NH v2 (2.4Ghz/5Ghz, high power, Ralink RT3572 chipset)
- ALFA AWUS052NH v2 (2.4Ghz/5Ghz, Diversity, high power, Ralink chipset)
- TP-Link-TL-WDN3200 (2.4/5Ghz, Diversity, RT5572 chipset) 
- Rosewill RNX-N600UBE (2.4/5Ghz, Diversity, RT5572 chipset, txpower unknown currently, RT5572 chipset)
- AW-NU138 (2.3/2.4Ghz, Atheros AR9271 chipset)

Pay attention to the version number of the wifi adapter, manufacturers often use a completely different chipset with a different version number!

### **AWUS036NHA**
This adapter will provide around 280mW output power. Ranges of several kilometers have been reported (with directional antennas though).

### **Ubiquit Wifistation USB**
This adapter is quite large, but seems to have a good quality amp on it. Useable TXPower is not yet determined, but should be slightly higher than the AWUSH036NHA.

### **TL-WN722N V1**
This adapter will provide around 60mW output power. Range should be roughly around 800-1000m with 2.1dbi stock antennas.

_**IMPORTANT:**_ There have been reports that the TL-WN722N V1 seems to be replaced by V2 versions. These V2 versions use a completely different chipset and are _not_ compatible. Consider asking the seller for the version, if it says "V2" on the back of the dongle it's the wrong chipset!

_**IMPORTANT:**_ Under certain circumstances, the second antenna on the PCB causes bad reception. Please disconnect the antenna by removing the white PCB component on the back of the PCB like shown below (in the picture, the component was soldered to the upper pad to be able to reverse the mod if needed)

![722N](https://raw.githubusercontent.com/bortek/EZ-WifiBroadcast/master/wiki-content/722n-mod.jpg)



### AW-NU138
This adapter is very small, output power about 50mW. The internal antenna can be de-soldered and replaced with an external antenna. Since it's very small it runs quite warm, good cooling is needed.



### **CSL 300Mbit stick**
This adapter provides around 30mw output power. Range on 5Ghz is not very high, around 200-300m. Stock antennas are not usable on 5Ghz, as they are simple 2.4Ghz 2.1dbi sleeved-dipole antennas.

When used as an Rx dongle, bad blocks can occur when the received signal strength is higher than -20dbm. This can be worked-around by using more than one adapter and pointing antennas in different directions / polarizations.



### **AWUS051NH**
This adapter will provide around 330mw output power. Range on 5Ghz is around 800-1000m. Stock antenna is not recommended because they have 5dbi gain, which will give a too-flat radiation pattern.



### **AWUS052NH**
This adapter will provide around 330mw output power. This is the same adapter as the 051NH, but with two TX chains. Stock antennas are not recommended because they have 5dbi gain, which will give a too-flat radiation pattern.


## Finding alternatives

For cheap alternatives check out the usual computer stores and maybe consider Aliexpress. Be a little careful, some cards are of questionable quality. However, often, brandname wifi modules or USB sticks originally made for applications like Smart-TVs etc. are offered for a very good price.


A good way to find out more about wifi sticks and modules offered online is to look for product numbers, chipsets, or even better an FCC ID. With those, try to find high-res internal photos of the cards, to find out the chipset and the amps used.

Search the web for those numbers and also these two very helpful sites:
* https://fccid.io/ (FCC documents which contain internal photos)
* https://wikidevi.com/wiki/ (general infos and sometimes photos)

When you have found photos, google for the numbers on the amps to find a datasheet giving a rough estimate about the expectable output power.

It would be nice if you report back your findings in case you tried a wifi card that is not listed here.


## External amp
Another way to increase output power is to use a low-power wifi stick combined with an external amp like this "2W" amp:

https://www.banggood.com/2_4G-2W-Radio-Signal-Booster-Antenna-Feeder-For-DJI-Phantom-Multirotor-TX-Extend-Range-p-986756.html?rmmds=search

Real output power is around 600mW with a low-power AR9271 stick.
