## Active mechanical sensors

So far all the sensors you've used have been passive electronic sensors that just sit there and make measurements of their surroundings. However to measure things like rainfall and wind speed/direction, you'll need to use active mechanical devices that interact physically with the environment.

The original Oracle Weather Station kit used popular [wind and rain sensors](https://www.argentdata.com/catalog/product_info.php?products_id=145){:target="_blank"} that are often used in consumer weather stations. These are the recommended sensors to use as they are robust and reliable. The [datasheet](https://www.argentdata.com/files/80422_datasheet.pdf){:target="_blank"} for these sensors gives more information about their size and construction.

### Connectors

These sensors usually come with RJ11 connectors (they look like a standard telephone jack) which are sturdy and are difficult to accidentally dislodge so your Weather Station will remain operational even in blustery conditions.

When it comes to connecting them to your Pi, you have three options:
- Chop off the male RJ11 connectors and connect the wires using screw terminals or by soldering.
- Use RJ11 breakout boards - these can be really helpful for prototyping but the larger ones can be too bulky for long term deployment.

![](images/RJ11_breakout_large.JPG)

Smaller ones often come with solderable pins that can be used with stripboard or a prototyping HAT to make a durable connection.

![](images/RJ11_breakout_small.JPG)

The assembly instructions later for creating a permanent hardware solution will use these smaller breakout boards.  
- Use female RJ11 connectors - these are quite fiddly to use with breadboards but can provide a very sturdy connection if used with a Printed Circuit Board (PCB) as part of a permanent Weather Station.
