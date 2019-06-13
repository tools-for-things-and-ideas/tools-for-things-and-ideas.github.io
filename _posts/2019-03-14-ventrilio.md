---
layout: post
title: Ventrilio
summary: Appropriating a form of critical<br> and robotic AI ventriloquism.
poster-image: ventrilio-poster.png
published: true
---
VENTRILIO: The Smart Turk <br>
by Jerry Galle & Boris Debackere<br>

Those who talk should do and only those who do should talk.<br>
Scars signal skin in the game. <br>
― Nassim Nicholas Taleb, Skin in the Game: The Hidden Asymmetries in Daily Life

![](/images/ventrilio01.jpeg)

VENTRILIO is an emotionally deprived AI on a quest for love. While the question “what is
love” percolates through the machine, it becomes obvious that the answer to the question is
as much desired as the object of the quest.<br>
As a sounding board on the quest for love, VENTRILIO appropriates a form of critical
ventriloquism and flirts with the unsettling —uncanny valley— feeling by getting acquainted
with an anthropomorphic doll. VENTRILIO performs the age old act of ventriloquism with a
twist. Namely, the figure vents the voice of the AI while being controlled by a robot arm.
VENTRILIO, the machine, learns by scraping sites of the web where humans leave traces of
their deepest desires: dating apps, social media, Tinder and comments on pornsites, ...<br>

VENTRILIO is an installation consisting of a robot arm, a doll, a Raspberry Pi and a
loudspeaker. The doll is custom made with the use of 3D printing. The electronic setup is
hidden inside the dummy’s clothing. The audio is produced with a small inbuilt speaker
connected to a Raspberry Pi where the AI processes are generated. The data is gathered
from several api’s such as this [one.](https://github.com/jbrower95/Pornhub-Comment-Scraper)

![](/images/ventrilio03.png)

To move 'the smart Turk' around we will use the Dobot robot arm with a custom made mechanized extension to manipulate its mouth and eyes.<br> 
Possible libraries to work with to send coordinates to the robots are this [one](https://github.com/luismesas/pydobot) or this [one](https://github.com/WarrG3X/dobot-rl). <br>
The [Edge TPU devices](https://aiyprojects.withgoogle.com/edge-tpu) could serve as the brain for Ventrilio.

To start using this library, type in command line terminal: <br>
```python
pip install pydobot
```
Check for Dobot after connecting it to your computer in terminal:<br>
```python
python -m serial.tools.list_ports
```

Gain access to the port in terminal: <br>
```python
sudo chmod 666 /dev/ttyUSB0
```
Then run this example Python code to check if everything works. If you're working on a mac use mask for OSX as written below. For Linux, use port found with commands above.

```python

import time
from glob import glob

from pydobot import Dobot

available_ports = glob('/dev/cu*usb*')  # mask for OSX Dobot port
if len(available_ports) == 0:
    print('no port found for Dobot Magician')
    exit(1)

device = Dobot(port=available_ports[0])

time.sleep(0.5)
device.speed(100)
device.go(250.0, 0.0, 25.0)
device.speed(10)
device.go(250.0, 0.0, 0.0)
time.sleep(2)
device.close()

```

![](/images/ventrilio-dobot.jpg)

![](/images/ventrilioDummy.png)

This project is in the making.


![](/images/ventrilio-stitching-ear.jpg)

Fixing mesh errors around the ears

![](/images/ventrilio-inside-head.jpg)

The shape that will be cut out the head to make room for the chin joint

![](/images/ventrilio-head-in-head.jpg)

Ready to be cut out

![](/images/ventrilio-side-view.jpg)

Side view

![](/images/ventrilio-chin.jpg)

Chin shape

![](/images/ventrilio-back-view.jpg)

Looking into the head from the back

![](/images/ventrilio-servo-mount.jpg)

A close up on the servo mount

![](/images/ventrilio-render.jpg)

A mockup render









