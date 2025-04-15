# Option Bytes

> ## Release Dealy  
Post-debounce, default value 10, unit in milliseconds. Generally not recommended to modify.  
If double-clicking occurs, try increasing this value to 20 or higher.  

---

> ## HID Features  
Extended features, enable as needed. Unsupported options will not appear in settings.  
**If using Bluetooth mode, delete the device and re-pair it after enabling.**  

### Relative Mouse  
Controls cursor movement, mouse button clicks, etc.  

### Multimedia Control  
Adjust volume, etc.  

### Joystick  
Only applicable to **Windows**.  
**Do not** enable on **macOS**—it may cause malfunctions. If accidentally enabled, use a Windows system to disable it.  
After enabling this option, the keyboard can be recognized as a game controller by games.  
Enable **joystick** in the option bytes.  
Save settings and reconnect the USB cable after configuration.  
Switch the key mode to **Game Controller**,  
then select the button number.  
This button is independent of any gamepad buttons and requires game support for custom keybindings.  

### Dial Mode  
Only functional for knobs.  
Allows different software-specific configurations in **Windows**.  
Save settings and reconnect the USB cable after configuration.  

### Absolute Mouse  
Enables cursor positioning in scripts and mouse action recording/playback.  
Exclusive to **Windows**.  

### Gamepad  
Emulates a full game controller, including 6 axes, a hat switch, buttons, etc.  

### Other Options  

- Power-On Delay  
Delays device recognition by 0.5 seconds after USB insertion. Suitable for slower computers.  
If the device fails to initialize, try enabling this option.  

- AZERTY Keyboard  
Enables one-key password compatibility for French keyboard layouts.  

- Disable Lighting  
Self-explanatory—enabling this option turns off all lighting effects.  

---  

> ## Language  
Modifies the display language of the device (if equipped with a screen).  

> ## Screen Width/Height  
Reference resolution for cursor positioning in scripts. Typically auto-configured by software.  

> ## USB Polling Rate  
USB report rate selection. Default: 1000Hz.  

> ## Keyboard Layout  
Key output layout for the one-key password function.  

> ## Oversampling  
Precision setting for the magnetic axis function. Default value: 10.  