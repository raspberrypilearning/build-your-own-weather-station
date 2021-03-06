## Wind gusts

Weather reports and forecasts will normally report the wind speed along with wind gust information. A wind gust is a brief increase in wind speed that can occur whenever the wind is blowing. Gusts are more noticeable as the wind speed increases. This is because the force exerted by the wind increases rapidly as the wind speed increases.

Gusts normally occur because the air is not able to move along the ground at a constant speed. Obstacles such as vegetation, buildings, and elevation changes causes surface friction, which will slow the wind down in some places more than others. Air closer to the ground suffers from this phenomenon more than air higher up. This creates a more turbulent wind flow along the ground, which leads to gusts. A typical wind gust lasts less than 20 seconds.

### Storing wind readings

When your weather station is fully operational, you can record the maximum wind speed during a given period (the gust) as well as the average speed. You can do this by constantly taking wind speed measurements for five seconds, and temporarily storing them to be processed every few minutes. To do this, we will use a Python data structure called a **list**.

- Open IDLE, and open the file `/home/pi/weather-station/wind.py` file that you created in the last step.

- Add a line at the very top to import the `statistics` library.

```python
import statistics
```

- Then add this line, which creates an empty list called `store_speeds`, below the `import` lines:

```python
store_speeds = []
```

- Now modify the `while True` loop so that it contains a sub-loop that continually takes wind speed readings and adds them to this list. You can then use `statistics.mean` to calculate the mean value of readings in the `store_speeds` list. 

```python
while True:
    start_time = time.time()
    while time.time() - start_time <= wind_interval:
        reset_wind()
        time.sleep(wind_interval)
        final_speed = calculate_speed(wind_interval)
        store_speeds.append(final_speed)

    wind_gust = max(store_speeds)
    wind_speed = statistics.mean(store_speeds)
    print(wind_speed, wind_gust)

```

Notice that we're using `time.time()` to create a variable called `start_time` and then checking when the time has advanced by more than `wind_interval` seconds in the inner `while` loop.

- Run you code. Blow on the anemometer or spin it by hand and watch the readings that are produced.

![](images/gust_test.png)

When you stop spinning, you should see that the second reading remains the same (as this is the peak gust that has been produced), while the average speed falls off over time as the anemometer slows down.
