## Assembling everything ready for outdoors
You should now have working weather station prototype on breadboard. If you are happy keeping your weather station in this form then you skip ahead to the *Keeping your weather station dry* section.


For a more robust, long term installation, or if you don't have room for a breadboard in your enclosure, you can construct a weather station HAT for your Pi. This will involve some soldering, but don't worry if you've never soldered before - there is a [great blog post and movie](https://www.raspberrypi.org/blog/getting-started-soldering/) to get you up to speed.

As usual, there is more than one way to achieve this. You could design a layout for stripboard 9also known as veroboard)

![](https://upload.wikimedia.org/wikipedia/commons/5/50/VEROBOARD_sample.jpg)

Soldering stripboard connections can be trickier than the 'through-hole' type you may be familiar with from assembling other digital Making kits. However prototyping HATs for Raspberry Pi are also available and these have Plated Through Holes (PTH) connections that are much easier tow work with.

The circuit diagram below shows a possible design for a weather station HAT using the Adafruit Perma-Proto HAT kit.

![](images/final_circuit_strip_bb.png)

###Things to note about this diagram

Note that to avoid cluttering the view, in this circuit diagram the 6 pins for each of the two RJ11 breakout boards are shown as female headers.

Interpreting this diagram requires s slightly different approach to building a breadboard circuit. Because the PTH connections go all the way through the board, wires and components can actually (and usefully) connected on either side.

![](images/weatherHAT_combi.png)

In the photo above, you can see that two 2-pin male connectors have been used for the connections for the BME280 sensor. As this sensor should be housed in a separate enclosure, this method makes assembly easier. However you could solder the wires connecting the sensor directly to the hat (after threading them through the water-tight glands or grommets used).

## Assembly

You are recommended to take things one step at a time, testing each connection to a weather sensor once you've added it to the board.

- First of all, solder the 40 pin header onto the Adafruit board.
- Solder on two 2-pin male headers, one across the SCL and SDA connections in the top left, and one across the +3v and GND rails.

![](images/ada_1.png)

- Connect the BME280 to these pins and place the HAT on the Pi.
- Boot the Pi and test that the BME280 works using the `bme280_sensor.py` code that you wrote earlier.

![](images/ada_2.png)

Next, add connections for the  DS18B20 probe. You can be sneaky and make use of unused screw terminals on one of the RJ11 breakout boards: the rainfall gauge only uses the two centre pins of the connector so the 2 outer on either side are free.

- Solder a 4.7K resistor in the bottom area as shown. Your RJ11 breakout board will need to sit just above this so try to seat the resistor so that it is flat against the top of the Adafruit board and not poking up in the end.

![](images/ada_3.png)

- Now add two connections to the bottom Ground rail using small lengths of wire.

![](images/ada_4.png)

- Then add longer wires to connect the GPIO pin breakout connections (pins 6 and 4) and the 3V rail. Once again, try to keep these as low as possible where the RJ11 breakout board will sit.  As mentioned earlier, you can solder the wires through from the bottom of the HAT rather than across the top. As long as the correct holes are connected together, it doesn't matter which side of the HAT is used. The connection to 3V will pass through a 'busy' part of the board if it goes over the top so this is a good choice to connect on the rear.

![](images/ada_5.png)

The connection to 3V will pass through a 'busy' part of the board if it goes over the top so this is a good choice to connect on the rear.

![](images/BYO_HAT_back.JPG)

- Now prepare RJ11 breakout board. You may have to solder the male pins onto the breakout board first. Make sure the shortest end of the pin is the part that you solder on. the longer end is the part that you'll solder onto the Adafruit board.

- Some of the pre-soldered parts of these breakout boards can be quite spiky. To avoid these peaks of solder from causing shorts when it is placed onto the Adafruit board, carefully trim them with side cutters.  It is also a good idea to then cover them with a small strip of insulating tape.

## Keeping your weather station dry

This is really important. If the Pi or any of the electronics gets wet or even very damp, they will fail or start to corrode. The Oracle Weather Station uses a small weatherproof enclosure to house the external environmental sensors. The key idea is to allow outside air to flow around the sensors but to prevent moisture from reaching them
