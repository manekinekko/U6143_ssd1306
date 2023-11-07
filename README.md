# U6143_ssd1306
## Preparation
```bash
sudo raspi-config
```
Choose Interface Options 
Enable i2c

##  Clone U6143_ssd1306 library 
```bash
git clone https://github.com/UCTRONICS/U6143_ssd1306.git
```
## Compile 
```bash
cd U6143_ssd1306/C
```
```bash
sudo make clean && sudo make 
```
## Run 
```
sudo ./display
```

## Add automatic start script
- Open the rc.local file 
```bash
sudo nano /etc/rc.local
```
- Add command to the rc.local file
```bash
cd /home/pi/U6143_ssd1306/C
sudo make clean 
sudo make 
sudo ./display &
```
- reboot your system

## For older 0.91 inch lcd without mcu 
- For the older version lcd without mcu controller, you can use python demo
- Install the dependent library files
```bash
sudo pip3 install adafruit-circuitpython-ssd1306
sudo apt-get install python3-pip
sudo apt-get install python3-pil
```
- Test demo 
```bash 
cd /home/pi/U6143_ssd1306/python 
sudo python3 ssd1306_stats.py
```

## Custom display temperature type 
- Open the U6143_ssd1306/C/ssd1306_i2c.h file. You can modify the value of the TEMPERATURE_TYPE variable to change the type of temperature displayed. (The default is Fahrenheit)
![EasyBehavior](https://github.com/UCTRONICS/pic/blob/master/OLED/select_temperature.jpg)


## Custom display IPADDRESS_TYPE type 
- Open the U6143_ssd1306/C/ssd1306_i2c.h file. You can modify the value of the IPADDRESS_TYPE variable to change the type of IP displayed. (The default is ETH0)
![EasyBehavior](https://github.com/UCTRONICS/pic/blob/master/OLED/select_ip.jpg)

## Custom display information 
- Open the U6143_ssd1306/C/ssd1306_i2c.h file. You can modify the value of the IP_SWITCH variable to determine whether to display the IP address or custom information. (The custom IP address is displayed by default)
![EasyBehavior](https://github.com/UCTRONICS/pic/blob/master/OLED/custom_display.jpg)

## Cluster setup script (WIP):

```
ssh hostname "sudo locale-gen --purge en_US.UTF-8"
ssh hostname "echo -e 'LANG=\"en_US.UTF-8"\nLANGUAGE="en_US:en\"\n' > /etc/default/locale"
ssh hostname "sudo apt-get update && sudo apt-get install raspi-config build-essential i2c-tools libi2c-dev -y"
ssh hostname "git clone https://github.com/manekinekko/U6143_ssd1306.git && cd U6143_ssd1306/C && sudo make clean && sudo make"
ssh hostname "sudo touch /etc/rc.local && echo 'sudo /home/wassim/U6143_ssd1306/C/display &' >> /etc/rc.local"
ssh hostname "sudo chmod +x /etc/rc.local && sudo systemctl enable rc-local.service && sudo systemctl start  rc-local.service"

#!/bin/sh

sudo /home/wassim/U6143_ssd1306/C/display &

exit 0

```







