---
layout: post
title: Droplet Printing
summary: A voxel approach to 3D printing
poster-image: droplet-printing-poster.jpg
published: true
---
 

Slicers make a 3D printer move in contour lines. This is an efficient method to build up conventional models. But coming from a context of digital images, I wonder if there might be an alternative to this method that is closer to the pixel.
In this experiment, I'll be looking into the possibilities of a [voxel](https://en.wikipedia.org/wiki/Voxel) based approach. Instead of lines, the plastic model would be built up droplet per droplet.
This admittedly inefficient printing method would perhaps allow for a more sponge like texture, or a printing method based on images or coordinates. So a water-tight mesh object isn't necessary for this method. We still have to keep gravity and thus overhang angles in mind. Unless we add droplets of PVA to the mix.

The experiments are being done on a [Lulzbot Taz-6](https://www.lulzbot.com/store/printers/lulzbot-taz-6), but the principle should work on any FFF printer. The printing filament used is in house recycled PLA.

This is a research project in progress.

![](/images/droplet-printing-first-drop.jpg)


Creating a sponge like object:

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
|![](/images/droplet-printing-16.jpg)|Making a taller object by stacking layers, shifting them half the size of a droplet (First no shift, then +X, then -Y, then -X, then back to the first XY position), to allow for cavities in the structure.|
|![](/images/droplet-printing-17.jpg)|The top view looks pretty similar to the previous ones.|
|![](/images/droplet-printing-18.jpg)|Maybe the shifting sequence allows for too much space, so the lines become squiggly.|
|![](/images/droplet-printing-19.jpg)|Still all by all a rather rectangular shape. Air can pass easily through it.|
|![](/images/droplet-printing-20.jpg)|For some reason the backside turned out detached from the rest. The outsides are the exceptions of the shifting pattern. I'm curious how the inside looks like.|
 
  
Bigger droplets:

|![](/images/droplet-printing-28.jpg)|Extruding too little material while raising the Z-axis too fast and too far results in little chimney like structures.|
|---|---|
|![](/images/droplet-printing-29.jpg)|Starting 1mm above the base, with 3mm extrusion. This is not yet enough material for the Z-height traveled.|
|![](/images/droplet-printing-30.jpg)|5mm extrusion this time. Still not enough. I waited 4 seconds after moving the nozzle up to let the tips cool down. This way they don't bow down .|
|![](/images/droplet-printing-31.jpg)|10mm material extrusion. The exstrusion is too fast and leaves a rough texture.|
|![](/images/droplet-printing-32.jpg)|This is how it looks after the extrusion is slowed down|
|![](/images/droplet-printing-33.jpg)|The first stacking test had a way too large z-height|
|![](/images/droplet-printing-34.jpg)|Corrected Z-height. Maybe this is a little too packed. There's almost no air pockets anymore. I should increase the droplet height or increase the grid size.|

  
Making big blobs with a 3D printer:

|![](/images/droplet-printing-22.jpg)|By manually extruding copious amounts of plastic through a 0.8mm nozzle, a 3D printer can make very un-3D print like objects.|
|---|---|
|![](/images/droplet-printing-23.jpg)|The shape seems to be determined by the cooling rather than by the plastic extrusion.|
|![](/images/droplet-printing-27.jpg)|This could be the building block of new objects|
|![](/images/droplet-printing-25.jpg)|In this test, we tried to keep the nozzle as deeply submerged in the plastic as we could. The plastic would be about a millimeter away from the heater element at all times.|
|![](/images/droplet-printing-26.jpg)|These tests were done on a printbed at room temperature. Curious what a heated bed and automated extrusion and Z-axis motion will result in.|
