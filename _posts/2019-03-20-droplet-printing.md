---
layout: post
title: Droplet Printing
summary: A voxel approach to 3D printing
poster-image: droplet-printing-poster.jpg
published: true
---

Slicers make a 3D printer move in contour lines. This is an efficient method to build up conventional models. But coming from a context of digital images, I wonder if there might be an alternative to this method.
In this experiment, I'll be looking into the possibilities of a [voxel](https://en.wikipedia.org/wiki/Voxel) based approach. Instead of lines, the plastic model would be built up droplet per droplet. 
This admittedly unefficient printing method would allow for a more sponge like texture.
Slicers make a 3D printer move in contour lines. This is an efficient method to build up conventional models. But coming from a context of digital images, I wonder if there might be an alternative to this method that is closer to the pixel.
In this experiment, I'll be looking into the possibilities of a [voxel](https://en.wikipedia.org/wiki/Voxel) based approach. Instead of lines, the plastic model would be built up droplet per droplet.
This admittedly inefficient printing method would perhaps allow for a more sponge like texture, or a printing method based on images or coordinates. So a water-tight mesh object isn't necessary for this method. We still have to keep gravity and thus overhang angles in mind.

The experiments are being done on a [Lulzbot Taz-6](https://www.lulzbot.com/store/printers/lulzbot-taz-6), but the principle should work on any FFF printer.

This is a work in process.

![](/images/droplet-printing-first-drop.jpg)



|![](/images/droplet-printing-01.jpg)|As a first test, I used the gcode from a flattened cube and added a single drop.|
|---|---|
|![](/images/droplet-printing-02.jpg)|Three hardcoded rows with different extrusion amounts.|
|![](/images/droplet-printing-03.jpg)|Three hardcoded row with equal extrusion amounts. The first drop seems to receive too little material.|
|![](/images/droplet-printing-04.jpg)|Extruding more material with a lower nozzle height. Oops!|
|![](/images/droplet-printing-05.jpg)|Coordinates of the drops and the base didn't lign up properly, so I decided to create a parametric base, instead of using the Gcode-output from a slicer. I followed the guide on [creating G-code from Processing](http://www.codeplastic.com/2017/06/05/g-code-with-processing-part-1/) by [CodePlastic](http://www.codeplastic.com).|
|![](/images/droplet-printing-06.jpg)|This one has about 0.1mm thickness. Too thin.|
|![](/images/droplet-printing-07.jpg)|I settled on a base layer height of 0.14mm.|
|![](/images/droplet-printing-08.jpg)|First parametric drops. Not priming material after retracting at the end of the previous print, created some under extrusion at the top of the test piece.|
|![](/images/droplet-printing-09.jpg)|Fixed the under extrusion but made a mistake again when switching from absolute to relative extruder coordinates.|
|![](/images/droplet-printing-10.jpg)|Smaller drops and more under extrusion.|
|![](/images/droplet-printing-11.jpg)|Bigger drops and more under extrusion.|
|![](/images/droplet-printing-12.jpg)|A first test with the second layer. I displaced the second layer in both X and Y, which made the new drops fall down to the base.|
|![](/images/droplet-printing-13.jpg)|Just shifting the second layer on the Y axis, the new drop seem to rest on the two neighbouring ones. The drops seem to be pushed down too much.|
|![](/images/droplet-printing-14.jpg)|Moving the nozzle heigher for the second layer, I hoped to prevent the drops from being pushed down, but the filament was ground away.|
|![](/images/droplet-printing-15.jpg)|I cleaned the feeder motor bolt and lowered the extrusion speeds. I also doubled the extrusion amount for layer 2.|
