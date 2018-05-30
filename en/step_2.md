## What you will need

There are many different sensors available that you could use to make weather measurements. You don't have to use the exact same hardware that is described here to build your weather station, but if you choose different components, you will probably need to also find (or write) a Python library that works with them.

The specific sensors and components here were chosen after considering a number of factors:
- Availability
- Cost
- Linux/Python support
- Reliability
- Accuracy
- Ease of use

This does not mean that the components chosen are the cheapest, most accurate, and easiest to use. Rather they are balanced for all these factors. For example, in some cases accuracy has been sacrificed in favour of ease of use.

When selecting the components for your weather station, you should make choices based on what is most important for your particular project. We always like to hear about alternative builds, so please post your designs in the [Weather station forum](https://www.raspberrypi.org/forums/viewforum.php?f=112&sid=fd0218c9a5c6ff4445eb618f3b0a6eca){:target="_blank"}.

### Hardware

+ A Raspberry Pi, either one that has built-in wireless connectivity or has a a WiFi dongle
+ A BME280 pressure, temperature, and humidity sensor
+ A DS18B20 digital thermal probe (with 1m lead)
+ Two 4.7 KOhm resistors
+ Some 5mm-pitch PCB mount screw terminal blocks
+ A breadboard, some jumper wires
+ [An anemometer, wind vane, and rain gauge](https://www.argentdata.com/catalog/product_info.php?products_id=145){:target="_blank"}
+ Two RJ11 breakout boards (optional)
+ A MCP3008 analogue-to-digital convertor integrated circuit
+ Weatherproof enclosures; recommended products are this [75x75x37mm](http://cpc.farnell.com/spelsberg/332-907/universal-junc-box-7-entry/dp/EN81013){:target="_blank"} box for the BME280 and this larger [150x110x70mm](http://cpc.farnell.com/olan/ol20112/box-ip55-glanded-150x110x70mm/dp/EN82191){:target="_blank"} box for the Pi and a soldered HAT; if you're sticking with a less durable breadboard-only solution, then you may need a larger enclosure such as this [190x140x70mm one](http://cpc.farnell.com/olan/ol20013/box-ip55-glanded-190x140x70mm/dp/EN82192){:target="_blank"}


### Software

+ The Oracle Raspberry Pi Weather Station software. You don't need to install it, but you'll use some of the Python programs. Clone the GitHub repository by opening a Terminal window and typing:
```bash
git clone https://github.com/RaspberryPiFoundation/weather-station
```

+ The BME280 Python library:
```bash
sudo pip3 install RPi.bme280
```
+ The MariaDB database server software:
```bash
sudo apt-get install -y mariadb-server mariadb-client libmariadbclient-dev
sudo pip3 install mysqlclient
```

### Additional resources

If you are going to construct a permanent Weather HAT for your Pi, you may also need:
+ A soldering iron, solder, and safety equipment
+ Solid core wire (22 AWG)
+ An [Adafruit Perma-Proto HAT for Pi Mini Kit](https://www.adafruit.com/product/2310){:target="_blank"}
+ A 16-pin DIL/DIP IC Socket
+ Two 2-pin male headers
+ General prototyping tools: side-cutters, wire strippers. screwdrivers, etc.
+ Insulating tape
+ Access to a 3D printer or 3D printing service for these parts: [a mount to secure the Raspberry Pi inside the larger box](resources/BYOWS-bracket.stl){:target="_blank"}. and a [bracket to hold BME280 sensor into the smaller one](resources/bme280holder.stl){:target="_blank"}.
