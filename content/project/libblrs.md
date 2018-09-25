---
title: "libblrs"
desc: "Helpful utilities for making the most of PROS"
img: "/images/libblrs.png"
img_desc: "libBLRS logo"
order: 0
---

## Overview
libblrs exists as a set of utilities to help make teams' robot code more consistent and reliable from year to year. The utilities were created with a lot of testing across a number of different robots and VEX games, and can be treated as "black box code" by everyone except the most advanced users. libblrs is split into four sub-libraries:

## libbtns: Buttons library
This library makes it easier to interact with the VEX joystick and the buttons on the external LCD.

## libfbc: Feedback controller library
This library contains abstracted feedback controllers, making it easier to employ PID, TBH, and other control algorithms in user code.

## liblcd: LCD script selection library
This library allows users to define a set of autonomous scripts (and accompanying titles) that can be selected from prior to a match using an external LCD.

## libmtrmgr: Motor manager library
This library allows users to easily integrate slewing, inversion, and scaling with motor output. In many cases, slewing and scaling can improve motor response to feedback control and reduce the likelihood of stalling.

## Open source
The source code for libblrs is publicly available and free for anyone to use with their own VEX robot code. To learn more, check out the [source code repository on GitHub](https://github.com/purduesigbots/libblrs).
