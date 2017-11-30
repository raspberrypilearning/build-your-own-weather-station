## Fully functional weather station

Now that you've tested all the sensors individually, it's time to set up the software so that you have a complete collection system.

The original Oracle Weather Station adopts a Unix daemon approach to running the software, and you can adapt that code to run your custom build. The GPIO connections you've been using so far match those expected by this software so a slightly modified version of the code will work, and you've already used the original Oracle Weather Station code for the DS18B20 digital thermal probe.

To complete your custom Weather Station, you can also adapt and amalgamate the code you've written for testing to to regularly measure and record

### Wind speed, gusts and direction

The code you wrote for wind speed and gust measurement will form the basis of your overall Weather Station software.

Take a copy of your `wind.py` and call it `weather_station_BYO.py` (you can can do this in Idle by opening `wind.py` and then using *Save As*).

- You will need to add some additional libraries, some of the Oracle Weather Station code along with some of the programs you've already written. the top of your file should contain the following:

```python
from gpiozero import Button
import time
import math
import bme280_sensor
import wind_direction_byo
import statistics
import ds18b20_therm
import database
```
As it currently stands, your code will continually record the wind speed every 5 seconds, keeping track of the largest measurement (gusts) and calculating the mean speed. You can extend this to also simultaneously measure wind direction.

- Modify your code so that instead of pausing for 5 seconds in each loop, the program takes 5 seconds worth of wind direction measurements.

---hints---
---hint---
You can use the same time.time() method to create a second sub-loop inside the first. Make sure you use a different variable name to store the starting time.
---/hint---
---hint---
You can also use a list to store the wind direction readings just as you did for the wind speeds.
```python
store_directions = []
```
---/hint---
---hint---
Your modified function could look like this. You can use the `get_average` function you wrote to calculate this value from the list of measurements.

```python
while True:
    start_time = time.time()
    while time.time() - start_time <= wind_interval:
        wind_start_time = time.time()
        reset_wind()
        #time.sleep(wind_interval)
        while time.time() - wind_start_time <= wind_interval:
                store_directions.append(wind_direction_byo2.get_value())

        final_speed = calculate_speed(wind_interval)
        store_speeds.append(final_speed)
    wind_average = wind_direction_byo2.get_average(store_directions)

    wind_gust = max(store_speeds)
    wind_speed = statistics.mean(store_speeds)
    print(wind_speed, wind_gust, wind_average)
```
---/hint---
---/hints---

- Test your code. Spin the anemometer and wind vane. Does the program produce sensible values.

- Currently your program is constantly updating the mean values and peak wind speed as new measurements are made. Your Weather Station should start afresh with each 5 seconds of measurement. Add two lines to your code to empty the lists that hold the wind speeds and directions after every pass through the loop.

---hints---
---hint---
You need to empty the `store_speeds` and `store_directions` lists.
---/hint---
---hint---
You can do this with the lines:
```python
store_speeds = []
store_directions =[]
```
---/hint---
---hint---
Your modified function could look like this.

```python
while True:
    start_time = time.time()
    while time.time() - start_time <= wind_interval:
        wind_start_time = time.time()
        reset_wind()
        #time.sleep(wind_interval)
        while time.time() - wind_start_time <= wind_interval:
                store_directions.append(wind_direction_byo2.get_value())

        final_speed = calculate_speed(wind_interval)
        store_speeds.append(final_speed)
    wind_average = wind_direction_byo2.get_average(store_directions)

    wind_gust = max(store_speeds)
    wind_speed = statistics.mean(store_speeds)
    print(wind_speed, wind_gust, wind_average)
    store_speeds = []
    store_directions =[]
```
---/hint---
---/hints---

- Test your code again. You should see that you are recording the angular position of the wind vane, and counting the rotations of the anemometer for 5 seconds. Your code then calculates the mean wind speed and average position of the vane for that period. You will have also noticed that the value for wind gust is now always the same as the mean, because you are emptying the list of speeds after every 5 second period - so there is only ever 1 value (the last one).

Every 5 seconds is a nice sampling speed, but is too frequent to be storing new measurements.  A better period of measurement would be every 5 *minutes*. You can then store 5 minutes worth of of speeds and then record the peak value (gust) from that collection of measurements. That is much more useful!

- Modify the code so that it calculates new mean speeds and directions and records the strongest gust every 5 minutes, with a sampling frequency of 5 seconds.

---hints---
---hint---
You should change the period of the outer-most timed loop to be 5 minutes.
---/hint---
---hint---
Create another variable called `interval` outside the main (`while True`) loop:
```python
interval = 300
```
5 x 60 seconds = 300
---/hint---
---hint---
Then use that as the timing comparison for the outer timed loop:

```python
while True:
    start_time = time.time()
    while time.time() - start_time <= interval:
        wind_start_time = time.time()
        reset_wind()
        #time.sleep(wind_interval)
        while time.time() - wind_start_time <= wind_interval:
                store_directions.append(wind_direction_byo2.get_value())

        final_speed = calculate_speed(wind_interval)
        store_speeds.append(final_speed)
    wind_average = wind_direction_byo2.get_average(store_directions)

    wind_gust = max(store_speeds)
    wind_speed = statistics.mean(store_speeds)
    print(wind_speed, wind_gust, wind_average)
    store_speeds = []
    store_directions =[]
```
---/hint---
---/hints---
- Test your code. It should now report readings every 5 minutes. Simulate some wind activity by rotating the vane and anemometer and check that your measurements are what you'd expect.

Now you can add the other sensors into this 5 minute loop.

## Temperature, Pressure and humidity

When you wrote the code for the BME280 pressure, temperature and humidity sensor, you created a `read_all` function to return all three measurements. You can call this function from within `weather_station_BYO.py` as you've included your `bme280_sensor` program as an imported library.

- Modify your code so that the readings from the BME280 are also recorded every 5 minutes.

---hints---
---hint---
You can call the `read_all` function that you wrote earlier.
---/hint---
---hint---
```python
humidity, pressure, ambient_temp = bme280_sensor.read_all()
```
---/hint---
---hint---
Your completed code should look  like this:

```python
while True:
    start_time = time.time()
    while time.time() - start_time <= interval:
        wind_start_time = time.time()
        reset_wind()
        #time.sleep(wind_interval)
        while time.time() - wind_start_time <= wind_interval:
                store_directions.append(wind_direction_byo2.get_value())

        final_speed = calculate_speed(wind_interval)
        store_speeds.append(final_speed)
    wind_average = wind_direction_byo2.get_average(store_directions)

    wind_gust = max(store_speeds)
    wind_speed = statistics.mean(store_speeds)
    humidity, pressure, ambient_temp = bme280_sensor.read_all()
    print(wind_speed, wind_gust, wind_average, humidity, pressure, ambient_temp)
    store_speeds = []
    store_directions =[]
```
---/hint---
---/hints---

- Test your code. Exhale onto the BME280 and check that the readings change appropriately.

- Now do the same thing for the ground temperature probe. Modify your code so that readings are collected every 5 minutes.

---hint---
You will need to initialise the sensor first:

```python
temp_probe = ds18b20_therm.DS18B20()
```
---/hint---
---hints---
---hint---
You can use the `read_temp()` function.
---/hint---

---hint---
Your completed code should look  like this:

```python
from gpiozero import Button
import time
import math
import bme280_sensor
import wind_direction_byo2
import statistics
import ds18b20_therm
import database

wind_count = 0       # Counts how many half-rotations
radius_cm = 9.0 # Radius of your anemometer
wind_interval = 5 # How often (secs) to sample speed
interval =  5 # measurements recorded every 5 minutes
CM_IN_A_KM = 100000.0
SECS_IN_AN_HOUR = 3600
ADJUSTMENT = 1.18
BUCKET_SIZE = 0.2794
rain_count = 0
gust = 0
store_speeds = []
store_directions = []


# Every half-rotation, add 1 to count
def spin():
	global wind_count
	wind_count = wind_count + 1
	#print( wind_count )

def calculate_speed(time_sec):
        global wind_count
        global gust
        circumference_cm = (2 * math.pi) * radius_cm
        rotations = wind_count / 2.0

        # Calculate distance travelled by a cup in km
        dist_km = (circumference_cm * rotations) / CM_IN_A_KM

        # Speed = distance / time
        km_per_sec = dist_km / time_sec
        km_per_hour = km_per_sec * SECS_IN_AN_HOUR

        # Calculate speed
        final_speed = km_per_hour * ADJUSTMENT

        return final_speed

def bucket_tipped():
    global rain_count
    rain_count = rain_count + 1
    #print (rain_count * BUCKET_SIZE)

def reset_rainfall():
    global rain_count
    rain_count = 0

def reset_wind():
    global wind_count
    wind_count = 0

def reset_gust():
    global gust
    gust = 0

wind_speed_sensor = Button(5)
wind_speed_sensor.when_activated = spin
temp_probe = ds18b20_therm.DS18B20()

while True:
    start_time = time.time()
    while time.time() - start_time <= interval:
        wind_start_time = time.time()
        reset_wind()
        #time.sleep(wind_interval)
        while time.time() - wind_start_time <= wind_interval:
                store_directions.append(wind_direction_byo2.get_value())

        final_speed = calculate_speed(wind_interval)# Add this speed to the list
        store_speeds.append(final_speed)
    wind_average = wind_direction_byo2.get_average(store_directions)

    wind_gust = max(store_speeds)
    wind_speed = statistics.mean(store_speeds)
    store_speeds = []
    #print(store_directions)
    store_directions = []
    ground_temp = temp_probe.read_temp()
    humidity, pressure, ambient_temp = bme280_sensor.read_all()

    print(wind_average, wind_speed, wind_gust, humidity, pressure, ambient_temp, ground_temp)


```
---/hint---
---/hints---

You should now have working weather station prototype on breadboard. This is perfect for testing but probably not suitable for long-term, reliable installation outside.

To modify this so that it will survive outdoors for a long period you will need to make more permanent connections. This will involve some soldering, but don't worry if you've never soldered before - there is a [great blog post and movie](https://www.raspberrypi.org/blog/getting-started-soldering/){:target="_blank"} to get you up to speed.

## Powering your Weather Station

POE
Normal Power supply

## Keeping your weather station dry

This is really important. If the Pi or any of the electronics gets wet or even very damp, they will fail or start to corrode. The Oracle Weather Station uses a small weatherproof enclosure to house the external environmental sensors. The key idea is to allow outside air to flow around the sensors but to prevent moisture from reaching them
