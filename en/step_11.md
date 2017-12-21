You should now have working weather station prototype on breadboard. If you are happy keeping your weather station in this form then you skip ahead to the *Keeping your weather station dry* section.


For a more robust, long term installation, or if you don't have room for a breadboard in your enclosure, you can construct a weather station HAT for your Pi. This will involve some soldering, but don't worry if you've never soldered before - there is a [great blog post and movie](https://www.raspberrypi.org/blog/getting-started-soldering/){:target="_blank"} to get you up to speed.

As usual, there is more than one way to achieve this. You could design a layout for stripboard 9also known as veroboard)

![](https://upload.wikimedia.org/wikipedia/commons/5/50/VEROBOARD_sample.jpg)

Soldering stripboard connections can be trickier than the 'through-hole' type you may be familiar with from assembling other digital Making kits. However prototyping HATs for Raspberry Pi are also available and these have Plated Through Holes (PTH) connections that are much easier tow work with.

The circuit diagram below shows a possible design for a weather station HAT using the Adafruit Perma-Proto HAT kit.

![](images/final_circuit_strip_bb.png)

Note that to avoid cluttering the view, in this circuit diagram the 6 pins for each of the two RJ11 breakout boards are shown as female headers.

Interpreting this diagram requires s slightly different approach to building a breadboard circuit. Because the PTH connections go all the way through the board, wires and components can actually (and usefully) connected on either side.

![](images/weatherHAT_combi.png)

In the photo above, you can see that two 2-pin male connectors have been used for the connections for the BME280 sensor. As this sensor should be housed in a separate enclosure, this method makes assembly easier. However you could solder the wires connecting the sensor directly to the hat 9after threading them through the water-tight glands or grommets used
## Keeping your weather station dry

This is really important. If the Pi or any of the electronics gets wet or even very damp, they will fail or start to corrode. The Oracle Weather Station uses a small weatherproof enclosure to house the external environmental sensors. The key idea is to allow outside air to flow around the sensors but to prevent moisture from reaching them
