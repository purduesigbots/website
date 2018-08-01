---
title: "R.A.D.I.U.S. Array"
desc: "Reflectance and Analog Data Interpretation Unified Sensor Array"
img: "/images/radius.jpg"
img_desc: "top view of the R.A.D.I.U.S. Array board"
order: 3
---

<iframe width="100%" height="461" src="https://www.youtube.com/embed/WLyXgygtGUg" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## Overview
The SIGBots R.A.D.I.U.S. Array is a sophisticated line tracking sensor with capabilities exceeding those of the VEX Line Tracker. By combining 32 sensors and on-board processing, the array enables fast and accurate line tracking in a variety of conditions.

## Features
The R.A.D.I.U.S. Array uses four sets of [QTR8A line tracking sensors](https://www.pololu.com/product/960) for a combined total of 32 sensors. Each sensor module of eight emitters is broken into six-sensor and two-sensor pieces and arranged in the form of a 6x6 square with the corners missing. This arrangement increases the total effective sensing area to a nearly 2.5" by 3.5" rectangle (in contrast with the tiny window provided by the VEX Line Tracker) and allows lines to be acquired at high speeds. In addition, the large sensing area allows the angle and position of the line to be estimated based on the particular pattern of active and inactive sensors.

The board includes a [3.3V voltage regulator](http://www.ti.com/product/lm2937) so the whole system can be connected to a power supply or a VEX Cortex Microntroller via a VEX PWM Cable. Data is returned to the VEX Cortex via an I2C connection, with a secondary I2C port that can be used to chain other devices, for example a gyroscope or a VEX Integrated Motor Encoder. [TVS diodes](http://www.vishay.com/docs/85809/gl05t.pdf) protect the I2C bus from electrostatic discharge. All the electrical engineering and firmware development for this board was done by members of Purdue SIGBots.

## Data Processing
Since no commonly available microcontrollers have 32 analog-to-digital conversion channels, the R.A.D.I.U.S Array makes use of external ADC chips. Each chip is a [TLV1453](http://www.ti.com/product/tlv1543) with 3.3V supply and eleven channels, controlled over SPI. A central micocontroller, the [ATmega328P](http://www.atmel.com/devices/atmega328p.aspx) (commonly used in the Arduino development board), is tasked with reading the large quantities of data from the sensors and reducing it to a few key criteria regarding the line's position, angle, and intersection.

Initially, the [least squares method](http://mathworld.wolfram.com/LeastSquaresFitting.html) was used with a weighted data array to determine the slope of the line currently in view. Sensors over the line with a correspondingly large signal would be incorporated heavily into the resulting regression, while sensors that detected the line weakly (or not at all) had little to no weight in the calculation. However, the linear least squares regression fails on lines that are nearly vertical, as the slope diverges to a singularity for a fully vertical line.

To rectify these shortcomings, the more complex [perpendicular least squares method](http://mathworld.wolfram.com/LeastSquaresFittingPerpendicularOffsets.html) was employed instead for the final revision. This method takes into account the perpendicular distance to the line, and therefore has no trouble dealing with vertical lines. Intersecting lines in the field of view were a another key test case&mdash; while detection was relatively easy, determining the intersection angle was comparatively difficult. Once the center of gravity was determined with a weighted average, however, the sensors could be split into quadrants to isolate the two lines of best fit.

## Drawbacks
- Emitters can use large amounts of power and flood the field with too much infrared light
- Variance from sensor to sensor is higher than with the VEX sensors
- Infrared filtering (in the sensors) is not as good as in the VEX sensors, but frequency filtering can be incorporated in software
