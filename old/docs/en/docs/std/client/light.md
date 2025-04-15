# Lighting settings

> ## Set the specified color  
Change the light mode to static (of course you can also want other effects),
Change the color mode to Select Color.  
- Change the light color to ice blue (#00ffff)  
![](/img/led_col.jpg)  

> ## Turn off the light  
**Same as above, setting it to black means it is turned off. RGBA value 0 0 0 0**

---
> ## Detailed explanation of light mode 

- static  
Set a fixed color,  
Can be implemented in conjunction with events **Press to light and release to turn off** etc.
- Indicator light  
Can be set to Numlock, CapsLock, ScrollLock and other status indicators of the keyboard.  
- breathe  
Achieve breathing effect. If the color mode is selected, the color table can cycle through the colors.  
You can set the light hold and off hold to make the light stay on for a period of time when it is fully on and fully off respectively. Unit 8ms  
- take one breath  
Same as above, but you need to cooperate with the lighting event **Press to execute lighting configuration** to achieve the effect of breathing once for each key press.  
- Gradient  
This mode only works with **Color Table Loop** or **Random Color** in the color mode.
- switch  
The color can be switched according to the specified frequency.  
The lighting time interval needs to be set at the same time. Unit 8ms  
This mode only works with **Color Table Loop** or **Random Color** in the color mode.  
- switch once  
Same as above, but you need to cooperate with the lighting event **Press to execute lighting configuration** to achieve the effect of switching every time the key is pressed.  
- flashing  
Can flash according to the specified frequency and duration.  
The lighting time and off time interval need to be set at the same time. Unit 8ms  
- Flash once  
Same as above, but you need to cooperate with the lighting event **Press to execute lighting configuration** to achieve the effect of flashing once every time the key is pressed.  
- fade  
Need to cooperate with lighting events **Press to execute lighting configuration**  
- Fade in  
Need to cooperate with lighting events **Press to execute lighting configuration**  

---  

> ## Detailed explanation of color mode  

- Select color    
Set the specified color,  
Black equals turning off the lights.  
The darker the color, the lower the brightness.  
- Color Table cycle  
Cycle through colors sequentially in the keyboard's Color Table  
- Random Color Table  
Pick a random color from the keyboard Color Table  
- random color    
Relative to color palette randomness, true randomness may be black (not bright) or white  

---