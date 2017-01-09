In some cases instead of Pi camera we might want to input the video signal from an external camera or another video source. For example a GoPro or DSLR camera which has an HDMI output. NOTE: That this solutions might add additional latency to the video signal.

## Auvidea B101
This is a HDMI to CSI-2 Bridge (15 pin FPC) adapter. The output from this card plug in directly into camera slot on Pi. 

Here is the response (via email) from Auvidea about the supported resolution. "the B101 only supports 1080p25, because this is a limitation of the Toshiba driver in the RPi. However there will be the V20, which has SDI input and it fully emulates the Pi camera. Here 1080p at any frame rate up to 30 Hz is supported. The Pi seems to max out at 47Hz. We are looking at new versions which will have LVDS and HDMI input. The B101 rev 3 supports all Pi models."

Technical details are here http://www.auvidea.eu/download/manual/B10x_technical_reference_1.3.pdf

More info on Auvidea website http://auvidea.eu/


## Lintest Systems PiCapture HD1
This card has been tested by one of the users and reported on the Forum to work Ok. It has both HDMI and Composite inputs. 

- Set your external HDMI camera to 1920x1080 progressive with 25 or 30fps
- Check that the HD1 adapter has correctly detected the above camera resolution (LEDs)
- Set this in wifibroadcast-1.txt:

WIDTH=1920

HEIGHT=1080

FPS=25  #(or 30)

EXTRAPARAMS="-cd H264 -n -fl -ih -pf high -md 1 -awb off -awbg 1.0,1.0 -ex off"


More info here:

https://www.rcgroups.com/forums/showpost.php?p=36584377&postcount=1960

https://www.rcgroups.com/forums/showthread.php?2664393-EZ-WifiBroadcast-cheap-digital-HD-transmission-made-easy%21/page131#post36586673

https://lintestsystems.com/products/picapture-hd1

