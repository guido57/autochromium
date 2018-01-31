# autochromium

Automate chromium-browser on Raspberry PI 3, with python.

### Overview
The chromium browser version for Raspberry PI is very versatile but if you want to customize some behaviours, you need some automation.

In this project I'll use selenium for python to show how to automatically activate the voice search in the google search page.

### Collect Hardware
1. [Raspberry PI 3 Model B Scheda madre CPU 1.2 GHz Quad Core, 1 GB RAM](https://www.amazon.it/gp/product/B01CD5VC92/ref=oh_aui_search_detailpage?ie=UTF8&psc=1) bought on Amazon
2. USB microphone [I bought this on Amazon](https://www.amazon.it/Microfono-Piccolo-desktop-Discorso-registrazione/dp/B00XU1GHO4/ref=sr_1_5?s=electronics&ie=UTF8&qid=1517425711&sr=1-5&keywords=microfono+usb)
3. amplified speaker (any)
4. (optional) HDMI monitor or TFT LCD 3.5" screen

### Prepare your Raspberry
1. Start from a clean sd: I tested 8M and 32M SD Samsung cards.
2. Install "Raspian Jessie with Desktop" or "Raspbian Stretch with Desktop", I tested:
   - Stretch "2017-11-29-raspbian-stretch.img" downloaded and with "installation guide" at [Download Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/)
   - Jessie "2017-04-10-raspbian-jessie.img"
   - Jessie "2016-11-25-raspbian-jessie.img"
3. (Optional, if you don't have screen, keyboard and mouse) Prepare the SD you just created for headless operations following these instructions. [
Raspbian Stretch Headless Setup Procedure](https://www.raspberrypi.org/forums/viewtopic.php?t=191252) 

### Install Software

1. Install the python selenium module with the command
```
pip3 selenium
```

2. Get your chromium-browser version

chromedriver serves as a bridge between chromium-browser and Selenium WebDriver.

For Raspberry PI 3 you need a chromedriver version which is compatible with your chromium-browser.
For instance, the very latest raspbian version at this time (Jan-18) is "2017-11-29-raspbian-stretch" and it comes with chromium-browser version: 
Version 60.0.3112.89 (Developer Build) Built on Ubuntu 14.04, running on Raspbian 9.3 (32-bit)

To know your specific chromium-browser version, simply:
1. launch chromium-browser from the graphical interface 
2. click on the menu icon
3. click on About Chromium as you see here:
[![](https://github.com/guido57/autochromium/blob/master/chromium-browser-v.PNG)]

or from the shell:
```
chromium-browser --version
```

3. Get your chromedriver version and check if it works.

- Go to the Canonical Group web site, which develops and mantains Ubuntu and its armhf chromium-browser version. 
[https://launchpad.net/ubuntu/trusty/armhf/chromium-chromedriver](https://launchpad.net/ubuntu/trusty/armhf/chromium-chromedriver)

- Look for the most recent version and download it as a deb package.
- Then intall it double clicking on its icon.
- Then to check if everything is OK, ask the version of the chromedriver with the following command:
```
/usr/lib/chromium-browser/chromedriver -v
```
A correct answer could be:
```
/usr/lib/chromium-browser/chromedriver -v
ChromeDriver 2.33
```

The most recent:
- chromium-chromedriver_63.0.3239.132-0ubuntu0.14.04.1_armhf.deb

is OK. But I succcessfully tested also:
- chromium-chromedriver_62.0.3202.94-0ubuntu0.14.04.1215_armhf.deb
- chromium-chromedriver_61.0.3163.100-0ubuntu0.14.04.1202_armhf.deb

while this one:
- chromium-chromedriver_60.0.3112.113-0ubuntu0.14.04.1194_armhf.deb 

gave me the following error:
```
/usr/lib/chromium-browser/chromedriver: error while loading shared libraries: libbase.so: cannot open shared object file: No such file or directory
```
that means that a shared library (libbase.so) which chromedriver expected to be present in the chromium-browser installation is not present!


### Set speaker and microphone
1. Simply connect any audio amplified speaker to the 3.5mm audio output jack of your Raspberry
2. Simply insert your USB microphone to any USB socket of your Raspberry
3. Determine card and device of your "bcm2835 ALSA" integrated audio which serves the 3.5mm jack with:
```
aplay -l
'''
I got card 0 and device 0:
'''
**** List of PLAYBACK Hardware Devices ****
card **0**: ALSA [bcm2835 ALSA], device **0**: bcm2835 ALSA [**bcm2835 ALSA**]
  Subdevices: 8/8
  Subdevice #0: subdevice #0
  Subdevice #1: subdevice #1
  Subdevice #2: subdevice #2
  Subdevice #3: subdevice #3
  Subdevice #4: subdevice #4
  Subdevice #5: subdevice #5
  Subdevice #6: subdevice #6
  Subdevice #7: subdevice #7
card 0: ALSA [bcm2835 ALSA], device 1: bcm2835 ALSA [bcm2835 IEC958/HDMI]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
'''

4. Determine card and device of your USB Audio capture device (microphone):
```
arecord -l
'''
I got card 0 and device 0:
'''
**** List of CAPTURE Hardware Devices ****
card **1**: Device [USB PnP Sound Device], device **0**: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
'''

5. create or modify /home/pi/.asoundrc like the following:
```
pcm.!default {
	type asym
	playback.pcm {
		type plug
		slave.pcm "hw:0,0"
	}
	capture.pcm {
		type plug
		slave.pcm "hw:1,0"
	}

}

ctl.!default {
	type hw
	card 0
}
```

