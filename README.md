
# Raspberry-Pi_Workspace

## 192.168.0.10

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
git clone https://github.com/adafruit/Adafruit_Python_DHT.git

cd Adafruit_Python_DHT
sudo python3 setup.py install

// inside of the folder
cd examples
// you can check by ls -al
ls -al
// there's AdafuitDHT.py
python3 AdafruitDHT.py 2302 17
// * you can check the instruction
cat AdafruitDHT.py
```

## The Web Application Stack
User & Web Browser


[ Server Operating System ]


Web Server -- NGINX


Application Server -- nWSGI


App framework -- Flask


Application -- Raspbian Streatch Lite, debian


[ Raspberry Pi Server Hardware -- Raspberry Pi ]


### 35. Set up system Python - preparation
```
sudo apt-get install build-essential
sudo apt-get install libncurses5-dev libncursesw5-dev libreadline6-dev
sudo apt-get install libbz2-dev libexpat1-dev liblzma-dev zlib1g-dev libsqlite3-dev libgdbm-dev tk8.5-dev
sudo apt-get install python-dev
sudo apt-get install libssl-dev openssl

```
### 36. Download, compile and install Python 3
```
mkdir python-source
cd python-source
wget https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tgz
tar zxvf Python-3.6.4.tgz
cd Python-3.6.4
./configure --prefix=/usr/local/opt/python-3.6.4
make        (takes time)
sudo make install
usr/local/opt/python-3.6.4/bin/python3.6 --version      (to check out the version)
```
### 37. Setup the app Python Virtual Environment
In the Python-3.6.4 folder, 
```
sudo su

cd /var
ls -al
```
'sudo su' lets you enter root@ mode in Python-3.6.4
```
mkdir www
cd www
mkdir lab_app
ls -al
cd lab_app
```
Inside of the folder of lab_app, extracts Python virtual environment called venv.
```
/usr/local/opt/python-3.6.4/bin/python3.6.4/bin/python3.6 -m venv .
// * if I'm not in the folder yet, this works as well (or they're equivalent, . or location)
/usr/local/opt/python-3.6.4/bin/python3.6.4/bin/python3.6 -m venv /var/www/lab_app/
```
After that, you will be able to see more files downloaded
```
ls -al bin (just for checking)
```
Even if you went through all, you still see the default Python on Raspberry Pi. In order to use latest version that we just installed, (in the folder, lab_app) 
```
. bin/activate
python --version
deactivate (always able to go back)
```

### 38. Setup Nginx
Installment on the virtual environment (latest version),
```
apt-get install nginx
```
To check it's successfully installed, open a browser and put Raspberry Pi IP address. If so, you will be able to see Nginx welcome page.

### 39. Flask
Installment on the virtual environment (latest version),
```
pip install flask

(if you want to upgrade pip)
pip install --upgrade pip
```
```
vim hello.py
```
```python
from flask import Flask
app = Flask(__name__)
@app.route("/")

# after app.route, all will be called
def hello():
  return "Hello World"

# Without the run function, Flask won't work
if __name__ == "__main__":
  app.run(host='0.0.0.0', port=8080)
```
Open a browser, put IP address with port number (8080)

### 40. Simple Flask app

```python
from flask import Flask
app = Flask(__name__)
@app.route("/")

# after app.route, all will be called
def hello():
  return "Hello World"
  
# http://ip:8080/example
@app.route("/example")
def example_route():
  return "This is an example route"

# Without the run function, Flask won't work
if __name__ == "__main__":
  app.run(host='0.0.0.0', port=8080)

# But even if, you commented run function, you can run by using 'flask run --host=0.0.0.0 --port=1234'
# Missing host and port are not accessble due to permission
```
References
- [Flask](flask.pocoo.org)
- [Python main](txplo.re/pymain)

### 41. USWGI Installation
```
pip install uwsgi
```

### 42. Nginx configuration
Remove Nginx welcome page
```
rm /etc/nginx/sites-enabled/default
```
Create Nginx configuration file
```
vim lab_app_nginx.conf
```
```
server {
  listen 80;
  server_name localhost;
  charset utf-8;
  client_max_body_size 75M;
  
  location /static {
    root /var/www/lab_app/;
  }
  
  location / { try_files $uri @labapp; }
  location @labapp {
      include uwsgi_params;
      uwsgi_pass unix:/var/www/lab_app/lab_app_uwsgi.sock;
  }
}
```

```
ln -s /var/www/lab_app/lab_app_nginx.conf /etc/nginx/conf.d/
ls -al /etc/nginx/conf.d/   ## to check configure file is set or not
/etc/init.d/nginx restart   ## restart nginx
```
