---
layout: post
author: Dougie
category: raspi
published: false
---

I like Pimoroni's products, they're generally well made with reasonable documentation. The first run of their new [Grow](https://learn.pimoroni.com/tutorial/hel/assembling-grow) Hat was discounted because of a slight flaw - the screens don't dim.
<!-- more -->
The kit comes with three sensors using Pulse Frequency Modulation (PFM), a method to represent an analogue value as binary. Using a square waveform, the width and amplitude are kept constant but the *frequency* is varied. Here, the higher the frequency the *drier* the soil being measured. The diagram Pimoroni use on their tutorial is confusing as it looks like width is being varied rather than frequency[^1].

As the article says, you need to calibrate the sensors. Finding the values requires you to select the channel on the hat and then cycle through the options and read off the current frequency. I let mine get dry, read the values and then saturated them and re-read the new values. The sensors' values seem to be quite different so this step is important.

| Channel | 1 | 2 | 3 |
|--|--|--|--|
| Dry | 9.22 | 16.49 | 6.43 |
| Wet | 1.06 | 1.06 | 0.73 |

**Update: This has been running for a few weeks now and the results have been consistent.**

I didn't notice mention of this but there's a light sensor on the hat. Poking around the company's [Github](https://github.com/pimoroni/grow-python). In the words of Prof Denzel Dexter, results were dissapointing. It appears that the library doesn't support the light sensor yet but there is link to the sensor's [datasheet](http://optoelectronics.liteon.com/upload/download/ds86-2013-0003/ltr-559als-01_ds_v1.pdf).

Being as I am far, far too lazy to check the device daily (plus I'm forever away), the next step is to get it to send a message to Telegram. That's a subject for another post though...

---
[^1]: I emailed the author but never got an answer.
