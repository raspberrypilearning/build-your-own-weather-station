## What you will need

There are many different sensors available that you could use to make weather measurements. You don't have to use the exact same hardware to build your weather station, however if you choose different components you will need to also find (or write) a Python library that works with it.

The specific sensors here are chosen after considering a number of factors:
- Availability
- Cost
- Linux/Python support
- Reliability
- Accuracy

### Hardware

+ A Raspberry Pi.
+ A BME280 pressure, temperature and humidity sensor.
+ A DS18B20 digital thermal probe (with 1m lead)
+ Two 4.7 K Ohm resistors.
+ Some 5mm pitch PCB mount screw terminal blocks
+ A breadboard and jumper wires
+ [An anemometer, wind vane and rain gauge](https://www.argentdata.com/catalog/product_info.php?products_id=145){:target="_blank"}
+ An RJ11 breakout board (optional)
+ An MCP3008 Analogue to digital Convertor Integrated Circuit.

### Software

+ The Oracle Raspberry Pi Weather Station Software. Install this by opening a Terminal window and typing:
```bash
git clone https://github.com/RaspberryPiFoundation/weather-station
```

+ The BME280 Python library:
```bash
sudo pip3 install RPi.bme280
```

### Additional Resources

+ List additional resources, or delete section.
