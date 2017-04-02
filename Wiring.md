### Important notes:

- Many (even expensive brandname) USB power supplies or portable power banks either don't deliver the advertised amps and/or don't maintain stable 5Volts. 

- The same applies for USB cables and connectors. Many connectors have bad tolerances (too thin, which makes them wiggle and prone to intermittent connections) and cables use 28AWG or even less which causes too much voltage drop, even on short 30cm cables.

- Make sure that you supply the Pi with stable 5V. Use atleast a 2A BEC and short wires with atleast 20AWG (0.5mm²). 

- Power the Pi through the GPIO Pins, not through the micro USB Port. Do not use USB cables and connectors, solder everything directly or use proper connectors like e.g. XH balancer connectors or similar

- Do not power high-output cards like the AWUS036NHA or AWUS051/052NH through the USB ports of the Pi, connect them directly to the BEC. 

- Consider adding a low-ESR electrolytic capacitor near to the Pi and high-output card to stabilize the power. If you have a high-power motor setup (race-quad for example), also consider adding low-ESR caps near to the ESCs or at the central PDB to make sure the BEC gets clean power.

- Make sure the camera flat cable is properly inserted and fixed. Consider adding a drop of hotglue or tape to secure it.

- Make sure the Pi do doesn't get too hot. If it reaches 80 degrees C, it will reduce CPU speed to prevent it from overheating. This will make the video stream stall/stutter or cause the video stream to be delayed several seconds! Consider adding a small heatsink if using it in an enclosed/bad ventilated setup.

- Make sure the wifi cards don't get too hot. This will cause badblocks and/or the power output will be reduced significantly.

- Keep some distance to components that carry high currents and emit electromagnetic fields like motors, ESCs, power wires etc.

## Wiring:

![](https://raw.githubusercontent.com/bortek/EZ-WifiBroadcast/master/wiki-content/Pi0-Wiring-small.jpg)
![](https://raw.githubusercontent.com/bortek/EZ-WifiBroadcast/master/wiki-content/Pi3-Wiring-small.jpg)
![](https://raw.githubusercontent.com/bortek/EZ-WifiBroadcast/master/wiki-content/052nh-wiring.jpg)

