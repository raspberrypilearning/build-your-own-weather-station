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

- Now go to your `calculate_speed` function and add these two lines before the final `return` line:

```python
final_speed = km_per_hour * ADJUSTMENT
store_speeds.append(final_speed)
```
