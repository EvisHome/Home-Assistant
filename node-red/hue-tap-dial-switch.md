# Hue Tap Dial Switch

## Overview
I have set my light switches so that multiple presses on the buttons change the scene of the light(s) that are linked to that button and holding the same button turns the linked light(s) off.

When any of the buttons are pressed, the dial is activated to the light(s) that is "linked" to that button. So the dial can be used to dim the light which button was last pressed.

## instructions

This needs an input_select helper entity. With this helper you can use the dial to control four different entities. When you push button number 1, the entity_select is set to button1, and you can use that information to control an entity. If you push button number 2 you can now use the dial to control second entity.

### Functions
The *Button Press Loop* function mimics Philips Hue multipress actions. Depending how many times a button is pressed a different action is taken. Only the Button Press Loop you can set your self how many pressesn you want to activate. You have to modify the switch element to match the number of actions you want to output. And there is a time, which after the output resets back to 1.

*Change Brightness* outputs a number between 0-100, it the settings you can set the step and if the output number is decreasing or increasing with every input.

## Node-Red Diagram

## Node-Red JSON
