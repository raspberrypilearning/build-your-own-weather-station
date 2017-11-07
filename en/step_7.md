## Wind gusts

Weather reports and forecasts will normally report the wind speed along with wind gust information.

A wind gust is a brief increase in wind speed that can occur whenever the wind is blowing. Gusts are more noticeable as the wind speed increases. This is because the force exerted by the wind increases rapidly as the wind speed increases.  Gusts normally occur because the air is not able to move along the ground at a constant speed. Obstacles such as  from vegetation, buildings and elevation changes causes surface friction  which will slow the wind down in some places more than others. Air closer to the ground is suffers from this phenomenon more b than air which is higher up. This creates a more turbulent wind flow along the ground which leads to gusts. A typical wind gust lasts less than 20 seconds.

A gust occurs within a given time period when:

the highest wind speed measured during that period is above 29.6km/h AND
the difference between the peak speed and lowest speed in that period is greater than 16.7km/h AND
the time period is 20 seconds or less

### Storing wind readings

You can modify the code your wrote in the previous step to also measure wind gusts. Since the time period we're interested in is 20 seconds and our existing program records wind speed every 5 seconds (this is the number of seconds stored in the interval variable in the program), we need to record the four most recent readings to cover the last 20 seconds. To do this we will use a Python data structure called a list.

- Open Idle and the open file your `/home/pi/wind.py` file that you created in the last step.

- Add this line, which creates an empty list, after the `import` lines at the top.

```python
store_speeds = []
```

- Now go to your `calculate_speed` function. The reading for the wind speed is the final line where we return km_per_hour * ADJUSTMENT. Returning a value immediately ends the function, but as you'll need  to add some other calculations you need to change this and add the reading to your `store_speeds` list. Add these two lines before the final `return` line:

```python
final_speed = km_per_hour * ADJUSTMENT
store_speeds.append(final_speed)
```

- You'll also want to be able to access the `store_speeds` list from within the `calculate_speed` function, so declare it as a global variable:

```python
global store_speeds
```

- You only want to store the last 4 measurements of wind speed to cover the previous 20 seconds, but if you carry on adding each new measurement to the list, you will soon have a very long list! To prevent this from happening, modify your `calculate_speed` function to include a check for how long the list is using the len() function.  If adding another reading will take the list over 4 items, chop off the oldest measurement.

---hints---
---hint---
We can use the slicing operator to remove the oldest - in this case the first - item in a list

```python
if len(store_speeds) > 4:
        store_speeds = store_speeds[1:]
```

---/hint---
---hint---
Your new `calculate_speed` function should look like this:
```python

def calc_speed(time_sec):
        global count
        global store_speeds
        circumference_cm = (2 * math.pi) * radius_cm        
        rotations = count / 2.0

        # Calculate distance travelled by a cup in km
        dist_km = (circumference_cm * rotations) / CM_IN_A_KM

        # Speed = distance / time
        km_per_sec = dist_km / time_sec
        km_per_hour = km_per_sec * SECS_IN_AN_HOUR

        # Calculate speed
        final_speed = km_per_hour * ADJUSTMENT

        # Add this speed to the list
        store_speeds.append(final_speed)

        # If that takes the list over 4 items, chop off the first
        if len(store_speeds) > 4:
                store_speeds = store_speeds[1:]

        # Show what is in the store_speeds list
        print( str(store_speeds) )

        return final_speed
```
---/hint---
---/hints---

### Checking for gusts

For a gust to have occurred, two conditions need to be true:

Condition 1 - Highest wind speed above 29.6km/h
Condition 2 - Difference between highest and lowest is above 16.7km/h

- Add a function called `check_for_gusts` to check whether these two conditions have been met for a set of 4 readings in the `store_speeds` list.

---hints---
---hint---

Inside this function, create variables to store the highest and lowest speeds in the store_speeds list. You can calculate these easily using the built-in Python functions min() and max().

---/hint---
---hint---
Now add constants to represent the values we are testing against:

GUST_ABOVE - a gust occurs when the wind speed is above 29.6km/h AND
GUST_RANGE - a gust occurs when the range is above 16.7km/h

Check the conditions and return either the gust speed or 0.
---/hint---
---hint---
Your new `check_for_gusts` function should look like this:
```python

def check_for_gusts():
        highest = max(store_speeds)
        lowest = min(store_speeds)
        GUST_ABOVE = 29.6       
        GUST_RANGE = 16.7
        if highest > GUST_ABOVE and highest - lowest > GUST_RANGE:
            return highest
        else:
            return 0    
```
---/hint---
---/hints---

- Finally, add a line to print the gust measurement.
