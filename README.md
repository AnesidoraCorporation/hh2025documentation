# Hacker Hotel Banana
The badge comes with a default bananamode, a charging mode and an option to create new bananamodes. The following section will focus on the default mode, followed by the charging mode. If you want to read about creating your own mode, read the 'Alternative modes' section.

Note: in the code and the documentation it is assumed we are looking to the front of the badge. This is when you can read the Hacker Hotel logo in a normal way.

## Default mode
* switch1 - change team (team 1 (red) or team 2 (green))
* switch2 - only changes color of third RGB LED (D3)
* btn1 - Select previous ledmode (see topic ledmode)
* btn2 - Select next ledmode (see topic ledmode)
* s1 - this is the "trigger". You can move it to both sides and push it. In the code "moving to both sides" is defined as left and right so we stick to that here.
  * swleft - to the left: change banana mode
  * swright - to the right: shoot
  * swmiddle - push: reload

* led1 to led5 - individually controlled LEDs. See ledmode section for usage.

* irin (U3) - IR sensor
* irled (D4) - IR LED 

In the default mode you can shoot 5 times. After that, you can "reload" by pressing the trigger button (swmiddle). If you get shot, a counter will count to 5. After 5 shots, your banana will turn into "game over mode". The restart the default mode, press btn1 for about 1 or 2 seconds.

### ledmode
ledmode is a special mode option available in the default bananamode. Within the default bananamode, use btn1 and btn2 to navigate through the modes. ledmode has three different modes:
* ledmode 0: shows the battery status
* ledmode 1 (default): shows number of shots left
* ledmode 2: shows number of hits.

## Charging mode
Charging mode is primarily designed for charging your banana at night while you are trying to catch some sleep without a neopixel disco effect.
* While charging only led5 (D12) will turn on
* When it is done charging or simply not charging, the neopixel D2 will turn green on modest brightness.

## Alternative modes
One of the ideas with this badge is that as much people as possible should be able to play with the code. That's why it is written in CircuitPython. You can alter to code and upload it and that is bassically it. But if you want to keep the original code and want build on top of it, there is some structure available to do so. You can read that here.

(Btw, you don't have to stick with the default code or even CircuitPython!)

### Using the alternative mode
Next to the default mode there is one alternative mode already embedded in the main loop. Every time the loop executes it will check the `current_mode`. By default the current mode is 0 and this is by default the only banana mode available/configured. To add a banana mode, you should edit the `banana_modes` variable. This is by default this list `[0]`, it only contains the default mode 0. Change it to `[0, 1]`, to make the alternative mode available. 

Since the code for this banana mode was already embedded it will work immediately, although the only working feature is to set the next mode (because otherwise you're not able the change the mode as soon as you changed it). Also we set up some of the basic interactions/triggers you could now code yourself.

### Add new alternative mode
If you want to add extra alternative modes you can simply add a new `elif current_mode == <int>` to the main loop. The following code is a minimal example to get it to work.

```
elif current_mode == 2:

    # pixels[1] = colors("blue") # optional color setting
    # pixels[2] = colors("blue") # optional color setting

    # Mode selection
    if swleft.value == 0:
        current_mode = set_mode()
        time.sleep(mode_delay)
```

And also add your new bananamode to the `banana_modes` variable. See topic above for more information
