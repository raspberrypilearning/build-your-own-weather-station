## What you will need

There are many different sensors available that you could use to make weather measurements. You don't have to use the exact same hardware to build your weather station, however if you choose different components you will need to also find the correct Python library to use with it.

The specific sensors here are chosen after considering a number of factors:
- Availability
- Cost
- Linux/Python support
- Reliability
- Accuracy

### Hardware

+ A Raspberry Pi.
+ A DHT22 or DHT11 temperature-humidity sensor.
+ A 4.7 K Ohm resistor.
+ A breadboard and jumper wires

### Software

+ Adafruit DHT11/22 Python library

``bash
git clone https://github.com/adafruit/Adafruit_Python_DHT.github
cd Adafruit_Python_DHT
python3 setup.py install
```

+ List software here, or delete section.

### Additional Resources

+ List additional resources, or delete section.
