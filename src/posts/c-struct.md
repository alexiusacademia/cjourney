---
title: C Struct
description: Show definition and usage of struct in C.
author: alex
date: 2023-04-01T05:37:24.287Z
tags:
  - programming
  - struct
  - clang
---
In this post, we will see the usage of structs in C. We will use the codes used in the `flow_c` repo <https://github.com/alexiusacademia/cflow-01/blob/main/flow_c.c>

So instead of just defining the flow and channel parameters of the channel, it will be grouped inside a struct like so:

```c
struct RectangularChannel
{
    float base_width;
    float water_depth;
    float discharge;
    float channel_slope;
    float n_manning;
};
```

and then on the core code inside the main function

```c
struct RectangularChannel rc;

    printf("Enter discharge (cms): ");
    scanf("%f", &rc.discharge);
    printf("Enter Manning\'s roughness coefficient: ");
    scanf("%f", &rc.n_manning);
    printf("Enter channel slope (m/m): ");
    scanf("%f", &rc.channel_slope);
    printf("Enter base width (m): ");
    scanf("%f", &rc.base_width);

    float trial_discharge = 0;       // Used for trial and error calculation to compare with the discharge input
    const float increment = 0.00001; // Increment for the trial of water depth each loop
    rc.water_depth = 0;              // Reset to zero

    float w_perimeter; // Calculated wetted perimeter
    float f_area;      // Calculated flow area
    float h_radius;    // Hydraulic radius
    float a_velocity;  // Average velocity

    long long milliseconds;

    while (trial_discharge < rc.discharge)
    {
        w_perimeter = rc.base_width + (2 * rc.water_depth);
        f_area = rc.base_width * rc.water_depth;
        h_radius = f_area / w_perimeter;
        a_velocity = (1 / rc.n_manning) * powf(h_radius, (2.0 / 3.0)) * sqrt(rc.channel_slope);
        trial_discharge = a_velocity * f_area;

        rc.water_depth += increment;
    }
```

For example, instead of using `discharge` variable, here it will be `rc.discharge`. It uses the dot notation to access the members of the struct.

Now this is the simplest usage of a struct in C. We will know furthermore when we are already using struct as parameter to a function how accessing its members will be.

The full code of this is 

```c
#include <stdio.h>
#include <math.h>

void welcome_message()
{
    printf("Welcome to CFlow, a program written in C to calculate\nwater depth on a rectangular channel section for open channel flow.\n\n");
}

struct RectangularChannel
{
    float base_width;
    float water_depth;
    float discharge;
    float channel_slope;
    float n_manning;
};

int main()
{
    struct RectangularChannel rc;

    printf("Enter discharge (cms): ");
    scanf("%f", &rc.discharge);
    printf("Enter Manning\'s roughness coefficient: ");
    scanf("%f", &rc.n_manning);
    printf("Enter channel slope (m/m): ");
    scanf("%f", &rc.channel_slope);
    printf("Enter base width (m): ");
    scanf("%f", &rc.base_width);

    float trial_discharge = 0;       // Used for trial and error calculation to compare with the discharge input
    const float increment = 0.00001; // Increment for the trial of water depth each loop
    rc.water_depth = 0;              // Reset to zero

    float w_perimeter; // Calculated wetted perimeter
    float f_area;      // Calculated flow area
    float h_radius;    // Hydraulic radius
    float a_velocity;  // Average velocity

    long long milliseconds;

    while (trial_discharge < rc.discharge)
    {
        w_perimeter = rc.base_width + (2 * rc.water_depth);
        f_area = rc.base_width * rc.water_depth;
        h_radius = f_area / w_perimeter;
        a_velocity = (1 / rc.n_manning) * powf(h_radius, (2.0 / 3.0)) * sqrt(rc.channel_slope);
        trial_discharge = a_velocity * f_area;

        rc.water_depth += increment;
    }

    // Display the result
    printf("Water depth of the channel is %.3f m.\n", rc.water_depth);

    return 0;
}
```

It has the same usage of the previous repo in the filename `flow_c.c`.

I hope this gives you some clear and simplified overview of struct type in C. Thank you for reading and see you on the next article!