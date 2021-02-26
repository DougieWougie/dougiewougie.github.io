---
layout: post
author: Dougie
category: programming
---

Pimoroni’s Rainbow Hat offers a nice selection of inputs and outputs using a variety of protocols. This makes it a great way to experiment with Raspberry Pi, especially as Hardware Attached on Top (HAT) avoids the messiness of breadboards and shorting links!
<!-- more -->
Designed for Android Things, it also has a Python library and a well written getting started guide. I haven’t had a play with Android Things yet so will leave that for another day and am currently a little obsessed with Python anyway.
Installation

Attaching directly to the Pi using the GPIO pins, it’s very straight forward to install (I’m using a Raspberry Pi B+ and Raspbian Stretch). There’s a nice installation guide but it’s just a single script:

```
curl https://get.pimoroni.com/rainbowhat | bash
```

Can’t really see anyway that Pimoroni could make it easier. If you’re wondering about it’s suitability for younger explorers I’d say you’d be fine.

## What and how with Python

The Python library is well documented, although not completely (notably the “star” segmented display). So what have we got to play with?
### LED

LED are great so that’s where we start. I found a blog post from a chap called Tim which has a great deal of detail on the AP102 LED used but beware it’s a right rabbit hole (which I spent some time wandering around). These are controlled using the Serial Peripheral Interface (SPI). Documentation suggests the brightness can be adjusted but I couldn’t see it working.

I ended up spending more time messing around with different ways to use the LED that I used it’s own class but most of the methods look something like this:

```python
from rainbowhat import rainbow
from random import randint

for each in range(255):
    rainbow.clear()
    rainbow.set_all(randint(0, 6)), r, g, b)
    rainbow.show()
Segmented display
```

This updates very quickly, refreshing quickly enough to scroll. As mentioned above the library documentation omits display.

```python
import rainbowhat as rh

def scroll(scroll_text):
    while True:
        show = ''
        for letter in scroll_text:
            show = show + letter
            rh.display.clear()
            rh.display.print_str(show)
            rh.display.show()
            time.sleep(0.25)
            time.sleep(2)

scroll('Merry Christmas!')
```

### Temperature and pressure sensor

This is a single sensor that measures both. I haven’t played much with it but it seems about right. The temperature probably needs to be compensated for against the Pi’s temperature as it seems a little higher than I’d expect for room temperature. The functions are accessed using weather.temperature() and weather.pressure().

There’s also an altitude function (which is derived from pressure) weather.altitude(qnh=1020). I notice the parameters are specified as a keyword argument, I need to look at the library and see if I can use QNE as well as QNH.
Capacitive buttons

There’s three capacitive buttons, which are more responsive than I expected. These are accessed using a decorator (more detailed post here) and documentation mentions press and release states but I found there is also a pressed state (as in currently being pressed). I haven’t found if it’s possible to check if two or more a currently pressed and will look at that in another post.

```python
@rh.touch.A.press()
def touch_a(channel):
    # Whatever you want it to do!
```

I found I wanted an event handler running as a parallel process to monitor the buttons. Concurrency in Python is interesting and I am writing a separate post about it.

Each has a useful corresponding LED so you can show state. These are red, green and blue and are accessed as such, for example to turn on the blue one rainbowhat.light.blue.on().
Piezo buzzer

The buzzer can play midi notes by number or specific frequencies using buzzer.midi_note(number, duration=1.0) and buzzer.note(frequency, duration=1.0). I can’t imagine me using this much as I’m tone deaf so the most important method for me would be buzzer.stop.

## Thoughts

I certainly recommend this, especially if you’re getting into Python, Raspberry Pi and working with hardware.

HAT are a lot simpler and tidier than breadboards while still giving visual feedback. There is a good choice inputs and outputs here and the library is consistent and logical. They say that if something is Pythonic, you should be able to work out how it functions and that’s true here.
