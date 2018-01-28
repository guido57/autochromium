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

- Now go to the Canonical Group web site, which develops an mantains Ubuntu and its armhf chromium-browser version. 
[https://launchpad.net/ubuntu/trusty/armhf/chromium-chromedriver](https://launchpad.net/ubuntu/trusty/armhf/chromium-chromedriver)

- Look for the chromedriver version whose number version is closest to the one of your chromium-browser and download it as a deb package.
For example, I have chromium-browser Version 60.0.3112.89, so the closest at that page is 60.0.3112.113. So I downloaded 
chromium-chromedriver_60.0.3112.113-0ubuntu0.14.04.1194_armhf.deb 
on my Raspberry PI.

- Then I installed it double clicking on the icon.

- Then I asked the version of the chromedriver with the following command:
```
/usr/lib/chromium-browser/chromedriver -v
```
but instead of obtaining the version number I got the following error:
```
/usr/lib/chromium-browser/chromedriver: error while loading shared libraries: libbase.so: cannot open shared object file: No such file or directory
```
which means that a shared library which chromedriver expected to be present in the chromium-browser installation is not present!

