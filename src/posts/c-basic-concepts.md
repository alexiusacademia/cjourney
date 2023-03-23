---
title: C Basic Concepts
description: Practicing the basic concepts in C like variables, user input and
  output and the program control structure while loop
author: syncster
date: 2023-03-23T07:02:04.161Z
tags:
  - programming
  - c basic concepts
  - clang
  - while loop in c
---

## Concepts Review

In this entry, I will try to create a project-based approach on the concepts learned in the C language. Perhaps, not just for this entry but to most concept reviews in the future. I find this more motivational than just pure concepts and topics as this gives more satisfying results.

## Project to Create

I﻿n most of the language I study, I try to create a common program, just to compare how each language work. In this program, I tried various languages such as the following:

- Python
- G﻿olang
- D﻿lang
- S﻿wift

T﻿his program is for hydraulics engineering and specifically, open channel flow. It will calculate the depth of flow in a rectangular canal/channel.

H﻿ere is the code:

```
/**
 * Program to practice usage of:
 *  - user input/output
 *  - variables/constant, and
 *  - loop
 */
#include <stdio.h>
#include <math.h>

void welcome_message()
{
    printf("Welcome to CFlow, a program written in C to calculate\nwater depth on a rectangular channel section for open channel flow.\n\n");
}

int main()
{
    welcome_message();

    float water_depth;   // Water depth in meters
    float n_manning;     // Manning's roughness coefficient
    float base_width;    // Channel base width in meters
    float channel_slope; // Channel bed slope on a reach
    float discharge;     // Channel flow in cubic meters per second

    printf("Enter discharge (cms): ");
    scanf("%f", &discharge);
    printf("Enter Manning\'s roughness coefficient: ");
    scanf("%f", &n_manning);
    printf("Enter channel slope (m/m): ");
    scanf("%f", &channel_slope);
    printf("Enter base width (m): ");
    scanf("%f", &base_width);

    float trial_discharge = 0;      // Used for trial and error calculation to compare with the discharge input
    const float increment = 0.0001; // Increment for the trial of water depth each loop
    water_depth = 0;                // Reset to zero

    float w_perimeter; // Calculated wetted perimeter
    float f_area;      // Calculated flow area
    float h_radius;    // Hydraulic radius
    float a_velocity;  // Average velocity

    while (trial_discharge < discharge)
    {
        w_perimeter = base_width + (2 * water_depth);
        f_area = base_width * water_depth;
        h_radius = f_area / w_perimeter;
        a_velocity = (1 / n_manning) * powf(h_radius, (2.0 / 3.0)) * sqrt(channel_slope);
        trial_discharge = a_velocity * f_area;

        water_depth += increment;
    }

    // Display the result
    printf("Water depth of the channel is %.3f m.\n", water_depth);

    return 0;
}
```

The code is hosted in github at [https://github.com/alexiusacademia/cflow-01](https://github.com/alexiusacademia/cflow-01)

## C﻿onclusion

This program demonstrates the basic concepts of the C language. Comparing it to a python code with the same function, it's almost of the same length. This however will be shown in the next entry of this blog where I will try to compare the two language, python and C, in terms of speed and code.

Thank you for reading and hope to find you in the next entry of this series!
