---
layout: post
title: Stutter Code
summary: Interrupting the flow reveals the underlying structure of the Gcode
poster-image: stuttercode-poster.jpg
published: true
---

A simple hack that inserts a short pause after every move in a Gcode file makes a little filemant ooze out of the nozzle. This creates patterns resembling artisanal basketry.


![](/images/stuttercode-1022065.jpg)
 
 
![](/images/stuttercode-cura.jpg) 
In this first test, we sliced a simple cylinder with a concentric top/bottom pattern and exported the Gcode file.

![](/images/stuttercode-original_gcode.jpg) 
This is the original Gcode, opened in a text processor.

![](/images/stuttercode-grep.jpg) 
Using the search and replace function with [GREP](https://www.regexbuddy.com/regex.html) enabled, we can search for any 3D print move with the pattern `^(G1 X.*$)`. Anything in the brackets is used in the replace section with `\1`, and here we added a newline, and the [dwell command](https://reprap.org/wiki/G-code) G4 P200, to pause the machine for 200 milliseconds after every move.

![](/images/stuttercode-modified_gcode.jpg) 
This is the modified Gcode.

It might be fun to make local changes in the duration of the pause.
