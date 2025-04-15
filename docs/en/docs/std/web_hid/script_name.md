
# Script Name  

## 1. Function  
- Distinguish script functionalities  
- Restrict parameter types for flexible script reuse  

## 2. Parameter Constraints  

<details>  
<summary>Expand details</summary>

| Symbol | Description          | Format                | Remarks                                                                 |  
|--------|----------------------|-----------------------|-------------------------------------------------------------------------|  
| ~      | Parameter end        | ~                     | Marks the end of parameters, followed by the script name (mode name)    |  
| \      | Parameter type       | \a\b\c\d~            | Parses a single letter (defaults to "\\u\\u\\u\\u~" if the script name does not start with "\\", "\{", or "~") |  
|        | Parameter name       | \m modifier\g normal~ | Letters followed by parameter names                                     |  
| -      | Custom option (single choice) | \U switch-0on-1off~ | -value + option name                                                    |  
| =      | Custom option (multi-choice) | \U mouse=1left=2right=4middle~ |                                                                 |  
| {}     | Collection           | {\m\g}short{\m\g}long~ |                                                                 |  
| \\u    | Unsigned 0~255       |                       |                                                                         |  
| \\s    | Signed -128~127      |                       |                                                                         |  
| \\\\u  | Unsigned 0~65535     |                       |                                                                         |  
| \\\\s  | Signed -32768~32767  |                       |                                                                         |  
| \\\\\\\\u | Same as above      |                       |                                                                         |  
| \\\\\\\\s | Same as above      |                       |                                                                         |  
| \m     | Modifier key         |                       |                                                                         |  
| \g     | Normal key           |                       |                                                                         |  
| \M     | Mouse key            |                       |                                                                         |  
| \c     | Multimedia key       |                       |                                                                         |  
| \j     | Joystick key         |                       |                                                                         |  
| \a     | Joystick axis        |                       |                                                                         |  
| \P     | Password             |                       |                                                                         |  
| \S     | String               |                       |                                                                         |  
| \A     | Keyboard LED (Numlock, etc.) |               |                                                                 |  
| \L     | Key layer            |                       |                                                                         |  
| \U     | User-defined options |                       |                                                                         |  

</details>  

## 3. Usage Examples  

- **Before**  
A script automatically clicks the A key repeatedly when held down, with a 35ms interval and 20ms random variation.  
![alt text](/img_script_name/1.jpg)  
When bound to a key, it appears as:  
![alt text](/img_script_name/1.1.jpg)  
Difficult to distinguish functionalities and lacks flexibility in modifying keys.  

- **After**  
A script automatically clicks the V0 key repeatedly when held down, with a V1 ms interval and V2 ms random variation.  
![alt text](/img_script_name/2.jpg)  
When bound to a key, it appears as:  
![alt text](/img_script_name/2.1.jpg)  
Now you can use names to distinguish specific script functionalities, flexibly adjust keys and timing, and reuse the script across different keys.  