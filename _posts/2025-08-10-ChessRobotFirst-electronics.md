---
title: Chess-Playing Robot — Basic Electronics
description: First electronics shakedown! Getting basic CNC functionality up and running.
date: 2025-08-22 15:42:14
categories: [Chess Robot, Electronics]
tags: [Chess, Sensors, Electronics, Arduino, CNC,  GRBL, Gcode, Universal Gcode Sender, CAD, Onshape, 3D Printing]
image:
  path: "/assets/chess/4elec/googlydemo_cropped.gif"
  alt: "THE GOOGLY EYES ARE EVERYTHING"
pin: false
---

> **Work in Progress — Basic Electronics**  
> Developing the electronics needed for basic motion. Advanced path planning and algorithmic control and sensors coming eventually.
{: .prompt-tip}
 
---

 ![grbllogo](/assets/chess/4elec/arduinogrbl.png){: .right}
## Last post's todolist COMPLETE!
- [x] Printed new carriage parts  
- [x] Mounted linear rails and bearings  
- [x] Integrated stepper driver and GRBL test  
- [x] Wired endstop sensors  
- [x] Begin motion testing

### And most importantly 
{: data-toc-skip='' .mt-4 .mb-0 }

## IT MOVES AND HAS GOOGLY EYES 
{: data-toc-skip='' .mt-4 .mb-0 }

---

## Research 

Early in my research for this project I came across GRBL, and the CNC Shield for the Arduino Uno. They are the standard answer for hobbyists trying to make their own custom CNC machines, plotters, and some 3D printers. Which is kind of what this robot is designed to be. Its got about 64 specific locations that we can send the end effector to to pick an place. Its kinda like a tool change at 64 locations. GRBL is flashed onto the Arduino and Gcode can then be sent to the robot directing its movements. Gcode is the industry standard for this type of motion. CNCs and 3D printers all use it. (This version of GRBL is slightly modified to accept servo commands.)

---

## Arduino and Motor controller
My solution to use this pair and is obviously financially motivated. Once I get everything up and running the way I like, I can look into more powerful controllers if needed... But honestly for this application all the controller needs to do is wait for the Gcode to come from our pipeline and make a few efficient movements. 
<div style="display:flex; gap:10px; flex-wrap:wrap; justify-content:center;">
  <figure style="flex:1; min-width:280px;">
    <img src="/assets/chess/4elec/Arduinouno.png" alt="Ol' Reliable" height="100%">
    <figcaption><em>Ol' Reliable Arduino Uno</em></figcaption>
  </figure>
  <figure style="flex:1; min-width:280px;">
    <img src="/assets/chess/4elec/CNCShield2.png" alt="CNC Shield" height="100%">
    <figcaption><em>CNC Shield that mounts directly on top of the Uno</em></figcaption>
  </figure>
</div>

![A4988 driver](/assets/chess/4elec/A4988.png){: .right}
The shield literally just pops in on top of the Arduino and is done. A few enabling jumpers and it will run on its own power supply that we give separate to the Arduino drawing its 5 volts from the USB.

On top of THAT the shield takes a few dedicated motor drivers. One for each stepper motors we are running. 

All told the electrical hardware was pretty cheap:
- Stepper Motors $16.99 (x3 I got an extra)
- Arduino Uno Kit $26.99
  - CNC Shield
  - Arduino Uno
  - 4x Motor Drivers w/ radiators
  - 4x end stop switches 
  
about $78 plus tax. 

---
## Universal Gcode Sender
![UGSlogo](/assets/chess/4elec/UGSlogo.png){: .right} 
Of the Multitude of different methods of interfacing with the Arduino the most straight forward I've found so far with the most features and customization options, to use until I build my own python or ROS2 pipeline. It can import images and convert them to Gcode, which is the next step on the road. In order to get everything dialed in and make sure the structure can stand up to the movement in terms of things like rigidity and vibration. 

### Tuning

As part of the setup we need to tell the motors to move a set amount and compare that to what actually happens. I did this by zip tying a pencil to the X-Axis carriage and putting a ruler underneath it to see the actual distance moved. 

### Features

- Convert images to SVG and Gcode for the machine 
  - Takes into account the specific machines envelope
- I can make it controlled by a joystick IMPORTANT
- Large display of movement info for testing
- Control for pen up and down commands
- Support for hard endstops

---

## End Stops 

I ended up using 4 switches for end stops for maximum safety. The two at the home (0,0) coordinates are important for homing the system each time for calibration purposes. The two at the extremes of the envelope are mostly useless since I will be including soft limits for the robots travel, but they will be useful in case of coding errors or swapped symbols... not that I would ever make such a mistake. 

The switches themselves are just hot glued in place at the extremes of the Y-Axis and on the bottom of the X-Carriage as it moves from end to end.

---
## Goals for next time!

I know this post is pretty quick. I'll post more next time, working out the electronics was more work than anticipated. 

- [ ] Design and Prototype Plotter head  
- [ ] Integrate to run on Raspberry Pi  
- [ ] Draw something cool!
- [ ] Re-design and print permanent mountings for end stop switches
- [ ] Maybe add a joystick and arcade buttons?!?

---


[← Back to Projects](/projects)

