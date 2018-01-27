# autochromium

Automate chromium-browser on Raspberry PI 3, with python.

### Overview
The chromium browser version for Raspberry PI is very versatile but if you want to customize some behaviours, you need some automation.

In this project I'll use selenium for python to show how to automatically activate the voice search in the google search page.

### Prepare your Raspberry
0. I used a [Raspberry PI 3 Model B Scheda madre CPU 1.2 GHz Quad Core, 1 GB RAM](https://www.amazon.it/gp/product/B01CD5VC92/ref=oh_aui_search_detailpage?ie=UTF8&psc=1) bought at Amazon
1. Start from a clean sd: I tested 8M and 32M SD Samsung cards.
2. Install "Raspian Jessie with Desktop" or "Raspbian Stretch with Desktop", I tested:
   - Stretch "2017-11-29-raspbian-stretch.img" downloaded and with "installation guide" at [Download Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/)
   - Jessie "2017-04-10-raspbian-jessie.img"
   - Jessie "2016-11-25-raspbian-jessie.img"
3. (Optional, if you don't have screen, keyboard and mouse) Prepare the SD you just created for headless operations following these instructions. [
Raspbian Stretch Headless Setup Procedure](https://www.raspberrypi.org/forums/viewtopic.php?t=191252) 
4. Install the python selenium module with the command
```
pip3 selenium
```

5. Install the chromedriver driver
chromedriver serves as a bridge between chromium-browser and Selenium WebDriver
For Raspberry PI 3 you need a chromedriver version which is compatible with your chromium-browser.
For instance, on Nov-17 the very latest raspbian version, named 2017-11-29-raspbian-stretch comes with chromium-browser version: 
Version 60.0.3112.89 (Developer Build) Built on Ubuntu 14.04, running on Raspbian 9.3 (32-bit)
To see it, simply launch chromium-browser from the graphical interface 



e right version of Download the right armhf (yes, Raspberry PI 3 is based on armhf CPU architecture) version of chromedriver.



[![](https://github.com/guido57/MyThermostat/blob/master/off.PNG)](https://github.com/guido57/MyThermostat/blob/master/off.PNG)
- Manual. The relay is on if the room temperature is below the set temperature

[![](https://github.com/guido57/MyThermostat/blob/master/manual.PNG)](https://github.com/guido57/MyThermostat/blob/master/manual.PNG)
- Thermostat. The relay is on if the room temperature is below the set temperature at that time range.

[![](https://github.com/guido57/MyThermostat/blob/master/thermostat.PNG)](https://github.com/guido57/MyThermostat/blob/master/thermostat.PNG)

See the logic diagram below also.

### Prepare your Raspberry
0. I used a [Raspberry PI 3 Model B Scheda madre CPU 1.2 GHz Quad Core, 1 GB RAM](https://www.amazon.it/gp/product/B01CD5VC92/ref=oh_aui_search_detailpage?ie=UTF8&psc=1) bought at Amazon
1. Start from a clean sd: I tested 8M and 32M SD Samsung cards.
2. Install "Raspian Jessie with Desktop" or "Raspbian Stretch with Desktop", I tested:
   - Stretch "2017-11-29-raspbian-stretch.img" downloaded and with "installation guide" at [Download Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/)
   - Jessie "2017-04-10-raspbian-jessie.img"
   - Jessie "2016-11-25-raspbian-jessie.img"
3. (Optional, if you don't have screen, keyboard and mouse) Prepare the SD you just created for headless operations following these instructions. [
Raspbian Stretch Headless Setup Procedure](https://www.raspberrypi.org/forums/viewtopic.php?t=191252) 
4. Install the python PIL module with the command
```
pip3 pillow
