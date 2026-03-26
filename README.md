# Thrustmaster Warthog extended button TARGET script

Inspired by sedenion's [Thrustmaster Combined Full DX Mapping](https://forum.dcs.world/topic/144048-thrustmaster-combined-full-dx-mapping-extending-the-32-dx-buttons-limit/).
I found their script a little too specific to DCS, and I needed something more universally usable. Specifically I needed something that could also turn the toggle switches into PULSE button presses.

This script combines the Thrustmaster Warthog into a single combined device that supports up to 120 buttons and 8 axis. 
Additionally, it changes the toggle buttons into momentary button presses.
This gives much better support to games which have limited or no support for press-and-hold style buttons (e.g. IL-2 Great Battles and Elite Dangerous).
Toggle switches send a single button pulse when toggled up or down, instead of holding the button.

This script has several optional features:

* Split each toggle position into it's own button assignment.
* Split short and long press as two separate button assignments on most hats and buttons.
* Change the APENG button assignment based on the position of the two adjacent toggles.
* Change the Left Throttle DX button based on the position of the pinky switch.
* Use the Slew as a mouse.

What this script does not do:

* Support anything other than the Thrustmaster Warthog and default grip.
* Assign game specific keyboard functions.
* Sync LED state.
* Require multiple files or external libraries.
* Static button assignments.
* Anything too clever to make it difficult to customize.

## Installation
Simply download the script to your preferred location. 
Open and Run it with the TARGET Script Editor.

## Configuration
This script is designed to be easily modifiable. It's all contained in one file with simple code even novices scripters can likely modify it.

You can easily configure the script behavior at the top of the script using the following defines.

| define| description |
|-------|-------------|
|AUTOPILOT_MACRO| When 1, activates the advanced Autopilot macro for the APENG button. Otherwise works as a normal button. |
|MULTI_FUNCTION_TOGGLES| When 1, every toggle sends a different DX button for each state of the toggle (e.g. DX40 in when flipped on, and DX41 when flipped off). This is recommended if for games that support separate on/off control bindings. When 0, both states send the same DX code.|
|SLEW_IS_MOUSE| When 1, the slew works as a mouse axis, and the slew click as a mouse Left Click. Otherwise works as an additional two axis and DX button.|
|LONG_PRESS_FUNCTIONS| When 1, most buttons outside of the Triggers, Boat Switch, Speed Break, and POVHat send a different DX button on long press.|

An important note is that DX button assignments are dynamic, and may change if you change configuration options. Make sure to finalize your customizations before binding controls in your game.

### Advanced Configuration
You may wish for certain toggles to send separate DX buttons for each states, and others to simply repeat the same state in up/down position. Simply scan through the code for the matching MapKey assignents, and change the surrounding `if(MULTI_FUNCTION_TOGGLES){` block to `if(0){` or `if(1){` to enable or disable multifunction toggles for that specific swtich. 

To turn off long press functions for a specific button, replace the NextTempoDX() function call in the appropraite MapKey assignment with NextDX().

## Autopilot Macro
The autopilot macro is designed for the following autopilot modes. Path, Altitude/Heading, Altitude bank right, Altitude bank left. The APENG will send a different DX button for each of the following states.
|LASTE == APPAT|
|LASTE == APAH|
|LASTE == APALT && RDR_ALTM == RDRNORM|
|LASTE == APALT && RDR_ALTM == RDRDIS|

Essentially, the RDR ALTM switch would control the banking direction when in AP ALT autopilot, but otherwise not affect APPATH or APAH mode.

## Configure Mouse sensitivity
If using SLEW_IS_MOUSE, you can adjust the S-Curve found near the bottom of the script. I have a modified Slew thumbstick, so the default slew might require an even more aggressive decrease in sensitivity.
