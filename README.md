# Seeing Wand

Point the Seeing Wand, push the button, and it will tell you what it sees. This fun project can be built over a few hours and has a practical side for the vision impaired. Yes, "there is an app for that," but the form factor is much cooler and the cost less than a smartphone as it is based on the $10 Raspberry Pi Zero W.

Learn how to build the Seeing Wand at https://www.zakon.org/hobbes/projects/seeing_wand/



## My implementation

The above URL is not valid.  Here is the correct URL:
https://www.zakon.org/robert/projects/seeing_wand/

The Seeing Wand works by taking a picture of where it is pointed at when a button is pushed, sending the image to Microsoft's Cognitive Services to get a description, then speaking the description using the espeak text-to-speech (TTS) software. The camera used is Raspberry Pi's Camera Module v2, and the speaker is Pimoroni's SpeakerPhat. These are wired and packaged inside a tube with two momentary push buttons and a power source. For the example shown, we used a scrap piece of PVC and a 2200mAh power cube device charger with a 5V/1A output that was a conference tchotchke.


### My Fork

My fork of code repo:  https://github.com/jliu70/SeeingWand




~/Downloads/Assistive_Technology_for_All-HS#51_Digital.pdf
```
jliu@JEFFREYs-MBP ~/Downloads  % cat Assistive_Technology_for_All-HS\#51_Digital.pdf.txt 
https://www.zakon.org/robert/projects/seeing_wand/
https://www.youtube.com/watch?v=lwVa66x6-rw   4/8/2018
https://github.com/hobbez/SeeingWand/  (last commit 4 years ago)
```

### Pimoroni pHAT doesn't seem to be available anymore?
#### Adafruit alternatives?  
```
Adafruit I2S 3W Stereo Speaker Bonnet for Raspberry Pi - Mini Kit
https://www.adafruit.com/product/3346
https://learn.adafruit.com/adafruit-speaker-bonnet-for-raspberry-pi
Stereo Enclosed Speaker Set - 3W 4 Ohm
https://www.adafruit.com/product/1669
Pirate Audio: Speaker for Raspberry Pi - Built-in 1W Speaker
https://www.adafruit.com/product/4451
```
#### Adafruit hardware purchased for the seeing wand (Ordered all three on 1/22/2022)
```
2766079,1669,"Stereo Enclosed Speaker Set   3W 4 Ohm",2,7.5000,15,"Delivered 1/26/2022, Edison Proposal project / black Adafruit mailer spare 17L box by bookcase"
2766079,3346,"Adafruit I2S 3W Stereo Speaker Bonnet for Raspberry Pi",2,12.9500,25.9,"Delivered 1/26/2022 / Edison Proposal project / black Adafruit mailer spare 17L box by bookcase"
2766079,3663,"Hammer Header Female   Solderless Raspberry Pi Connector",4,3.2500,13,"Delivered 1/26/2022 / Edison Proposal project / black Adafruit mailer spare 17L box by bookcase"
2766079,4451,"Pirate Audio: Speaker for Raspberry Pi   Built in 1W Speaker",1,24.9500,24.95,"Delivered 1/26/2022, Edison Proposal project / black Adafruit mailer spare 17L box by bookcase"
```


## Setup Raspberry Pi
 
### Raspberry OS - Raspbian  - maybe stick with Buster instead of Bullseye due to picamera library
#raspberrypi   2/15/2022   A preview release of the Picamera2 library python, replacment for the deprecated Picamera library with release of Bullseye in November 2021
https://www.raspberrypi.com/news/a-preview-release-of-the-picamera2-library/
https://blog.adafruit.com/2022/02/18/a-preview-release-of-the-picamera2-library-piday-raspberrypi-raspberry_pi/




### Setup speaker hardware 

We have a few options:
- hamburger speaker
- adafruit hardware

NOTE: for quick test we can try with hamburger speaker first on a Raspberry Pi 4B first (pi zero does not have audio jack)
Reference: CircuitPython School - Playing Sound (wav or mp3) with PyGame on a Raspberry Pi-5F9cl4ZCqQ8.mp4

The espeak TTS software is installed with:
```
sudo apt-get install espeak
```

Quick test of espeak
```
espeak -ven+f3 -k5 -s120 "i do not know what i just saw"
```

#### 3/13/2022 2pm to 4pm 
When using buster, installing espeak seems to fail.

Will try again after updating the software

If you see an error
https://forums.raspberrypi.com/viewtopic.php?t=245073
```
~ $ sudo apt-get update
Get:1 http://raspbian.raspberrypi.org/raspbian buster InRelease [15.0 kB]
Get:2 http://archive.raspberrypi.org/debian buster InRelease [25.1 kB]
Get:3 http://archive.raspberrypi.org/debian buster/main armhf Packages [205 kB]
Reading package lists... Done    
E: Repository 'http://raspbian.raspberrypi.org/raspbian buster InRelease' changed its 'Suite' value from 'testing' to 'stable'
N: This must be accepted explicitly before updates for this repository can be applied. See apt-secure(8) manpage for details.
```
Fix is to run 
```
sudo apt update --allow-releaseinfo-change
sudo apt upgrade
```
NOTE: was able to install espeak after the upgrade and verified that the speak command works. (using the hamburger speak on the sania box 2GB 4B pi, with the 32GB sandisk SD card on the upper left slot)


### Setup camera hardware 


### Microsoft Cognitive Services - get an API key
https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/

Maybe start with free 12-month trial account
