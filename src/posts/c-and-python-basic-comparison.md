---
title: C and Python Basic Comparison
description: A basic comparison in calculation speed for C and Python language.
author: syncster
date: 2023-03-23T16:48:08.363Z
tags:
  - programming
  - comparison
---

Hello everyone and welcome to my next article of this journey!

To get more satisfaction and motivation in learning C, I wanted to know if what other people and the books says is true,
that C is really a fast language in terms of performace. So here I am.

In my previous post, I wrote a code for solving the water depth on a rectangular open channel to show the basic
concepts of the language. To get a benchmark for these two languages, I used that code and then convert it to python to get
a comparison. The problem is when I ran the code in C and looked at the calculation time in milliseconds. In python, I get something
but in C, I get zero. This is already a hint how fast C is but to make sure and see how C does, I tried adjusting the parameters. To elevate and simulate a longer response, I used large input values for discharge and smaller increment value. This I think should significantly lengthen the time of the calculation by more the doubled.

Here is the code for C:

```c
#include <stdio.h>
#include <math.h>
#include <sys/time.h>

int main()
{
    float water_depth;           // Water depth in meters
    float n_manning = 0.015;     // Manning's roughness coefficient
    float base_width = 10;       // Channel base width in meters
    float channel_slope = 0.001; // Channel bed slope on a reach
    float discharge = 15;        // Channel flow in cubic meters per second

    float trial_discharge = 0;       // Used for trial and error calculation to compare with the discharge input
    const float increment = 0.00001; // Increment for the trial of water depth each loop
    water_depth = 0;                 // Reset to zero

    float w_perimeter; // Calculated wetted perimeter
    float f_area;      // Calculated flow area
    float h_radius;    // Hydraulic radius
    float a_velocity;  // Average velocity

    struct timeval start_time, end_time;
    long long milliseconds;

    gettimeofday(&start_time, NULL);

    while (trial_discharge < discharge)
    {
        w_perimeter = base_width + (2 * water_depth);
        f_area = base_width * water_depth;
        h_radius = f_area / w_perimeter;
        a_velocity = (1 / n_manning) * powf(h_radius, (2.0 / 3.0)) * sqrt(channel_slope);
        trial_discharge = a_velocity * f_area;

        water_depth += increment;
    }

    gettimeofday(&end_time, NULL);

    // Calculate the difference in milliseconds
    milliseconds = (end_time.tv_sec - start_time.tv_sec) * 1000LL +
                   (end_time.tv_usec - start_time.tv_usec) / 1000LL;

    printf("Calculation using C:\n");
    // Display the result
    printf("Water depth of the channel is %.3f m.\n", water_depth);

    // Display time of calculation in milliseconds
    printf("Time of calculation in milliseconds: %lld\n", milliseconds);
    printf("==========\n");

    return 0;
}
```

and for python

```python
import datetime

discharge = 15.0
channel_slope = 0.001
n_manning = 0.015
base_width = 10.0

water_depth = 0.0
trial_discharge = 0.0

timestamp = datetime.datetime.now()

while trial_discharge < discharge:
    p = base_width + 2 * water_depth
    a = base_width * water_depth
    r = a / p
    v = (1 / n_manning) * pow(r, (2.0/3.0)) * pow(channel_slope, 0.5)
    trial_discharge = v * a
    water_depth += 0.00001

timestamp2 = datetime.datetime.now()
delta = timestamp2 - timestamp
diff = delta.total_seconds() * 1000

print("Calculation using python:")
print("Water depth:", round(water_depth, 3))
print("Time in milliseconds:", diff)
```

Running this multiple times gives me the same result. The compiled program written in C is much faster than the one from python.

![c-python](https://user-images.githubusercontent.com/19258246/227296560-eeb22b57-d3ca-45b8-a519-d2cd93a7c758.png)

A﻿s we can see above, the program written in C which is the `flow_c.app` is roughly around 10x faster than the one written in Python in the file `flow_python.py`.

## Takeaways

T﻿his is just one performance comparison between Python and C and sure there will be more in the future. As of this simple example, C has already proven how fast it is in this particular problem and I will explore more aspects as necessary in the future.

Additionally in the code above, it demonstrated the use of a library `time` and how to get the time it takes for a calculation by getting the current time of the computer before and after the calculation.

Thank you again for staying with me in this post, see you next time!
