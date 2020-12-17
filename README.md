# SensorNetwork20202_DashServer_SDS011_DHT22
Author: Danien Jarvis
Contacts:  jarvissan21@gmail.com

Successor to [SDS-011-Python](https://github.com/JarvisSan22/SDS-011-Python)
Happy to recive feedback, and to implement contributions  

Raspberry pi (RPI) or linux system base for a sensor network, of SDS011 and DHT22. 
Network made up of ESP8266 Sensor nodes sending data to the network base over a local ip. 
Using the previous code in [SDS-011-Python](https://github.com/JarvisSan22/SDS-011-Python), GPS maps walk and logger data can be run on a RPI 
Network data is displated using plotly dash for a nice clean interface.



![SDS-011](https://github.com/JarvisSan22/SDS-011-Python/blob/master/SDS011-setup.jpg)
![DASH1](https://github.com/JarvisSan22/SensorNetwork2020_DashServer_SDS011_DHT22/blob/master/DASH1.png)
![DASH2](https://github.com/JarvisSan22/SensorNetwork2020_DashServer_SDS011_DHT22/blob/master/DASH2.png)

# Kit List 
- [SDS011](https://www.amazon.co.uk/gp/product/B07D7BL33R/ref=as_li_tl?ie=UTF8&camp=1634&creative=6738&creativeASIN=B07D7BL33R&linkCode=as2&tag=jarvissan-21&linkId=40bb211f585f6fb48dd5feecb261bd3f)
- [RPI3](https://www.amazon.co.uk/gp/product/B01CI5879A/ref=as_li_tl?ie=UTF8&camp=1634&creative=6738&creativeASIN=B01CI5879A&linkCode=as2&tag=jarvissan-21&linkId=d64cc755f2dcf6ff27d37a7fc09b8ac5) 
- [GPS](https://www.amazon.co.uk/gp/product/B015E2XSSO/ref=as_li_tl?ie=UTF8&camp=1634&creative=6738&creativeASIN=B015E2XSSO&linkCode=as2&tag=jarvissan-21&linkId=8563986ebd9d60f3488a35d2cb5a34f4) 
- [DHT22](https://www.amazon.co.uk/gp/product/B072391SJV?ie=UTF8) 
- [ESP8266]()
- [BLINKT](https://www.amazon.co.uk/gp/product/B01J7Y332Q/ref=as_li_tl?ie=UTF8&camp=1634&creative=6738&creativeASIN=B01J7Y332Q&linkCode=as2&tag=jarvissan-21&linkId=dbda11585051ff253bc34c06913a4a40) 
- [Battery Pack](https://www.amazon.co.uk/gp/product/B07QTJDGJ1?ie=UTF8)


# Repository details 
1. **AQ_run** {Logging scipts, go into this folder for run details}
   - **data** {Folder to store data files }
   - **Scripts** 
     - 2 **DHT** {DHT repository}
     - 2 **DHT.py** {DHT 11 and 22 script}
     - 2 **GPS2.py** {GPS scipts}
     - 2 **sds_rec.py** {SDS011 get data sripts}
     - 2 **start.py**  {Start recording and logg data script}
     - 2 **status.py** {RPI3 status scripts, checks if running, and updates time}
     - 2 **variables.py** {RPI3 and sensors varaible script}
1. **AQ_Plot** {Plotter scripts, go into this folder for details on how to run}
   - **AQMapfunctions.py** {GPS Map plotting functions}
   - **AQfunctions_Archive_2019.py** {Archive of old code}
   - **GPS_MAP.html** {Example GPS Map generated by AQMapfunctions}
   - **Plots/**  {Additional plot generated by AQMapfuctions that are used in the GPS_Map.html}
   - **data/TestData** {Some example GPS data to test AQMapfunctions}
1. **AQ_nodes"" {See thie Directory for node set up}
  - **DHT22-Flashnode.ino {ESP8266 DHT22 Sensor node script}
1. **AQ_Plot_server** { Data reciver and Plotly Interface, see this reposity for set up details  }
   - **dash_server.py** {Plotly Dash, base sensor network interface}
   - **data_reciver.py** {Flask node data reciver code}
   - **MultiPage**
     - 2 **Dash_GPSmap_server.py** {Plotly Dash, with pages for sensor network and GPS maps}
    
  

RPI3 2019 Setup Video 2019, for previous  
[Set up Video](https://www.youtube.com/watch?v=fvaiyqwaWeM)

#Base Code set up 
```
sudo apt-get update
sudo apt-get upgrade
```

**WIfi set up** 
```
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```
add  your network network
```
network={
   ssid="{your interent name}"
   psk="{your internet password}"
}
```

**Download this repository**
```
git clone https://github.com/SensorNetwork2020_DashServer_SDS011_DHT22
```

# DHT22 Set up 

Intall the package

```
 'sudo python3  SDS-011-Python-master/AQ/Scripts/DHT/setup.py install'
```

# GPS Set up 
GPS Dongle G-mouse, set up video for setting up the dolge GPS as the RPI3 clock !!!
https://www.youtube.com/watch?v=Oag9qYuhMGg


1st get gps module
```
sudo apt-get install gpsd gpsd-clients python-gps chrony
```
2nd  in terminal 
```
sudo nano /etc/default/gpsd
```
set the following
``` 
START_DAEMON=”true”
USBAUTO=”true”
DEVICES=”/dev/ttyACM0″
GPSD_OPTIONS=”-n”
```
3rd  in the terminal 
```
sudo nano /etc/chrony/chrony.conf
```
Add the following line to the end of the file:

```
refclock SHM 0 offset 0.5 delay 0.2 refid NMEA
```
3rd Reboot the RPI3 ""sudo reboot""

4th  check that both are active in the terminal
```
systemctl is-active gpsd
systemctl is-active chronyd
su
```
5th see the data
```
gpsmon -n
```

# Options

# Blinkt set up install

1st get the blinkt packages  
```
curl https://get.pimoroni.com/blinkt | bash
```
2nd fit the blinket into the RPI3 



