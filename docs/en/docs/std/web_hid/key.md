
# Key Bindings

> # Setting Keys  

1. Select **Default** key mode  
2. Click the box below to choose keyboard keys:  
- **Ctrl Shift Alt Win** can be **unselected, single-selected or multi-selected**  
- **Other keys** can be **unselected or single-selected**  
- Click again to deselect  

- **Setting Letter A**  
![](/img/A.jpg)

- **Setting Ctrl Key**  
![](/img/Ctrl.jpg)  

<details>
<summary>Trigger Principle</summary>  

  *Maintain at least 20ms after triggering regular keys until release*  
  *Without delay, some software may fail to recognize key presses properly.*  
  *For shorter hold time, use **Keyboard** mode which has no additional delays.*  
  *Ignore this tip if unclear.*  

</details>

> # Setting Shortcut Combinations

- **Setting Copy shortcut Ctrl+C**  
![](/img/Ctrl+C.jpg)

- **Setting Screenshot shortcut Win+Shift+S**  
![](/img/win+shift+s.jpg)

<details>
<summary>Trigger Principle</summary>  

  *In this mode, shortcuts will insert 20ms delay after modifiers before triggering regular keys.*  
  *Maintain regular key for at least 20ms until release*  
  *Without delays, some software may fail to recognize shortcuts properly.*  
  *For simultaneous key triggers, use **Keyboard** mode without extra delays.*  
  *Ignore this tip if unclear.*  

</details>

> # Setting Two-Step Key

!> This mode executes one shortcut when pressed and another when released  

1. Select **Two-step Key** mode  
2. Set two key groups using same method above  

- **Setting Paste+Enter**  
![](/img/2setp_paste+enter.jpg)  

<details>
<summary>Trigger Principle</summary>  

  *Process: Modifiers ->20ms-> Regular keys ->30ms-> Wait release ->Regular keys ->30ms*

</details>

> # Tap/Hold Functionality  

!> Not suitable for rotary encoders

1. Select **Tap/Hold** mode  
2. Set two key groups using same method above  

- **Set tap=A hold=B**  
![](/img/tap_and_hold.jpg)  

- **Set tap=Pause hold=Next Track**  
![](/img/tap_and_hold_mu.jpg)  

<details>
<summary>Trigger Principle</summary>  

  *1. Start 300ms countdown when key is pressed*  
  *2. Trigger hold action if timeout, else trigger tap action*

</details>

> # Mouse Mode  
Set keys as **Left/Right/Middle Click** or **Cursor Movement/Wheel Scroll**  

- **Setting Left Click**  
Select button in **Mouse Buttons**. Set three values to 0  
![](/img/mouse_key.jpg)  

- **Setting Cursor Down**  
Deselect all mouse buttons, set **Y-axis Move** to -1  
![](/img/mouse_move_down.jpg)  

- **Setting Wheel Scroll Down**  
Deselect all buttons, set **Scroll** to -1  

```
Horizontal: Positive=Right, Negative=Left  
Vertical: Positive=Up, Negative=Down  
Wheel: Positive=Forward (Reverse on Mac)  
Larger values mean faster movement.  
Continuous 50ms interval movement when holding key  
```

> # Media Controls  
System volume control, track switching, screen brightness etc.  

!> Brightness control only works for laptops or displays supporting system-level adjustment  

- **Setting Mute Toggle**  
![](/img/mute.jpg)  

  *Repeat Count triggers multiple presses (1-255 times)*
---  

> # Keyboard+LED Control  

!> *This mode sends LED status keys before/after shortcuts to update indicators*  
*Shortcuts can be empty for pure LED control*  
*Includes Num Lock/CapsLock/Scroll Lock*   
- **Enable NumLock & Disable CapsLock**  
![](/img/key_and_led.jpg)  

<details>
<summary>Trigger Principle</summary>  

  *1. Enable target LEDs (auto-send keys)*  
  *2. Send configured keys*  
  *3. Disable target LEDs (auto-send keys)*  

</details>

> # A+B+C+D Mode
*Press selected keys sequentially then release together*  
*For strict key sequence requirements or short key sets.*  
*Max 4 keys*  


> # One-key Password
*Type preset ASCII string automatically*  

- **Set auto-type "123456"+Enter**  
1. Enter content in **Assets->Passwords**  
![](/img/pwd_data.png)  
2. Change mode to **One-key Password** and select password ID  
![](/img/pwd.jpg)  
3. Append Key  
Add an extra key like Enter after password:  
![](/img/pwd_key.jpg)  
4. Input Interval  
Typing speed (default OK). Increase if missing characters occur.  
Recommended ≥10 for Bluetooth  
![](/img/pwd_time.jpg)  
5. CapsLock Lock  
Auto-lock caps during input to avoid IME interference:  
![](/img/pwd_case.jpg)  

- Other Layouts  
Default ANSI layout. Enable AZERTY in Device Options if needed

<details>
<summary>Trigger Principle</summary>  

  *1. Adjust CapsLock state (auto-send keys)*  
  *2. Send characters sequentially*  
  *3. Restore CapsLock state (auto-send keys)*  

</details>

> # One-key Web
Windows only, same setup as password

<details>
<summary>Trigger Principle</summary>  

  *1. Win+R to open Run dialog + auto caps lock*  
  *2. Wait ~500ms for window opening*  
  *3. Send characters and Enter*  
  *4. Restore CapsLock state*  

</details>

---  

> # One-key Text
Output preset text string

!> Partial devices unsupported  
**Potential shortcut conflicts.**  
Windows only  

Similar to password setup but input in **Text** tab with two encodings (GB18030/UTF16-LE)  
Switch encoding if garbled characters appear  
It is recommended to use the one-key password function for English content  

<details>
<summary>Trigger Principle</summary>  

*Input via Alt+Numpad code entry.*  

</details>

> # Shortcut *3
Execute three consecutive shortcuts like **Select All+Copy+Tab Switch (Ctrl+A C T)**

> # Loop Input
Loop through 1-3 keys when held. Interval = n×6ms

- **Cycle Down Arrow + Space**  
![](/img/while_down_and_space.jpg)  

> # Lock Mode

- **Press to hold A, press again to release**  
![](/img/key_mode_sl.jpg)  

> # Gamepad Button

!> Windows only. Do NOT enable on Mac.  
If enabled by mistake, disable via Windows.  

Enable **joystick** in Device Options' HID Features (save & replug).  
Set mode to **Gamepad Button** and input ID (0-127 valid).  
Requires game support for custom button mapping.

> # Key-to-Axis
Map linear key to joystick axis (requires Gamepad HID) or mouse movement (Relative Mouse)

!> Partial devices unsupported  

- Axis Options: X Y Z rX rY rZ 
- Mouse Axes: X/Y

- Alignment Modes  
Left/Right/Center-left/Center-right

> # Numlock Virtual Layer 

- **Key=A when NumLock on, Key=B when off**  
![](/img/num_sw.jpg)  

> # FN Layer Switching  

!> Partial devices unsupported

1. Set key mode to **FN** and select target layer  
2. Pressing switches layers temporarily  

![](/img/FN.jpg)  

<details>
<summary>Trigger Principle</summary>  

  *1. Store current layer*  
  *2. Switch to target layer*  
  *3. Wait release*  
  *4. Restore original layer*  

</details>


> # SW Layer Switching

!> Partial devices unsupported

- Direct layer switch on press

> # Bluetooth Device Switching

!> Partial devices unsupported  
Bluetooth mode only  

- Set key for fast device switching  
- Auto pairing mode (white LED blink) if device offline