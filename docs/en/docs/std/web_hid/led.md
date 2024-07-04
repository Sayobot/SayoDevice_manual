# Light settings
!> Only devices with key lights support this feature

> ## Set the desired color
>
> Change the light mode to static (of course you can also use other effects),
> Change the color mode to a specified color.

- Change the light color to ice blue (#ff00ff)  
![](/img/led_col.jpg)  

Tip: Click the **pipette icon** to **pick the color from the screen**

> ## Turn off the light
>
> **Same as above, set it to black to turn it off. RGB value 0 0 0** (#000000)

---

> ## Light mode details

- Static  
Set a fixed color,  
Can be used with **key events** to achieve **press on, release off**, etc.  

- Indicator light  
Can be set to the keyboard's **Numlock CapsLock ScrollLock** and other status indicators.

- Breathing  
Achieve a breathing effect. Use variable color with color mode  
You can set the light-on hold and light-off hold to make the light stay for a period of time when it is fully lit and fully off respectively. Unit 8ms  
- Breath once  
Same as above, but need to cooperate with the light event **Execute light configuration after pressing** to achieve the effect of breathing once for each key press.
- Gradient  
When the color mode** is not the specified color**, it is effective.
- Switch  
You can switch colors at the specified frequency,
You need to set the lighting time interval at the same time. Unit 8ms
When the color mode** is not the specified color**, it is effective.
- Switch once  
Same as above, but need to cooperate with the light event **Execute light configuration after pressing** to achieve the effect of switching once for each key press.
- Flash  
You can flash at the specified frequency and duration.
You need to set the lighting time and the time interval for the light-off at the same time. Unit 8ms
- Flash once  
Same as above, but need to cooperate with the light event **Execute light configuration after pressing** to achieve the effect of flashing once for each key press.
- Fade  
Need to cooperate with light events **Press to execute light configuration**
- Fade in  
Need to cooperate with light events **Press to execute light configuration**

---

## Color mode details

- Specify color  
Set a desired color,  
Black is equal to turning off the light.  
The darker the color, the lower the brightness.  

- Color table cycle  
Cycle the colors in the keyboard's built-in color table in sequence  
- Color table random  
Randomly select colors in the keyboard's built-in color table  
- Random color  
Compared with color table random, true random may be black (not bright) or white  

---