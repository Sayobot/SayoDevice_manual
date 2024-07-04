# Screen settings

!> Only some devices with screens

## Start

![](/img_screen/screen_main.jpg)

---

## Interface switching

There are three interfaces:  
Power-on interface: Displayed once when the device is powered on.  
Main interface: The interface displayed in normal state.  
Sleep interface: The interface displayed after **screen timeout** without any operation 

## Layers  

Select a layer on the right side of the interface  
The layers are drawn in order from **#01 to #16. **  
The layers with larger numbers will **overwrite** the layers with smaller numbers.  
**Click ⠿ on the right side of the layer to drag the layer order**  

## Layer type  

> ### Clear screen  
>
> Clear the image content of the previous frame. Usually set to #01, do not modify.  
> Exception: #01 is a complete image  

> ### Blank
>
> Do not use this layer

> ### Solid color
>
> Draw a solid color rectangle of specified width  

> ### Built-in components
>
> Built-in widgets.  
> Some components need to set color to display  
> 0=empty  
> 1=key velocity bar, vertical  
> 2=key velocity bar, horizontal  
> 3=CPU Load  
> 4=bangocat  
> 5=key indication  
> 6=system frequency information  

> ### Built-in counter
>
> Key counter  
> You can set the maximum number of digits. Maximum 10 digits.

> ### ASCII string
>
> Display a text  
> Support English letters and symbols

> ### Built-in icon
>
> Built-in image of keyboard

> ### Material (custom image)
>
> Uploaded custom image (upload in the material tab on the left side of the page)

## Layer parameters

> ### Displayed button layer
>
> Whether this layer is displayed in a certain button layer

> ### Trigger key
>
> Only effective with trigger events.

> ### Trigger event
>
> Optional always display, display when button is pressed, display when button is released, etc.

> ### Offset X/Y
>
> Layer offset, relative to the upper left corner.

> ### Material number
>
> Select different images or components. Range 0~x

> ### Maximum digits
>
> Maximum digits to display

> ### Text color
>
> Text color

> ### Background color
>
> Valid after background is turned on.
