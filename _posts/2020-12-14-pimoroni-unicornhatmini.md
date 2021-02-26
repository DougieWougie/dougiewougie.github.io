---
layout: post
title: Pimoroni Unicorn Hat Mini
author: Dougie
category: raspi
tags: raspi electronics pimoroni
published: false
---
# What is it?
Its Hardware Attached on Top (HAT) - a device that plugs into the 40 pin GPIO on the Pi (in this case a Zero).

This one has a row of 17x7 RGB LED driven by 2 [Holtek HT16D35A](https://www.holtek.com/documents/10179/116711/HT16D35A_Bv120.pdf) LED driver chips as well as 4 buttons.

# Pinout
The pinout are [available](https://pinout.xyz/pinout/unicorn_hat_mini#). We're using SPI...

## Serial Peripheral Interface
One of a couple of synchronous communication protocols, that is it uses its own clock signal to synchronise the two chips talking to each other. With a common clock the peripheral knows when to sample data (datasheet will specify if this on the leading of lagging edge). The chip that sends the clock is called the controller, and those it communicates with the peripherals.

Two data lines are used - one for input and one for output referred to as Controller Out Peripheral In (COPI) and Controller In Peripheral Out (CIPO). A clock line, SCK, carries the timing signal and a fourth line, Chip Select (CS) allows multiple peripherals to be addressed by a single controller.

### Sending data
