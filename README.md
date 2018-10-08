
# Raspberry-Pi_Workspace

## 192.168.0.15

### List of parts
https://www.txplore.com/p/rpifs-parts


**To complete this project, you will need the following parts:**

- Raspberry Pi 3 Model B (RPi 2 will also work very well) | Amazon US | Amazon UK | Amazon DE |
- Case for Raspberry Pi 3 | Amazon US | Amazon UK | Amazon DE |
- 5V 2500mA Micro USB Mains Power Wall Supply for Raspberry Pi | Amazon US | Amazon UK | Amazon DE |
- SanDisk Ultra 8GB Class 10 UHS-I MicroSDHC Memory Card with Adapter | Amazon US | Amazon UK | Amazon DE |
- Sparkfun 500 1/4W Resistor Kit | Amazon US | Amazon UK | Amazon DE |
- RJ45 Cat5e Ethernet Patch Cable | Amazon US | Amazon UK | Amazon DE |
- JBtek Raspberry Pi Micro USB Cable with ON / OFF Switch | Amazon US | Amazon UK | Amazon DE |
- Red LED Diodes | Amazon US | Amazon UK | Amazon DE |
- DHT22 temperature and humidity sensor | Amazon US | Amazon UK | Amazon DE |
- A breadboard-friendly momentary button | Amazon US | Amazon UK | Amazon DE |
- Mini breadboard | Amazon US | Amazon UK | Amazon DE |
- Jumper wires | Amazon US | Amazon UK | Amazon DE |

### Raspberry Pi 3 Spec
- The Raspberry Pi 3, like the Raspberry Pi 2, comes with 1GByte of SDRAM.
- The Raspberry Pi Model B (2 and 3) have 4 USB2.0 ports, an Ethernet 10/100 Mbps connector, HDMI and headphone ports, camera and display interfaces, plus a mini-USB port for power.
- The Raspberry Pi 3 also has built-in Wifi 802.11n LAN, and Bluetooth 4.0.
- The Raspberry Pi Model B (2 and 3) have a 40-pin GPIO header. Not all of the pins are General Purpose Input Outputs. Several have specific functions like GND, 5V or 3.3V.
- HAT: Hardware Attached on Top, a HAT is board the size of the Raspberry Pi that plugs into the 40-pin headers and implements various functionalities, like displays and relays.
- The Raspberry Pi Foundation recommends a 5V, 2.5A power supply. If your application does not include power-hungry peripherals, like LCD screens, relays and dics, you can use smaller supplies, like 1.5A. However, using the official 5.1V, 2.5A power supply can help avoid many common power-related problems.




### raspberrypi.org
Raspbian-stretch-lite.img 

etcher.io
- A utility for copying an image to SD cards

txplo.re/rpissh
- How to set up SSH on the Raspberry Pi
- SSH file is dealing with booting configure file named **wpa_supplicant.conf**


Default id and password, pi, raspberry
sudo - super user do, or substitute user do

sudo raspi-config

***Windows and Mac are pretty much similar but Windows requiring additional program to download***

## Raspbian Lite Set up
- format SD card and burn with image file. (I used Etcher)
- create SSH file without any extension. 
```
network {
..
}  
```
- connect Ethernet and power and wait about two minutes
- configure network with **Advaned IP Scanner** and **puTTY**
- get ip address of Raspberry Pi and connect with puTTY (mine is 192.168.0.15)


## sudo mode that allows you to control that other user can't

```
sudo su
ls - alk
ls -al

cd /proc
ls -al

exit
```

Raspberry Pi Configure
```
sudo raspi-config
```

Nano Text Editor to enable the 'root' user login with SSH
```
sudo su
nano /etc/ssh/sshd_config 

#PermitRootLogin (uncommented delete #)
->
PermitRootLogin yes
/etc/init.d/ssh/ restart

passwd root

```

Shutdown Raspberry Pi
```
sudo shutdown -r (reboot or restart)
sudo shutdown -h (hold)
sudo shutdown -h now
```

Backup Image file (Win32 Imager)
- shutdown rasberry Pi first with command

Install Python3
```
sudo apt-get install python3
```
Install Python3 (pip3)
```
sudo apt-get install python3 pip
```
If 'pip3 --version'' is not working then, you might need to update it.
```
sudo apt-get update
```
Install rpi.gpio package on pip3
```
pip3 install rpi.gpio
```
### Turn on light on pin 7
```python
import RPi.GPIO as GPIO
pin = 7
GPIO.setmode(GPIO.BOARD)
GPIO.setup(pin, GPIO.OUT)
GPIO.output(pin, GPIO.HIGH)
GPIO.output(pin, GPIO.LOW)
```

Install offical simple editor, vim
```
sudo apt-get install vim
```
Create file by vim
```
vim button.py
```
Check file
```
cat button.py
```


list (on RaspberryPi)
```
ls -al
```

### button.py
```python
import RPi.GPIO as GPIO
import time
inPin = 8
GPIO.setwarnings(False)
GPIO.setmode(GPIO.BOARD)
GPIO.setup(inPin, GPIO.IN)
while True:
  value = GPIO.input(inPin)
  if value:
    print("Pressed")
  else:
    print("Not Pressed")
  time.sleep(0.1)
GPIO.cleanup()
```

### button_led.py
```python
import RPi.GPIO as GPIO
import time
inPin = 8   ## Swtich connected to pin 8
ledPin = 7    ## LED connected to pin 7
GPIO.setwarnings(False)   ## Turn off warnings
GPIO.setmode(GPIO.BOARD)    ## Use BOARD pin numbering
GPIO.setup(inPin, GPIO.IN)    ## Set pin 8 to INPUT
GPIO.setup(ledPin, GPIO.OUT)    ## Set pin 7 to OUTPUT
while True:   ## Do this forever
  value = GPIO.input(inPin)   Read input from swtich
  print(value)
  if value:   ## If switch is released
    print("Pressed")
    GPIO.output(ledPin, GPIO.HIGH)    ## Turn LED on
  else:
    print("Not Pressed:)
    GPIO.output(ledPin, GPIO.LOW)   ## Turn LED off
  time.sleep(0.1)
GPIO.cleanup()
```


```
sudo apt-get install git-core
git config --global user.email. allen@allengoo.com
git config --global user.name "gooallen"
git clone https://github.com/.../.git
```
