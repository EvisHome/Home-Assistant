# Project Box Creator

### Overview

I wanted to make it as easy as possible to start experimenting with new 3D printable project boxes. I thought I'd parametrize my previous designs with TinkerCad Codeblocks, and for my needs it works really well.

My wall mount kit works also pretty well with the boxes, naturally depends on your box dimensions in the end how well it fits.

## Box Creation Options

*NOTE: When you open the TinkerCad Codeblocks, you may need to scroll to the top to actually see the correct variables that you can changes.*

![](all-box-settings.png)

### Box Dimensions
![](settings-overview.png)

The box dimensions are the external dimensions, if you need to specifically fit something inside, calculate the internal volume you need. Reduce the wall width from both sides, both ends, and from top and bottom to get the internal volume, measure accordingly.


**All dimensions are in millimeters (mm)**

* Box Width (*external width*)
* Box Length (*external length*)
* Box Height (*external height*)
* Wall Width
* Corner Radius
* Snap Length (*snap-in mechanism length on the sides*)

### Board Mount Settings

Optional settings for mounting a boards like ESP32s, Raspberry Pis etc. If you don't need the board mounting just leave leave the "board mount variables" to 0
* Enable Board Mount Feet
* Enable Lid Mount Feet

![](mount-settings.png)

*Note: If your Lid Mount Feet appear to be outside of the Lid inner wall, then you won't be able close the lid (small overlapping with the wall is probably is still fine), and need to make the box a bit bigger.*

### Air Vent Settings

If you don't want any holes in the box side walls, just leave this to 0 (disabled)
* Enable Side Vents

### Box Mount Kit Settings

There are 3 different positions for the mount kit, you can enable each individually, all, or none.

* Wall Mount Kit Hole - Top
* Wall Mount Kit Hole - Center
* Wall Mount Kit Hole - Bottom
