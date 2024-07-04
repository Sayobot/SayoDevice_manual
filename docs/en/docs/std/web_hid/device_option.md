# Device option

!> Different devices may support different functions

> ## Key debounce time
>
> release-debounce, default value 10, unit milliseconds, generally not recommended to modify.
> If the key is double-clicked, you can try to increase this value to more than 20

!> Not effected to hall keys. hall keys does not need debounce

---

> ## Device function
>
> Extended function, select every one you need

- ### Relative mouse

Control cursor movement, mouse button clicks, etc.

!> After setting, you need to save and reconnect the data cable  
If you use Bluetooth, you need to delete the device and re-pair

---

- ### Multimedia control  
  Adjust volume, etc.

!> After setting, you need to save and reconnect the data cable  
If you use Bluetooth, you need to delete the device and re-pair

---
- ### Joystick  
  Turn on **joystick** in the option byte  
  Change the key mode to **game controller**,  
  Then select the key number.  
  This key has nothing to do with any key on the game controller, and the game needs to support custom keys.

!> Only for **windows**.  
MacOS **Don't** turn it on, it will cause it to be unusable. If it is turned on by mistake, you can use the windows system to turn it off.  
After turning on this option, the keyboard can be recognized as a game controller by the game.  
After setting, you need to save and reconnect the data cable.  
If you use Bluetooth, you need to delete the device and re-pair.

---
- ### dial mode  
  This option is only useful for knobs.  
  Device options->Device function->Dial  
  In **windows system**, you can set different functions for different software.

!> After setting, you need to save and reconnect the data cable.  
If you use Bluetooth, you need to delete the device and re-pair.

---

- ### absolute mouse  
  After turning on this function, you can use the cursor positioning function in the script, and you can record and replay mouse operations.  
  Recording is limited to **windows system. **

!> After setting, you need to save and reconnect the data cable.  
If you use Bluetooth, you need to delete the device and re-pair.

---

- ### controller  
  Simulate a complete game controller, including 8 axes and Hat switch, buttons, etc.

!> After setting, you need to save and reconnect the data cable.  
If you use Bluetooth, you need to delete the device and re-pair.

---

- ### Other options

- Power-on delay  
  After turning on this option, the USB will be recognized after a delay of 0.5 seconds after insertion. Suitable for some slower computers.  
  If the device cannot be recognized normally, you can try to turn it on.

- AZERTY Keyboard  
  After turning on this mode, the one-key password is suitable for French keyboards.

- ~~KVM Compatibility mode~~  
  Deprecated, no need to care

- Disable lighting  
  As the name suggests, turning on this function will block the light.

---

> ## Language
>
> Modify the display language of the device (if there is a screen)

> ## Computer screen width and height
>
> The script uses the reference resolution for cursor positioning, which is generally configured automatically by software

> ## USB rate
>
> USB report rate selection. Default value 1000HZ

> ## Encoder channel
>
> For options that are only useful for knobs, **do not modify. **

> ## Sleep timeout
>
> Wireless mode is available, wired mode is invalid. You need to use a data cable to connect the keyboard to change.

> ## Indicator light timeout
>
> Wireless mode is available, wired mode is invalid. You need to use a data cable to connect the keyboard to change.

> ## Keyboard layout
>
> Key layout for one-key password function output
