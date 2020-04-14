---
layout: post
title: In need for some tacos
summary: Mapping contemporary stalagmites
poster-image: Waste_Objects-poster.jpg
published: true
---
A collaboration with [Lisa Wilkens](http://www.lisawilkens.com/), who will work with drawings and [Emi Kodama](http://emikodama.com/), who wrote and narrated a story.

One of the 3D printers at Formlab has a drawer on the bottom of the machine that collects waste
material. The waste material solidifies while new material keeps dripping down. Small 3D prints make
a little pool of waste material appear in the tray. Medium prints create small pointy mounds and large
prints fill one side of the tray to the brim. I wasn't informed by the 3D printer company that these
objects could form and was surprised when I opened the drawer after the first 3D print. These
unexpected byproducts have both a natural and digital feel to them since they visually refer to both
ancient times and contemporary state-of-the-art technology. They look like stalagmites or cooled down
lava and at the same time bear the traces of the high tech machine that made them. I’m fascinated
that these objects have this ambiguity in them. It makes me think of the oppositions: creation and
waste, intention and accident, precision and carelessness, being visible and invisible. It's an accidental
object. It’s unwanted but not rejected. I imagine it to be like a shadow of the 3D printed object.

![](/images/waste-objects-04.jpg)
![](/images/waste-objects-05.jpg)


Work in progress-images:

![](/images/waste-objects-01.jpg)
![](/images/waste-objects-02.jpg)
![](/images/waste-objects-03.jpg)
 
 
 
 
 
 
### Scanning the objects

![](/images/waste-objects-shape-back.JPG)

Let's take one of the objects to show the scanning process.

![](/images/waste-objects-scan_result_bad.jpg)

The wax like object is quite hard to make a 3D scan of. The scanner is light based and the object disperses the light under the surface, confusing the software. The result of the scan is low on detail and due to the uncertainty of the measurements, there are many holes.

![](/images/waste-objects-Ardrox-9D1B.JPG)

Using a developer spray like Ardrox 9D1B, the object gets a light coating of fine white powder.

![](/images/waste-objects-shape-white-back.JPG)

This coating makes it clearer for the scanner to see the surface.

![](/images/waste-objects-scan-result-better.jpg)

A scan of the coated object results in a more detailed and continuous 3D model as a result.

![](/images/waste-objects-scanning-2.JPG)

All sides of the object are scanned

![](/images/waste-objects-stitching-scans.jpg)

By aligning the meshes, multiple scans are stitched together.

![](/images/waste-objects-propping-up-the-shape.JPG)

The object is propped up to expose otherwise hard to reach corners

![](/images/waste-objects-hole-filling.jpg)

The last step is to fill remaining holes. This results in a watertight mesh.


### Baking the detail to a normal map

### Syncrhonizing events to a video
For a follow up version of this project I want to fire events at predetermined moments in a video. In the video, the 3D scanned wax objects are recorded by virtual cameras. To tie the digital and physical versions of the objects together, LED lights will illuminate the physical objects at the same time and position of the digital camera's. This way the ambiguity of the objects is doubled in the presentation of the video installation. 

This is a technical summary of the test setup demonstrating how to execute events syncrhonized to a video. A Raspberry pi plays a video and sends out the playback-position to an Arduino. The Arduino executes events based on pre specified timestamps. The idea is based on [this forum post](https://stackoverflow.com/a/46834834): OMXPlayer is a command line video player that is built into Raspberry pi. We only need omxplayer-wrapper to control the player though a Python script.

* Components: 
  * Raspberry Pi 4 (2Gb ram version)
  * Arduino Due
* Raspberry pi needs an operating system. I'm using Raspbian 3.3.1 (named 'Buster'), and I installed it on the micro SD card with the [Raspberry Pi Imager](https://www.raspberrypi.org/downloads/). This is an installer that will format the SD card and use a Noobs (**n**ew **o**ut **o**f the **b**ox **s**oftware) zip file to install the operating system.
* Before installing omxplayer-wrapper, you will need to install some other software packages that omxplayer-wrapper needs. Open the terminal on the raspberry pi and copy-paste the line under [OS pre-requisite installation](https://python-omxplayer-wrapper.readthedocs.io/en/latest/#installation). I had an error executing this: “E: unable to locate package libdbus-1”. Based on [this](https://github.com/willprice/python-omxplayer-wrapper/issues/168) issue report, it was suggested to try this line: "sudo apt install -y libdbus-1-3 libdbus-1-dev".
* The next step is to [install](https://python-omxplayer-wrapper.readthedocs.io/en/latest/#installation) omxplayer-wrapper itself. After the install, the wrapper didn't work. I think it happened because the Python version in the terminal defaulted to Python 2 instead of 3. The Python editor (Thonny IDE) uses Python 3 by default, hence it couldn't find the wrapper. If you use **pip3** instead of **pip**, the wrapper installs in the Python 3 environment, so it can be found by the script.
* The raspberry pi needs to have the video on it's system in order to display it. I used wetransfer to send it to the raspberry pi.
* I made the following script, and saved it as a .py file on the Raspberry pi. In the Thonny IDE, I could press run in order to execute the script.

```python
#!/usr/bin/env python3

# play video and send the milliseconds over serial to Arduino
# based on: https://stackoverflow.com/questions/45532783/fire-events-at-specific-timestamps-during-video-playback 

from omxplayer import OMXPlayer
from pathlib import Path
from time import sleep
import serial

# setup the serial connection
# open terminal and type: "ls /dev/tty*" to find the port name
port = "/dev/ttyACM0" # this value can change every time you reconnect the arduino
rate = 57600 # baud rate

ser = serial.Serial(port,rate)
ser.flushInput()

VIDEO_PATH = Path("tacos.mp4") # pointing to a test-video
player = OMXPlayer(VIDEO_PATH, args=['--no-osd', '--blank']) #'--loop', # for testing '--loop' has been left out
player.pause()
sleep(3)
player.play()

# Make a query to position() inside infinite loop :
while (1):
    position = player.position() * 1000
    print('%02d' % position) # format as ints and print. This is for debugging
    
    # send the position to the arduino
    position_encoded = b'%d\n' %position # encode int to bytes + add a newline character
    ser.write(position_encoded)
    
    if(position >= 133000): #stop at 2 min and 13 seconds. This is the length of the test-video.
        player.quit()
player.quit()
```

* connect the two microcontrollers with a USB cable. On the raspberry pi, any usb port works. On the Arduino Due, you'll need to connect to the programming port. That is the usb port closest to the power input barrel jack. The Arduino will be powered over USB by the raspberry pi.
* open the video you want to synchronise, find the frames that you're interesting in (in this project's case: all the first frames after a cut in the video) and convert them to milliseconds: in the case of a 25fps movie: (frame * 25) * 1000. Use these values in the array array *positions[]* in the following code block.
* Upload the following script to the Arduino Due. It receives the time in milliseconds from the Raspberry pi and executes code based on the predetermined times in the array. **Press the erase button on the Arduino 3 seconds prior to uploading the code.** You will need to do this every time you upload new code.

```C++
/*
Raspberry pi streams the current position of the video playhead in milliseconds.
Based on predetermined time values, code can be executed in sync with the video.
It is not a perfect sync, but I expect the error to be smaller than a single frame (40 milliseconds in the case of 25fps).
In this example, the built-in LED changes state every time there's a cut in the video.
*/

// Variables for communication
const byte numChars = 32; // max chars to be received
char receivedChars[numChars]; // an array to store the received data
boolean newData = false;
int dataNumber = 0; // chars converted to int

int positions[] = {1560, 43360, 55280, 75320, 80120, 95040, 121640}; // predetermined time-positions in milliseconds
int shot = 0; // use to execute each codeblock only once

void setup() {
  Serial.begin(57600);
  pinMode(13, OUTPUT);
  LED(0);
  delay(2);
}

void loop() {
  recvWithEndMarker();
  convertData();
  syncActions();
}

void recvWithEndMarker() {
  static byte ndx = 0;
  char endMarker = '\n';
  char rc;

  if (Serial.available() > 0) {
    rc = Serial.read();

    if (rc != endMarker) {
      receivedChars[ndx] = rc;
      ndx++;
      if (ndx >= numChars) {
        ndx = numChars - 1;
      }
    }
    else {
      receivedChars[ndx] = '\0'; // terminate the string
      ndx = 0;
      newData = true;
    }
  }
}

void convertData() {
  if (newData == true) {
    dataNumber = 0;
    dataNumber = atoi(receivedChars);   // convert chars into int
    if (dataNumber == 3003) {
      flash(3);
    }
    newData = false;
  }
}

void flash(int n) {
  for (int i = 0; i < n; i++) {
    digitalWrite(13, HIGH);
    delay(30);
    digitalWrite(13, LOW);
    delay(80);
  }
}

void LED(byte n) {
  if (n == 1)
    digitalWrite(13, HIGH);
  else
    digitalWrite(13, LOW);
}

void syncActions () {
  if ((dataNumber > positions[0]) && (shot == 0)) {
    LED(1);
    shot++;
  }
  else if (dataNumber > positions[1]) && (shot == 1)) {
    LED(0);
    shot++;
  }
  else if (dataNumber > (positions[2]) && (shot == 2)) {
    LED(1);
    shot++;
  }
  else if (dataNumber > (positions[3]) && (shot == 3)) {
    LED(0);
    shot++;
  }
  else if (dataNumber > (positions[4]) && (shot == 4)) {
    LED(1);
    shot++;
  }
  else if (dataNumber > (positions[5]) && (shot == 5)) {
    LED(0);
    shot++;
  }
  else if (dataNumber > (positions[6]) && (shot == 6)) {
    LED(1);
    shot++;
  }
}
```

#### Helpful references:
omxplayer-wrapped commands & info
* options: https://github.com/popcornmix/omxplayer#synopsis
* api docs: https://python-omxplayer-wrapper.readthedocs.io/en/latest/omxplayer/

Serial communication
* https://forum.arduino.cc/index.php?topic=396450.0
* https://roboticsbackend.com/raspberry-pi-arduino-serial-communication/
* https://learn.sparkfun.com/tutorials/serial-communication/all
