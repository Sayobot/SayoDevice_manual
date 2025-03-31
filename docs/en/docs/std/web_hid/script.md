# Device Scripts

!> This feature is only supported by certain device models

## Introduction

**Overview**

With scripts, you can implement complex operations, including but not limited to:

- A sequence of keyboard and mouse operations
- Loops (both global and local)
- Control of RGB lighting effects
- Advanced operations (utilizing a rich set of commands and interfaces)

**Reading Guide**

- If you have no programming background or don't want to dive deep, you can just read the first 3 chapters
- For quick reference, the command table at the end of this document often provides the fastest answers
- If something is unclear, don't stop reading - understanding will come after reading the entire document
- For advanced users, the complete command syntax is documented in the later sections

## **0. Getting Started**

**What is a script?**

- A script (also known as a macro) is a sequence of programmed actions
- Scripts orchestrate a series of events to happen in a defined order

**What can scripts do?**

The possibilities are limited only by your imagination:

- Execute keyboard input and mouse movements/clicks
- Control RGB lighting effects
- Even create a hardware calculator with the right commands

**How do scripts run?**

- In most cases, a key acts as a switch - pressing the key executes the associated script
- When a script runs, the 4 parameters set in the key settings are passed to the script's registers
- Scripts execute from top to bottom, performing each command in sequence
- Scripts continue running until they encounter a **delay**, **blocking command**, or **exit instruction**

## **1. Creating Your First Script**

**Script Editing Interface**  
![Script interface](img/script.jpg)

**Basic Key Operation (shown above)**

- The most basic sequence has 4 steps: press, delay, release, delay (the final delay can be omitted if it's the end of the script)
- Delay units are milliseconds (1 second = 1000 milliseconds)
- Minimum delay is 1 ms, but 5 ms or more is recommended for reliable operation
- Human key presses typically last at least 30 ms

**Assigning Scripts to Keys**

1. Change the key mode to "User Script" + script number (No.xxx)
2. Enter parameters (can be left at defaults for basic scripts)

![Multiple key operations](img/script_2_key.jpg)

**Adding More Keyboard Actions**

- Simply repeat the press, delay, release, delay sequence for each key
- Using the recording feature is recommended for complex sequences

## **2. Basic Commands**

### Delay Commands

- Pause script execution for a specified time
- Delays are measured in milliseconds
- Delay values range from 0~255 (unless using variables)  
  **Delay Multipliers**
  - x1: 1=1ms (the value entered equals the delay in milliseconds)
  - x256: 1=256ms (entering 1 creates a 256ms delay, 2 creates a 512ms delay)  
    **Random Delays**
  - Random range from 0 to (multiplier × entered value)
  - The entered value **absolutely cannot** be 0
- Examples:  
  **Delay for 0.1 seconds (100 milliseconds)**

```
-Delay x1 100
```

**Delay for 0.3 seconds (300 milliseconds)**

```
-Delay x1 200
-Delay x1 100
or
-Delay x256 1
-Delay x1 44
```

**Random delay between 0.2~0.3 seconds**

```
One fixed delay followed by one random delay:
-Delay x1 200
-Delay-Random-x1 100
```

---

### Key Operations

- Send basic key operations to the computer
- Always add a delay between two key operations
- Supports any operation nesting  
  **Key Values**
  - Directly select key operations
  - Operation content is fixed  
    **Parameters (advanced users)**
  - Use parameters or variables to reuse code or scripts
  - Operation content is flexible
- Examples:  
  **Press key A for 35 milliseconds (short press)**

```
-General Key-Value-Press A
-Delay x1 35
-General Key-Value-Release A
-Delay x1 35
```

**Press key A for 2 seconds (long press)**

```
-General Key-Value-Press A
-Delay x256 7
-Delay x1 208
-General Key-Value-Release A
-Delay x1 35
```

**Combination key Ctrl+C**

```
-Modifier Key-Value-Press Ctrl
-Delay x1 35
-General Key-Value-Press C
-Delay x1 35
-General Key-Value-Release C
-Delay x1 35
-Modifier Key-Value-Release Ctrl
-Delay x1 35
```

**Press key A for 35 milliseconds (short press) in a loop**

```
-General Key-Value-Press A
-Delay x1 35
-General Key-Value-Release A
-Delay x1 35
-Jump to Address 0 0
```

---

### Cursor Operations

- Move/position the mouse cursor
- Always add a delay between operations, and reset to zero after operations  
  **Axes**
  - X: Screen horizontal coordinate, positive to the right
  - Y: Screen vertical coordinate, positive downward
  - Scroll: Wheel operation
- Examples:  
  **Move cursor right**

```
-Mouse-Cursor Move-Value X-axis 10
-Delay x1 35
-Mouse-Cursor Move-Value X-axis 0
-Delay x1 35
```

**Move cursor down**

```
-Mouse-Cursor Move-Value Y-axis 10
-Delay x1 35
-Mouse-Cursor Move-Value Y-axis 0
-Delay x1 35
```

**Position cursor at specific coordinates (x,y) and left-click**

```
-Mouse-Cursor Position 100,100
-Delay x1 35
-Mouse Key-Value-Press Left Button
-Delay x1 35
-Mouse Key-Value-Release Left Button
-Delay x1 35
```

## **3. Special Commands**

### Enter Momentary Mode

- By default, scripts operate in toggle mode: press once to start, press again to stop (if still running)
- In momentary mode, scripts can only exit through commands
- Usually placed as the first instruction

### Key Blocking

- When this step executes, the script pauses if the key is in the specified state
- Execution resumes when the condition is no longer met  
   **Example:**  
  **Press A, release B**

```
-General Key-Value-Press A
-Delay x1 35
-General Key-Value-Release A
-Delay x1 35
-Block While Key Pressed
-General Key-Value-Press B
-Delay x1 35
-General Key-Value-Release B
-Delay x1 35
```

**Press once for A, press again for B (requires momentary mode)**

```
-Enter Momentary Mode
-General Key-Value-Press A
-Delay x1 35
-General Key-Value-Release A
-Delay x1 35
-Block While Key Pressed
-Block While Key Released
-General Key-Value-Press B
-Delay x1 35
-General Key-Value-Release B
-Delay x1 35
```

### Key State Exit

- **When this command executes**, the script exits if the key is in the specified state, otherwise continues  
   **Example:**  
  **Hold to continuously output keys, release to exit**

```
-General Key-Value-Press A
-Delay x1 35
-General Key-Value-Release A
-Delay x1 35
-Exit If Key Released
-Jump to Address 0 0
```

## **4. Reserved**

## **5. Command Architecture**

!> Please ensure your device firmware is updated to the latest version.  
Older versions may lack certain registers (reading will return 0)  
Older versions may not support certain commands (scripts may exit unexpectedly)

### Overall Architecture

- Scripts typically run on keys
- Each key can be considered a separate thread, with multiple threads running simultaneously
- Each thread has independent registers, but can access shared memory regions via pointers
- Each thread has 4 8-bit parameter registers (parameters passed through the key, read-write, can be independently reloaded), 4 32-bit special registers (for data storage or pointers), 1 32-bit A register (for accumulation, multiplication, division), and 1 32-bit B register (for division)

### Jump Control

- FLAGS were introduced to simplify jumps without the need to calculate addresses
- The SET_FLAG command can push the address of the next instruction into a register
- When jumping, if the register is 0, it will search forward

### Registers

| Name           | Value Range   | R/W | Usage                                                                     |
| -------------- | ------------- | --- | ------------------------------------------------------------------------- |
| Param 1~Param 4| 0~255         | RW  | Key input parameters/general registers                                    |
| R0~R3          | 0~4294967295  | RW  | General registers                                                         |
| A              | 0~4294967295  | RW  | Accumulator/general register                                              |
| B              | 0~4294967295  | RW  | Division register/general register                                        |
| DPTR           | 0~4294967295  | RW  | General register                                                          |
| P_R0~P_R3      | ?             | RW  | Shared RAM memory area pointers                                           |
| P_DPTR         | ?             | RO  | Data pointer                                                              |
| ZERO           | 0             | RO  | Always reads as 0                                                         |
| IO             | 0~255         | RO  | IO status, 0=pressed                                                      |
| SYS_TIME_MS    | 0~999         | RO  | System time, milliseconds                                                 |
| SYS_TIME       | 0~4294967295  | RO  | System time, seconds                                                      |
| SYS_KB_LED     | 0~255         | RW  | Keyboard LED status. R: Read current status. W: Modify status, requires 2 operations to ensure key release |
| SYS_KEY_NUM    | 0~4294967295  | RO  | Key count                                                                 |
| SYS_KEY_LAY    | 0~255         | RW  | Keyboard layer                                                            |
| S_SCRIPT_ADDR  | 0~4294967295  | RO  | Current script step address                                               |
| S_DATA_RANDOM  | 0~4294967295  | RW  | R: Get a random number W: Set random number seed                          |
| SYS_BLE_NUM    | 0~7           | WO  | Bluetooth multi-device switch, immediately restarts and switches after writing |
| S_SELECTED_LED | 0~x           | RW  | Selected LED for operation. Default is the LED of the executing key       |
| GL0~GL127      | 0~4294967295  | RW  | Global general registers, default values unknown, clear before use        |

## **6. Operation Commands**

### Key Operation Commands

- Supports various operations including keyboard, mouse, multimedia, etc.
- Commands support both direct values and parameters
- Supports press and release controls, allowing for nested/out-of-order operations, but press operations must have corresponding release operations
- Add at least 1ms delay after each operation to allow the host to receive the operation

```
- Modifier Keys
- General Keys
- Mouse Keys
- Multimedia Keys
- Joystick Buttons
- Mouse Cursor Movement
- Mouse Cursor Positioning
```

## **7. Jump Commands**

Scripts support flow control (jumps), allowing internal jumps or jumps to the next script.
Currently supported jump commands include:

```
JZ              //jump if (REG == 0)  Jump if parameter value is 0, otherwise continue
JNZ             //jump if (REG != 0)  Jump if parameter value is not 0, otherwise continue
JC              //jump if (CY == 0)   Jump if parameter CY value is 0, otherwise continue
JNC             //jump (if CY != 0)   Jump if parameter CY value is not 0, otherwise continue
CJNE            //CY = (REG1 < REG2);jump if (REG1 != REG2)  Set CY if REG1 < REG2, otherwise clear; jump if not equal, otherwise continue
DJNZ            //jump if (--REG != 0)  REG decrements first, jump if not zero, otherwise continue
```

For easier use, SET_FLAG can write the target address to a register, then JUMP_TO_FLAG can jump directly to the address stored in the register without calculating the address.

- Examples:
  · Short press outputs A, long press outputs B  
  ![](https://dl.sayobot.cn/script/%E8%84%9A%E6%9C%AC%E4%BE%8B%E5%AD%90/短按A长按B.png)  
  Explanation: When a key is pressed, the script starts, then waits 200 milliseconds before checking the key state again (IO is the key state, pressed is 0). If still pressed, it's recognized as a long press and jumps to the address saved in (R0) to output B. Otherwise, it continues to output A and exits.  
  Note that even though (R0) is not assigned a value here, its default value is 0, and the program will automatically search forward until it finds SET_FLAG.

- Local Loop  
  ![](https://dl.sayobot.cn/script/%E8%84%9A%E6%9C%AC%E4%BE%8B%E5%AD%90/局部循环.png)  
  The count parameter can also be passed through the key

## **8. Arithmetic Commands**

To be completed in a future update.

## **9. Parameter Specifications**

- Script names can be used to specify parameter types

| Symbol    | Usage                   | Format                           | Notes                                                                                      |
| --------- | ----------------------- | -------------------------------- | ------------------------------------------------------------------------------------------ |
| ~         | Parameter end           | ~                                | The script name (mode name) follows the end                                                |
| \\        | Parameter type specifier| \\a\\b\\c\\d~                    | Only interprets one letter (if script name doesn't start with "\\", "{" or "~", parameters are parsed as "\\u\\u\\u\\u~" by default) |
|           | Parameter name          | \\m Modifier key\\g General key~ | The parameter name follows the letter                                                      |
| -         | Custom option (single)  | \\U Switch-0 On-1 Off~           | -value+option name                                                                         |
| =         | Custom option (multiple)| \\U Mouse key=1 Left=2 Right=4 Middle~ |                                                                                      |
| {}        | Collection              | {\\m\\g}Short press{\\m\\g}Long press~ |                                                                                      |
| --------- | ------                  | ----------                       | ---                                                                                        |
| \\u       | Unsigned number 0~255   |                                  |                                                                                            |
| \\s       | Signed number -128~127  |                                  |                                                                                            |
| \\\\u     | Unsigned number 0~65535 |                                  |                                                                                            |
| \\\\s     | Signed number -32768~32767 |                               |                                                                                            |
| \\\\\\u   | Same as above           |                                  |                                                                                            |
| \\\\\\s   | Same as above           |                                  |                                                                                            |
| \\m       | Modifier keys           |                                  |                                                                                            |
| \\g       | General keys            |                                  |                                                                                            |
| \\M       | Mouse keys              |                                  |                                                                                            |
| \\c       | Multimedia keys         |                                  |                                                                                            |
| \\j       | Joystick buttons        |                                  |                                                                                            |
| \\a       | Joystick axes           |                                  |                                                                                            |
| \\P       | Password                |                                  |                                                                                            |
| \\S       | String                  |                                  |                                                                                            |
| \\A       | Keyboard indicators (Numlock etc.) |                       |                                                                                            |
| \\L       | Key layer               |                                  |                                                                                            |
| \\U       | User-defined options    |                                  |                                                                                            |

## **Command Reference Table**

!> Default is little-endian unless specifically noted

| Code | Mnemonic         | Length | Format                      | Method                                                                                     |
| ---- | ---------------- | ------ | --------------------------- | ------------------------------------------------------------------------------------------ |
| 0x00 |                  |        |                             |                                                                                            |
| 0x01 | NOP              | 1      | NOP                         | No operation                                                                               |
| 0x02 | JMP              | 3      | JMP addr16(BIG ENDIAN)      | PC=addr                                                                                    |
| 0x03 | SJMP             | 2      | SJMP rel(-128~+127)         | PC=PC+2+rel                                                                                |
| 0x04 |                  |        |                             |                                                                                            |
| 0x05 | SLEEP_X256       | 2      | SLEEP_X256 data8            | Sleep data*256 ms                                                                          |
| 0x06 | SLEEP            | 2      | SLEEP data8                 | Sleep data*1 ms                                                                           |
| 0x07 | SLEEP_RAND_X256  | 2      | SLEEP_RAND_X256 data8       | Sleep random() % (data*256) ms                                                            |
| 0x08 | SLEEP_RAND       | 2      | SLEEP_RAND data8            | Sleep random() % (data*1) ms                                                              |
| 0x09 | SLEEP_X256_VAL   | 2      | SLEEP_X256_VAL REG          | Sleep REG*256 ms                                                                          |
| 0x0A | SLEEP_VAL        | 2      | SLEEP_VAL REG               | Sleep REG*1 ms                                                                            |
| 0x0B | SLEEP_RAND_X8_VAL| 2      | SLEEP_X8_VAL REG            | Sleep random() % (REG*8) ms                                                               |
| 0x0C | SLEEP_RAND_VAL   | 2      | SLEEP_VAL REG               | Sleep random() % (REG*1) ms                                                               |
| 0X0D | SLEEP_U16        | 2      | SLEEP_U16 data16            | Sleep data*1ms                                                                            |
| 0x0E | SLEEP_RAND_U16   | 2      | SLEEP_RAND_U16 data16       | Sleep random() % (data*1) ms                                                              |
| 0x0F |                  |        |                             |                                                                                            |
| 0X10 | S_SK             | 2      | S_SK keyboard_modifier_keys | Send press key(s) [data value](https://manual.sayodevice.com/format/modifier_keys.json)    |
| 0X11 | S_GK             | 2      | S_GK keyboard_general_keys  | Send press a key [data value](https://manual.sayodevice.com/format/general_keys.json)      |
| 0X12 | S_MK             | 2      | S_MK mouse_keys             | Send press key(s) [data value](https://manual.sayodevice.com/format/mouse_keys.json)       |
| 0X13 | S_MU             | 2      | S_MU multimedia_keys        | Send press key(s) [data value](https://manual.sayodevice.com/format/mu_keys.json)          |
| 0X14 | S_SK_VAL         | 2      | S_SK_VAL REG                | Send press key(s) [data value](https://manual.sayodevice.com/format/modifier_keys.json)    |
| 0X15 | S_GK_VAL         | 2      | S_GK_VAL REG                | Send press a key [data value](https://manual.sayodevice.com/format/general_keys.json)      |
| 0X16 | S_MK_VAL         | 2      | S_MK_VAL REG                | Send press key(s) [data value](https://manual.sayodevice.com/format/mouse_keys.json)       |
| 0X17 | S_MU_VAL         | 2      | S_MU_VAL REG                | Send press key(s) [data value](https://manual.sayodevice.com/format/mu_keys.json)          |
| 0X18 | S_USK            | 2      | S_USK keyboard_modifier_keys| Send release key(s) [data value](https://manual.sayodevice.com/format/modifier_keys.json)  |
| 0X19 | S_UGK            | 2      | S_UGK keyboard_general_keys | Send release a key [data value](https://manual.sayodevice.com/format/general_keys.json)    |
| 0X1A | S_UMK            | 2      | S_UMK mouse_keys            | Send release key(s) [data value](https://manual.sayodevice.com/format/mouse_keys.json)     |
| 0X1B | S_UMU            | 2      | S_UMU multimedia_keys       | Send release key(s) [data value](https://manual.sayodevice.com/format/mu_keys.json)        |
| 0X1C | S_USK_VAL        | 2      | S_USK_VAL REG               | Send release key(s) [data value](https://manual.sayodevice.com/format/modifier_keys.json)  |
| 0X1D | S_UGK_VAL        | 2      | S_UGK_VAL REG               | Send release a key [data value](https://manual.sayodevice.com/format/general_keys.json)    |
| 0X1E | S_UMK_VAL        | 2      | S_UMK_VAL REG               | Send release key(s) [data value](https://manual.sayodevice.com/format/mouse_keys.json)     |
| 0X1F | S_UMU_VAL        | 2      | S_UMU_VAL REG               | Send release key(s) [data value](https://manual.sayodevice.com/format/mu_keys.json)        |
| 0x20 |                  |        |                             |                                                                                            |
| 0x21 | S_MO_DATA        | 3      | S_MO_DATA index data8       | Send mouse data (index 0=X 1=Y 2=Scroll)                                                   |
| 0x22 | S_MO_VAL         | 3      | S_MO_VAL index REG          | Send mouse data (index 0=X 1=Y 2=Scroll)                                                   |
| 0x23 | S_JOY_AXIS       | 4      | S_JOY_AXIS index data16     | Send controller data (index 0=X 1=Y 2=rX 3=rY 4=Z 5=rZ)                                    |
| 0x24 | S_JOY_AXIS_VAL   | 3      | S_JOY_AXIS_VAL index REG    | Send controller data (index 0=X 1=Y 2=rX 3=rY 4=Z 5=rZ)                                    |
| 0X25 | S_CURSOR         | 5      | S_CURSOR data16 data16      | Send move mouse cursor to X Y                                                              |
| 0X26 | S_CURSOR_VAL     | 5      | S_CURSOR_VAL REG REG        | Send move mouse cursor to X Y                                                              |
| 0X27 | S_DIAL           | 2      | S_DIAL data8                | Send DIAL data (0=release 1=press 2=clockwise rotation 3=Anticlockwise rotation)           |
| 0X28 | S_DIAL_VAL       | 2      | S_DIAL REG                  | Send DIAL data (0=release 1=press 2=clockwise rotation 3=Anticlockwise rotation)           |
| 0X29 |                  |        |                             |                                                                                            |
| 0X2A |                  |        |                             |                                                                                            |
| 0X2B |                  |        |                             |                                                                                            |
| 0X2C | S_JK             | 2      | S_JK data8                  | Joystick key number (0~127)                                                                |
| 0X2D | S_JK_VAL         | 2      | S_JK_VAL REG                | Joystick key number (0~127)                                                                |
| 0X2E | S_UJK            | 2      | S_UJK data8                 | Joystick key number (0~127)                                                                |
| 0X2F | S_UJK_VAL        | 2      | S_UJK_VAL REG               | Joystick key number (0~127)                                                                |
