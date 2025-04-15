# Device Script Documentation

## 1. Overview

### 1.1 Design Purpose
The program runs on a programmable keyboard that uses scripts to perform operations including but not limited to:
- Automating keyboard/mouse operations
- Controlling LED lighting effects
- Complex logic operations (conditional jumps, loops, etc.)

### 1.2 Architecture Features
- Variable instruction length
- Each key has four 8-bit parameters passed when triggered (can also be used as general registers)
- 16x32-bit thread-specific general registers (support indirect addressing via pointers)
- Minimum 4 global registers (shared between threads)
- Multi-threading support

### 1.3 Core Specifications
- Program code space: 4KB (device-dependent, ranges from 256B to 64KB)
- Limited RAM usage - minimum 128B. Prioritize register storage.

<details>
<summary>Register List</summary>

| Name               | Bit Width | R/W | Description                                                                                     |
|--------------------|-----------|-----|-------------------------------------------------------------------------------------------------|
| V0                 | 8         | RW  | Key input parameter / General-purpose register                                                 |
| V1                 | 8         | RW  | Key input parameter / General-purpose register                                                 |
| V2                 | 8         | RW  | Key input parameter / General-purpose register                                                 |
| V3                 | 8         | RW  | Key input parameter / General-purpose register                                                 |
| R0                 | 32        | RW  | General-purpose register                                                                      |
| R1                 | 32        | RW  | General-purpose register                                                                      |
| R2                 | 32        | RW  | General-purpose register                                                                      |
| R3                 | 32        | RW  | General-purpose register                                                                      |
| *DPTR              | 8         | R   | ROM addressing专用寄存器，mapped to R4，shared address space                                   |
| DPTR               | 32        | RW  | Mapped to R4                                                                                  |
| KEY_IO             | 8         | R   | 0=pressed                                                                                     |
| *R0                | 8         | RW  | Use R0 for RAM addressing                                                                     |
| *R1                | 8         | RW  | Use R1 for RAM addressing                                                                     |
| *R2                | 8         | RW  | Use R2 for RAM addressing                                                                     |
| *R3                | 8         | RW  | Use R3 for RAM addressing                                                                     |
| ZERO               | 8         | R   | Always reads 0                                                                                |
| A                  | 32        | RW  | Dedicated register. Mapped to R6，shared address space. Can reduce code length in some instructions |
| B                  | 32        | RW  | Dedicated register. Mapped to R7，shared address space. Can reduce code length in some instructions |
| SYS_TIME_MS        | 16        | R   | System time in milliseconds. Valid range: 0~999                                               |
| SYS_TIME_S         | 32        | R   | System time in seconds                                                                        |
| SYS_KBLED          | 8         | RW  | Keyboard LED status (Num Lock, Caps Lock, Scroll Lock, etc.). R: Read current status. W: Modify status (auto-sends keyboard commands). Requires two consecutive operations to ensure key release. |
| SYS_KEY_COUNT      | 32        | R   | System physical key press count                                                               |
| SYS_KEY_LAY        | 8         | RW  | Keyboard layer. A keyboard may have multiple key mapping layers                                |
| SCRIPT_ADDR        | 32        | R   | Script starting address                                                                       |
| RANDOM             | 32        | RW  | R: Get random number W: Set random seed                                                       |
| SYS_BLE_NUM        | 8         | RW  | Bluetooth multi-device switching                                                              |
| SYS_VOLUME         | 8         | RW  | Absolute system volume (currently ineffective on Windows systems)                             |
| SELECTED_LED       | 8         | RW  | Selected LED for operation. Defaults to the LED associated with the pressed key                |
| SELECTED_LED_COL   | 24        | RW  | Modify selected LED color (RGB888)                                                            |
| ALL_LED_COL        | 24        | RW  | Modify all LED colors (RGB888)                                                                |
| CFG_ADDR           | 32        | R   | Get current configuration file address                                                        |
| HE_KEY_LV          | 32        | RW  | Hall effect key actuation depth in microns (μm). R: Get current key W: Get target key (value will be pushed to stack, use POP instruction to retrieve) |
| R4                 | 32        | RW  | General-purpose register                                                                      |
| R5                 | 32        | RW  | General-purpose register                                                                      |
| R6                 | 32        | RW  | General-purpose register                                                                      |
| R7                 | 32        | RW  | General-purpose register                                                                      |
| R8                 | 32        | RW  | General-purpose register                                                                      |
| R9                 | 32        | RW  | General-purpose register                                                                      |
| R10                | 32        | RW  | General-purpose register                                                                      |
| R11                | 32        | RW  | General-purpose register                                                                      |
| R12                | 32        | RW  | General-purpose register                                                                      |
| R13                | 32        | RW  | General-purpose register                                                                      |
| R14                | 32        | RW  | General-purpose register                                                                      |
| R15                | 32        | RW  | General-purpose register                                                                      |
| *R4                | 8         | RW  | Use R4 for RAM addressing                                                                     |
| *R5                | 8         | RW  | Use R5 for RAM addressing                                                                     |
| *R6                | 8         | RW  | Use R6 for RAM addressing                                                                     |
| *R7                | 8         | RW  | Use R7 for RAM addressing                                                                     |
| *R0_16b            | 16        | RW  |                                                                                               |
| *R1_16b            | 16        | RW  |                                                                                               |
| *R2_16b            | 16        | RW  |                                                                                               |
| *R3_16b            | 16        | RW  |                                                                                               |
| *R4_16b            | 16        | RW  |                                                                                               |
| *R5_16b            | 16        | RW  |                                                                                               |
| *R6_16b            | 16        | RW  |                                                                                               |
| *R7_16b            | 16        | RW  |                                                                                               |
| *R0_32b            | 32        | RW  |                                                                                               |
| *R1_32b            | 32        | RW  |                                                                                               |
| *R2_32b            | 32        | RW  |                                                                                               |
| *R3_32b            | 32        | RW  |                                                                                               |
| *R4_32b            | 32        | RW  |                                                                                               |
| *R5_32b            | 32        | RW  |                                                                                               |
| *R6_32b            | 32        | RW  |                                                                                               |
| *R7_32b            | 32        | RW  |                                                                                               |
| GL_SIZE            |           |     | Number of GL registers (minimum 4, maximum 64)                                                |
| GL_0               | 32        |     | General global register                                                                       |
| GL_1               | 32        |     | General global register                                                                       |
| GL_2               | 32        |     | General global register                                                                       |
| GL_3               | 32        |     | General global register                                                                       |
| ...                | 32        |     | General global register                                                                       |

</details>

### 1.4 Script Execution  
- Normally, keyboard keys act as script triggers. Pressing a key will execute the corresponding script.  
- When a script is executed, the 4 optional parameters set for the key will be passed to the script's registers.  
- Scripts execute sequentially from top to bottom, performing corresponding instruction operations.  
- A script will continue executing indefinitely until encountering a **delay**, **wait**, or **exit** instruction.  
- After execution starts, scripts default to **toggle mode** (press once to start execution, press again to force termination and release keys). To detect double-click operations, first switch to **momentary mode**.  

### 1.5 Sending Key Operations  
- Output basic key operations to the host (typically a PC).  
- If key operations are sent, a delay must be added before releasing the key; otherwise, the host may not receive the operation.  
- The fundamental 4-step process: Press → Delay → Release → Delay (the final delay may be omitted if the next instruction after delay is an exit).  
- Delay unit: milliseconds (ms), where 1 second = 1000 ms.  
- Minimum delay: 1 ms. Recommended minimum: 5 ms. Excessively fast operations may cause host processing failures.  
- Typical human key press duration exceeds 30 ms. Default recommended value: 35 ms.  
- Delays must be added between consecutive key operations.  
- Supports press/release operations and nested operations (simultaneous pressing of multiple keys).  
- **Keys must be released before script termination, otherwise they will remain in a pressed state!!!**  

## 2. Instruction Structure  

```  
[Opcode] [Operand1] [Operand2] [Operand3]  
```  
- Opcode is fixed at 8 bits  
- Variable instruction length: Minimum 1 byte, maximum 6 bytes  
- Zero or more operands (registers or immediate values), see specific instruction descriptions  
- Unless otherwise specified, data is in **little-endian** format  
- Each operand occupies at least 1 byte:  
  - Registers: 1 byte  
  - 16-bit immediate: 2 bytes  
  - 24-bit immediate: 3 bytes  
  - 32-bit immediate: 4 bytes  
- Operand types:  
```  
label    // Jump target label (or unsigned 16-bit big-endian immediate value)  
i8       // Signed 8-bit little-endian immediate  
u8       // Unsigned 8-bit little-endian immediate  
i16      // Signed 16-bit little-endian immediate  
u16      // Unsigned 16-bit little-endian immediate  
i32      // Signed 32-bit little-endian immediate  
u32      // Unsigned 32-bit little-endian immediate  
reg      // Register  
RGB888   // 24-bit color data  
```  

## 3. Instruction List  
<details>  
<summary>Full Instruction Set</summary>  

| 助记符               | 操作码 | 操作码（HEX） | 指令长度 | 操作数 i  | 操作数 j | 操作数 k | 作用                                         | 备注                                                                                                |
|-------------------|-----|----------|------|--------|-------|-------|--------------------------------------------|---------------------------------------------------------------------------------------------------|
| END               | 0   | 0x0      | 1    | -      | -     | -     | 程序结束                                       |                                                                                                   |
| NOP               | 1   | 0x1      | 1    | -      | -     | -     | 空操作                                        |                                                                                                   |
| JMP               | 2   | 0x2      | 3    | label  | -     | -     | PC = i;                                    | 长跳转                                                                                               |
| SJMP              | 3   | 0x3      | 2    | i8     | -     | -     | PC = PC + i;                               | 短跳转，偏移量                                                                                           |
| AJMP              | 4   | 0x4      | 2    | u8     | -     | -     | PC = (PC & 0xff00) + i;                    | 在地址的256B范围内跳转                                                                                     |
| SLEEP_X256        | 5   | 0x5      | 2    | u8     | -     | -     | Sleep(i * 256);                            | 延时范围0-65280ms（256倍率）                                                                              |
| SLEEP             | 6   | 0x6      | 2    | u8     | -     | -     | Sleep(i * 1);                              | 延时范围0-255ms                                                                                       |
| SLEEP_RAND_X256   | 7   | 0x7      | 2    | u8     | -     | -     | Sleep(rand()%(i * 256)+1);                 | 随机延时范围1-65281ms（256倍率）                                                                            |
| SLEEP_RAND        | 8   | 0x8      | 2    | u8     | -     | -     | Sleep(rand()%i+1);                         | 随机延时范围1-256ms                                                                                     |
| SLEEP_X256_VAL    | 9   | 0x9      | 2    | reg    | -     | -     | Sleep(i * 256);                            | 延时的寄存器版本，范围取决于寄存器（256倍率）                                                                          |
| SLEEP_VAL         | 10  | 0x0A     | 2    | reg    | -     | -     | Sleep(i);                                  | 延时的寄存器版本，范围取决于寄存器                                                                                 |
| SLEEP_RAND_X8_VAL | 11  | 0x0B     | 2    | reg    | -     | -     | Sleep(rand()%(i * 8)+1);                   | 随机延时的寄存器版本，范围取决于寄存器（8倍率）                                                                          |
| SLEEP_RAND_VAL    | 12  | 0x0C     | 2    | reg    | -     | -     | Sleep(rand()%i+1);                         | 随机延时的寄存器版本，范围取决于寄存器                                                                               |
| SLEEP_U16         | 13  | 0x0D     | 3    | u16    | -     | -     | Sleep(i);                                  | 延时范围1-65536ms                                                                                     |
| SLEEP_RAND_U16    | 14  | 0x0E     | 3    | u16    | -     | -     | Sleep(rand()%i+1);                         | 延时范围1-65536ms                                                                                     |
| PRESS_SK          | 16  | 0x10     | 2    | u8     | -     | -     | 键盘 修饰键 i 按下                                | HID键码                                                                                             |
| PRESS_GK          | 17  | 0x11     | 2    | u8     | -     | -     | 键盘 普通键 i 按下                                | HID键码                                                                                             |
| PRESS_MK          | 18  | 0x12     | 2    | u8     | -     | -     | 鼠标 鼠标键 i 按下                                | HID键码                                                                                             |
| PRESS_MU          | 19  | 0x13     | 2    | u8     | -     | -     | 按键 多媒体 i 按下                                | HID键码                                                                                             |
| PRESS_SK_VAL      | 20  | 0x14     | 2    | reg    | -     | -     | 键盘 修饰键 i 按下                                | HID键码                                                                                             |
| PRESS_GK_VAL      | 21  | 0x15     | 2    | reg    | -     | -     | 键盘 普通键 i 按下                                | HID键码                                                                                             |
| PRESS_MK_VAL      | 22  | 0x16     | 2    | reg    | -     | -     | 鼠标 鼠标键 i 按下                                | HID键码                                                                                             |
| PRESS_MU_VAL      | 23  | 0x17     | 2    | reg    | -     | -     | 按键 多媒体 i 按下                                | HID键码                                                                                             |
| RELEASE_SK        | 24  | 0x18     | 2    | u8     | -     | -     | 键盘 修饰键 i 释放                                | HID键码                                                                                             |
| RELEASE_GK        | 25  | 0x19     | 2    | u8     | -     | -     | 键盘 普通键 i 释放                                | HID键码                                                                                             |
| RELEASE_MK        | 26  | 0x1A     | 2    | u8     | -     | -     | 鼠标 鼠标键 i 释放                                | HID键码                                                                                             |
| RELEASE_MU        | 27  | 0x1B     | 2    | u8     | -     | -     | 按键 多媒体 i 释放                                | HID键码                                                                                             |
| RELEASE_SK_VAL    | 28  | 0x1C     | 2    | reg    | -     | -     | 键盘 修饰键 i 释放                                | HID键码                                                                                             |
| RELEASE_GK_VAL    | 29  | 0x1D     | 2    | reg    | -     | -     | 键盘 普通键 i 释放                                | HID键码                                                                                             |
| RELEASE_MK_VAL    | 30  | 0x1E     | 2    | reg    | -     | -     | 鼠标 鼠标键 i 释放                                | HID键码                                                                                             |
| RELEASE_MU_VAL    | 31  | 0x1F     | 2    | reg    | -     | -     | 按键 多媒体 i 释放                                | HID键码                                                                                             |
| UPDATE            | 32  | 0x20     | 1    | -      | -     | -     | HID数据包强制重传(一般不会使用)                         |                                                                                                   |
| MO_XYZ            | 33  | 0x21     | 3    | u8     | i8    | -     | 鼠标 光标移动 axis=i data=j                      | 0: x, 1:y, 2:scroll                                                                               |
| MO_XYZ_VAL        | 34  | 0x22     | 3    | u8     | reg   | -     | 鼠标 光标移动 axis=i data=j                      |                                                                                                   |
| GA_XYZ            | 35  | 0x23     | 4    | u8     | u16   | -     | joystick axis=i data=j                     |                                                                                                   |
| GA_XYZ_VAL        | 36  | 0x24     | 3    | u8     | reg   | -     | joystick axis=i data=j                     |                                                                                                   |
| TB_XY             | 37  | 0x25     | 5    | i16    | i16   | -     | 鼠标 光标定位 x=i y=j                            |                                                                                                   |
| TB_XY_VAL         | 38  | 0x26     | 3    | reg    | reg   | -     | 鼠标 光标定位 x=i y=j                            |                                                                                                   |
| DIAL_DATA         | 39  | 0x27     | 2    | u8     | -     | -     | Dial data=i                                | data:0=release 1=press 2=cw 3=ccw                                                                 |
| DIAL_DATA_VAL     | 40  | 0x28     | 2    | reg    | -     | -     | Dial data=i                                | data:0=release 1=press 2=cw 3=ccw                                                                 |
| KEY_TO_AXIS       | 41  | 0x29     | 1    | -      | -     | -     | joystick axis=reg::val[0] type=reg::val[1] | 内部使用                                                                                              |
| PRESS_GAK         | 44  | 0x2C     | 2    | u8     | -     | -     | joystick 按键 i 按下                           |                                                                                                   |
| PRESS_GAK_VAL     | 45  | 0x2D     | 2    | reg    | -     | -     | joystick 按键 i 按下                           |                                                                                                   |
| RELEASE_GAK       | 46  | 0x2E     | 2    | u8     | -     | -     | joystick 按键 i 释放                           |                                                                                                   |
| RELEASE_GAK_VAL   | 47  | 0x2F     | 2    | reg    | -     | -     | joystick 按键 i 释放                           |                                                                                                   |
| C2K               | 48  | 0x30     | 1    | -      | -     | -     | print ascii character                      | 内部使用                                                                                              |
| U2K               | 49  | 0x31     | 1    | -      | -     | -     | print unicode character                    | 内部使用                                                                                              |
| C2K_RAND          | 50  | 0x32     | 1    | -      | -     | -     | print random ascii character               | 内部使用                                                                                              |
| U2K_REG           | 51  | 0x33     | 1    | -      | -     | -     | print value                                | 内部使用，需要循环调用直到输出完毕                                                                                 |
| PRINT_REG         | 52  | 0x34     | 2    | reg    | -     | -     | print value                                | 打印寄存器值，只需要执行一次即可完整输出                                                                              |
| JFA               | 64  | 0x40     | 4    | reg    | reg   | reg   | if (i>j)PC=k;                              | 比较两个寄存器的值(无符号数)，根据结果判断是否跳转，目标地址存储于寄存器                                                             |
| JFB               | 65  | 0x41     | 4    | reg    | reg   | reg   | if (i<j)PC=k;                              | 比较两个寄存器的值(无符号数)，根据结果判断是否跳转，目标地址存储于寄存器                                                             |
| JFG               | 66  | 0x42     | 4    | reg    | reg   | reg   | if (i>j)PC=k;                              | 比较两个寄存器的值(无符号数)，根据结果判断是否跳转，目标地址存储于寄存器                                                             |
| JFL               | 67  | 0x43     | 4    | reg    | reg   | reg   | if (i<j)PC=k;                              | 比较两个寄存器的值(无符号数)，根据结果判断是否跳转，目标地址存储于寄存器                                                             |
| JA                | 68  | 0x44     | 5    | reg    | reg   | label | if (i>j)PC=k;                              | 比较两个寄存器的值(有符号数)，根据结果判断是否跳转，目标地址为label                                                             |
| JB                | 69  | 0x45     | 5    | reg    | reg   | label | if (i<j)PC=k;                              | 比较两个寄存器的值(有符号数)，根据结果判断是否跳转，目标地址为label                                                             |
| JG                | 70  | 0x46     | 5    | reg    | reg   | label | if (i>j)PC=k;                              | 比较两个寄存器的值(有符号数)，根据结果判断是否跳转，目标地址为label                                                             |
| JL                | 71  | 0x47     | 5    | reg    | reg   | label | if (i<j)PC=k;                              | 比较两个寄存器的值(有符号数)，根据结果判断是否跳转，目标地址为label                                                             |
| JFC               | 72  | 0x48     | 2    | reg    | -     | -     | if (CY) PC = i;                            | 如果CY置位，则跳转。目标地址存储于寄存器                                                                             |
| JFNC              | 73  | 0x49     | 2    | reg    | -     | -     | if (!CY) PC = i;                           | 如果CY没有置位，则跳转。目标地址存储于寄存器                                                                           |
| JFZ               | 74  | 0x4A     | 3    | reg    | reg   | -     | if (!i) PC = j;                            | 寄存器为0跳转。目标地址存储于寄存器                                                                                |
| JFNZ              | 75  | 0x4B     | 3    | reg    | -     | -     | if (i) PC = j;                             | 寄存器不为0跳转。目标地址存储于寄存器                                                                               |
| DJFNZ             | 76  | 0x4C     | 3    | reg    | reg   | -     | if (--i) PC = j;                           | 寄存器减1并存回，寄存器不为0跳转。目标地址存储于寄存器                                                                      |
| CJFNE             | 77  | 0x4D     | 4    | reg    | reg   | reg   | if (i != j) {CY = i<j;PC = k}              | 比较两个寄存器并设置CY标识，不相等则跳转。目标地址存储于寄存器                                                                  |
| JC                | 78  | 0x4E     | 3    | label  | -     | -     | if (CY) PC = i;                            | 如果CY置位，则跳转。目标地址为label                                                                             |
| JNC               | 79  | 0x4F     | 3    | label  | -     | -     | if (!CY) PC = i;                           | 如果CY没有置位，则跳转。目标地址为label                                                                           |
| JZ                | 80  | 0x50     | 4    | reg    | label | -     | if (!i) PC = j;                            | 寄存器为0跳转。目标地址为label                                                                                |
| JNZ               | 81  | 0x51     | 4    | reg    | label | -     | if (i) PC = j;                             | 寄存器不为0跳转。目标地址为label                                                                               |
| DJNZ              | 82  | 0x52     | 4    | reg    | label | -     | if (--i) PC = j;                           | 寄存器减1并存回，寄存器不为0跳转。目标地址为label                                                                      |
| CJNE              | 83  | 0x53     | 5    | reg    | reg   | label | if (i != j) {CY = i<j;PC = k}              | 比较两个寄存器并设置CY标识，不相等则跳转。目标地址为label                                                                  |
| CALL              | 84  | 0x54     | 3    | label  | -     | -     | PUSH PC;PC=i;                              | 调用子程序，目标地址为label                                                                                  |
| RET               | 85  | 0x55     | 1    | -      | -     | -     | POP PC;                                    | 子程序返回                                                                                             |
| AND               | 86  | 0x56     | 3    | reg    | reg   | -     | i=i&j;                                     |                                                                                                   |
| AND8              | 87  | 0x57     | 3    | reg    | u8    | -     | i=i&j;                                     |                                                                                                   |
| ADD_A             | 88  | 0x58     | 2    | reg    | -     | -     | A = A + i;                                 |                                                                                                   |
| ADD8_A            | 89  | 0x59     | 2    | u8     | -     | -     | A = A + i;                                 |                                                                                                   |
| SUB_A             | 90  | 0x5A     | 2    | reg    | -     | -     | A = A - i;                                 |                                                                                                   |
| SUB8_A            | 91  | 0x5B     | 2    | u8     | -     | -     | A = A - i;                                 |                                                                                                   |
| OR_A              | 92  | 0x5C     | 2    | reg    | -     | -     | A = A | i;                                 |                                                                                                   |
| OR8_A             | 93  | 0x5D     | 2    | u8     | -     | -     | A = A | i;                                 |                                                                                                   |
| DEC               | 94  | 0x5E     | 2    | reg    | -     | -     | i--;                                       |                                                                                                   |
| INC               | 95  | 0x5F     | 2    | reg    | -     | -     | i++;                                       |                                                                                                   |
| MUL_A             | 96  | 0x60     | 1    | -      | -     | -     | A = A * B;                                 |                                                                                                   |
| DIV_A             | 97  | 0x61     | 1    | -      | -     | -     | A = A / B;B = A % B;                       |                                                                                                   |
| XOR               | 98  | 0x62     | 3    | reg    | reg   | -     | i=i^j;                                     |                                                                                                   |
| XOR8              | 99  | 0x63     | 3    | reg    | u8    | -     | i=i^j;                                     |                                                                                                   |
| SHL               | 100 | 0x64     | 3    | reg    | reg   | -     | i=i<<j;                                    |                                                                                                   |
| SHL8              | 101 | 0x65     | 3    | reg    | u8    | -     | i=i<<j;                                    |                                                                                                   |
| SHR               | 102 | 0x66     | 3    | reg    | reg   | -     | i=i>>j;                                    |                                                                                                   |
| SHR8              | 103 | 0x67     | 3    | reg    | u8    | -     | i=i>>j;                                    |                                                                                                   |
| CLR               | 104 | 0x68     | 2    | reg    | -     | -     | i=0;                                       | 寄存器清理                                                                                             |
| NOT               | 105 | 0x69     | 2    | reg    | -     | -     | i=~i;                                      | 寄存器按位取反                                                                                           |
| XCH               | 106 | 0x6A     | 3    | reg    | reg   | -     | i<==>j;                                    | ij交换                                                                                              |
| CMP               | 107 | 0x6B     | 3    | reg    | reg   | -     | CY=i<j;                                    | 比较两个寄存器并设置CY标识（目前本指令没有的必要）                                                                        |
| PUSH              | 108 | 0x6C     | 2    | reg    | -     | -     |                                            | 压栈                                                                                                |
| POP               | 109 | 0x6D     | 2    | reg    | -     | -     |                                            | 出栈                                                                                                |
| MOV               | 110 | 0x6E     | 3    | reg    | reg   | -     | i=j;                                       |                                                                                                   |
| MOV8              | 111 | 0x6F     | 3    | reg    | u8    | -     | i=j;                                       |                                                                                                   |
| MOV16             | 112 | 0x70     | 4    | reg    | u16   | -     | i=j;                                       |                                                                                                   |
| MOV32             | 113 | 0x71     | 6    | reg    | u32   | -     | i=j;                                       |                                                                                                   |
| ADD               | 114 | 0x72     | 3    | reg    | reg   | -     | i=i+j;                                     |                                                                                                   |
| ADD8              | 115 | 0x73     | 3    | reg    | u8    | -     | i=i+j;                                     |                                                                                                   |
| ADD16             | 116 | 0x74     | 4    | reg    | u16   | -     | i=i+j;                                     |                                                                                                   |
| SUB               | 117 | 0x75     | 3    | reg    | reg   | -     | i=i-j;                                     |                                                                                                   |
| SUB8              | 118 | 0x76     | 3    | reg    | u8    | -     | i=i-j;                                     |                                                                                                   |
| SUB16             | 119 | 0x77     | 4    | reg    | u16   | -     | i=i-j;                                     |                                                                                                   |
| OR                | 120 | 0x78     | 3    | reg    | reg   | -     | i=i|j;                                     |                                                                                                   |
| OR8               | 121 | 0x79     | 3    | reg    | u8    | -     | i=i|j;                                     |                                                                                                   |
| AND16             | 122 | 0x7A     | 4    | reg    | u16   | -     | i=i&j;                                     |                                                                                                   |
| OR16              | 123 | 0x7B     | 4    | reg    | u16   | -     | i=i|j;                                     |                                                                                                   |
| XOR16             | 124 | 0x7C     | 4    | reg    | u16   | -     | i=i^j;                                     |                                                                                                   |
| ADD32             | 125 | 0x7D     | 6    | reg    | u32   | -     | i=i+j;                                     |                                                                                                   |
| SUB32             | 126 | 0x7E     | 6    | reg    | u32   | -     | i=i-j;                                     |                                                                                                   |
| AND32             | 127 | 0x7F     | 6    | reg    | u32   | -     | i=i&j;                                     |                                                                                                   |
| OR32              | 128 | 0x80     | 6    | reg    | u32   | -     | i=i|j;                                     |                                                                                                   |
| XOR32             | 129 | 0x81     | 6    | reg    | u32   | -     | i=i^j;                                     |                                                                                                   |
| ADD_R             | 130 | 0x82     | 4    | reg    | reg   | reg   | i=j+k;                                     |                                                                                                   |
| SUB_R             | 131 | 0x83     | 4    | reg    | reg   | reg   | i=j-k;                                     |                                                                                                   |
| AND_R             | 132 | 0x84     | 4    | reg    | reg   | reg   | i=j&k;                                     |                                                                                                   |
| OR_R              | 133 | 0x85     | 4    | reg    | reg   | reg   | i=j|k;                                     |                                                                                                   |
| XOR_R             | 134 | 0x86     | 4    | reg    | reg   | reg   | i=j^k;                                     |                                                                                                   |
| MUL_R             | 135 | 0x87     | 4    | reg    | reg   | reg   | i=j*k;                                     |                                                                                                   |
| DIV_R             | 136 | 0x88     | 4    | reg    | reg   | reg   | i=j/k;                                     |                                                                                                   |
| MOD_R             | 137 | 0x89     | 4    | reg    | reg   | reg   | i=j%k;                                     |                                                                                                   |
| MOVSX8b           | 138 | 0x8A     | 3    | reg    | reg   | -     | i=j;                                       |                                                                                                   |
| MOVSX16b          | 139 | 0x8B     | 3    | reg    | reg   | -     | i=j;                                       |                                                                                                   |
| MOV8SX            | 140 | 0x8C     | 3    | reg    | u8    | -     | i=j;                                       |                                                                                                   |
| MOV16SX           | 141 | 0x8D     | 4    | reg    | i16   | -     | i=j;                                       |                                                                                                   |
| IMUL_A            | 142 | 0x8E     | 1    | -      | -     | -     | A=A*B;                                     |                                                                                                   |
| IMUL_R            | 143 | 0x8F     | 4    | reg    | reg   | reg   | i=j*k;                                     |                                                                                                   |
| LED_CTRL          | 224 | 0xE0     | 2    | u8     | -     | -     | SELECTED_LED = i;                          | 0xff = release                                                                                    |
| LED_COL           | 225 | 0xE1     | 4    | RGB888 | -     | -     | SELECTED_LED_COL = i;                      |                                                                                                   |
| START             | 226 | 0xE2     | 2    | u8     | -     | -     | Start_key(i-1);                            | 0=all                                                                                             |
| STOP              | 227 | 0xE3     | 2    | u8     | -     | -     | Stop_key(i-1);                             | 0=all                                                                                             |
| SYCON             | 232 | 0xE8     | 2    | u8     | -     | -     |                                            | 系统控制                                                                                              |
| MALLOC            | 240 | 0xF0     | 2    | reg    | -     | -     | i=malloc(i);                               |                                                                                                   |
| FREE              | 241 | 0xF1     | 2    | reg    | -     | -     | i=free(i);                                 |                                                                                                   |
| NEW_THREAD        | 242 | 0xF2     | 4    | u8     | reg   | reg   | i=TH ID;j=addr or keymode;k=V[4]           | i的取值范围0~3，实际占用寄存器R12-R15暂存线程地址；主线程退出子线程也会被强制退出；子线程退出不会自动释放malloc内存，除非主线程退出；子线程里可以继续开子线程，但是不建议套太多层 |
|                   | 243 | 0xF3     | 1    | -      | -     | -     |                                            |                                                                                                   |
| WHILE_UPDATE      | 244 | 0xF4     | 1    | -      | -     | -     | while (update_flag)Sleep(1);               | 等待HID上传数据完成                                                                                       |
| JMP_TO_SCRIPT     | 245 | 0xF5     | 2    | u8     | -     | -     |                                            | 跳转到其他脚本号（寄存器数据保留，但PC会重置）                                                                          |
| MOV_PC2REG        | 246 | 0xF6     | 2    | reg    | -     | -     | i=PC;                                      | 把下一条指令的地址保存到寄存器                                                                                   |
| VALUE_RELOAD      | 247 | 0xF7     | 2    | reg    | -     | -     | i=Reload(reg);                             | 重新加载脚本参数                                                                                          |
| MODE_JOG          | 248 | 0xF8     | 1    | -      | -     | -     |                                            | 进入点动模式（再次按下按键不会被强制打断）                                                                             |
| WAIT_IF_RELEASE   | 249 | 0xF9     | 1    | -      | -     | -     | while (IO) Sleep(1);                       | 如果物理按键是释放状态，等待按下后才会继续执行                                                                           |
| WAIT_IF_PRESS     | 250 | 0xFA     | 1    | -      | -     | -     | while (!IO) Sleep(1);                      | 如果物理按键是按下状态，等待释放后才会继续执行                                                                           |
| EXIT_IF_RELEAS    | 251 | 0xFB     | 1    | -      | -     | -     | if (IO) exit();                            | 如果物理按键是释放的，退出脚本                                                                                   |
| EXIT_IF_PRESS     | 252 | 0xFC     | 1    | -      | -     | -     | if (!IO) exit();                           | 如果物理按键是按下的，退出脚本                                                                                   |
| EXIT_IF_ANYKEY    | 253 | 0xFD     | 1    | -      | -     | -     | if (SYS_KEY_COUNT != n)                    | n=脚本开始执行时保存的按键计数器。脚本执行后，可以用此指令实现按任意键退出                                                            |
| RES               | 254 | 0xFE     | 1    | -      | -     | -     | PC = 0;                                    | 跳转到程序开头，等同于JMP 0                                                                                  |
| EXIT              | 255 | 0xFF     | 1    | -      | -     | -     | exit();                                    | 退出脚本                                                                                              |
</details>  

## 4. Addressing Modes  
- **Immediate**  `123`  
- **Register**  `R0`  
- **Indirect**  `*R0`  

## 5. Memory & Stack Model  
- **Address Space**: Undefined (requires register-based addressing)  
- **Stack Direction**: Grows upward (auto-managed, accessible only via `PUSH`/`POP` instructions)  
- **Memory Alignment**: No alignment required  

## 6. Exception Handling  
| Exception Type          | Behavior                                                                 |  
|-------------------------|--------------------------------------------------------------------------|  
| **Invalid Opcode**       | Automatically terminates current thread and cleans resources            |  
| **Register Out-of-Bound** | Write operations to read-only registers are silently ignored             |  
| **Stack Overflow**       | Automatically terminates current thread and cleans resources            |  

## 7. HID Key Codes  

<details>
<summary>Expand details</summary>

Modifier Keys
```      
    0x01: 'hidkey_L_Ctrl',
    0x02: 'hidkey_L_Shift',
    0x04: 'hidkey_L_Alt',
    0x08: 'hidkey_L_Meta',
    0x10: 'hidkey_R_Ctrl',
    0x20: 'hidkey_R_Shift',
    0x40: 'hidkey_R_Alt',
    0x80: 'hidkey_R_Meta',
```  
Standard Keys
```  
    0x00: 'hidkey_UsbReserved',
    0x01: 'hidkey_UsbErrorRollOver',
    0x02: 'hidkey_UsbPostFail',
    0x03: 'hidkey_UsbErrorUndefined',
    0x04: 'hidkey_A',
    0x05: 'hidkey_B',
    0x06: 'hidkey_C',
    0x07: 'hidkey_D',
    0x08: 'hidkey_E',
    0x09: 'hidkey_F',
    0x0a: 'hidkey_G',
    0x0b: 'hidkey_H',
    0x0c: 'hidkey_I',
    0x0d: 'hidkey_J',
    0x0e: 'hidkey_K',
    0x0f: 'hidkey_L',
    0x10: 'hidkey_M',
    0x11: 'hidkey_N',
    0x12: 'hidkey_O',
    0x13: 'hidkey_P',
    0x14: 'hidkey_Q',
    0x15: 'hidkey_R',
    0x16: 'hidkey_S',
    0x17: 'hidkey_T',
    0x18: 'hidkey_U',
    0x19: 'hidkey_V',
    0x1a: 'hidkey_W',
    0x1b: 'hidkey_X',
    0x1c: 'hidkey_Y',
    0x1d: 'hidkey_Z',
    0x1e: 'hidkey_1',
    0x1f: 'hidkey_2',
    0x20: 'hidkey_3',
    0x21: 'hidkey_4',
    0x22: 'hidkey_5',
    0x23: 'hidkey_6',
    0x24: 'hidkey_7',
    0x25: 'hidkey_8',
    0x26: 'hidkey_9',
    0x27: 'hidkey_0',
    0x28: 'hidkey_Enter',
    0x29: 'hidkey_Escape',
    0x2a: 'hidkey_Backspace',
    0x2b: 'hidkey_Tab',
    0x2c: 'hidkey_Space',
    0x2d: 'hidkey_Minus',
    0x2e: 'hidkey_Equal',
    0x2f: 'hidkey_BracketLeft',
    0x30: 'hidkey_BracketRight',
    0x31: 'hidkey_Backslash',
    0x33: 'hidkey_Semicolon',
    0x34: 'hidkey_Quote',
    0x35: 'hidkey_Backquote',
    0x36: 'hidkey_Comma',
    0x37: 'hidkey_Period',
    0x38: 'hidkey_Slash',
    0x39: 'hidkey_CapsLock',
    0x3a: 'hidkey_F1',
    0x3b: 'hidkey_F2',
    0x3c: 'hidkey_F3',
    0x3d: 'hidkey_F4',
    0x3e: 'hidkey_F5',
    0x3f: 'hidkey_F6',
    0x40: 'hidkey_F7',
    0x41: 'hidkey_F8',
    0x42: 'hidkey_F9',
    0x43: 'hidkey_F10',
    0x44: 'hidkey_F11',
    0x45: 'hidkey_F12',
    0x46: 'hidkey_PrintScreen',
    0x47: 'hidkey_ScrollLock',
    0x48: 'hidkey_Pause',
    0x49: 'hidkey_Insert',
    0x4a: 'hidkey_Home',
    0x4b: 'hidkey_PageUp',
    0x4c: 'hidkey_Delete',
    0x4d: 'hidkey_End',
    0x4e: 'hidkey_PageDown',
    0x4f: 'hidkey_ArrowRight',
    0x50: 'hidkey_ArrowLeft',
    0x51: 'hidkey_ArrowDown',
    0x52: 'hidkey_ArrowUp',
    0x53: 'hidkey_NumLock',
    0x54: 'hidkey_PadDivide',
    0x55: 'hidkey_PadMultiply',
    0x56: 'hidkey_PadSubtract',
    0x57: 'hidkey_PadAdd',
    0x58: 'hidkey_PadEnter',
    0x59: 'hidkey_Pad1',
    0x5a: 'hidkey_Pad2',
    0x5b: 'hidkey_Pad3',
    0x5c: 'hidkey_Pad4',
    0x5d: 'hidkey_Pad5',
    0x5e: 'hidkey_Pad6',
    0x5f: 'hidkey_Pad7',
    0x60: 'hidkey_Pad8',
    0x61: 'hidkey_Pad9',
    0x62: 'hidkey_Pad0',
    0x63: 'hidkey_PadDecimal',
    0x64: 'hidkey_IntlBackslash',
    0x65: 'hidkey_ContextMenu',
    0x66: 'hidkey_Power',
    0x67: 'hidkey_PadEqual',
    0x68: 'hidkey_F13',
    0x69: 'hidkey_F14',
    0x6a: 'hidkey_F15',
    0x6b: 'hidkey_F16',
    0x6c: 'hidkey_F17',
    0x6d: 'hidkey_F18',
    0x6e: 'hidkey_F19',
    0x6f: 'hidkey_F20',
    0x70: 'hidkey_F21',
    0x71: 'hidkey_F22',
    0x72: 'hidkey_F23',
    0x73: 'hidkey_F24',
    0x74: 'hidkey_Open',
    0x75: 'hidkey_Help',
    0x77: 'hidkey_Select',
    0x79: 'hidkey_Again',
    0x7a: 'hidkey_Undo',
    0x7b: 'hidkey_Cut',
    0x7c: 'hidkey_Copy',
    0x7d: 'hidkey_Paste',
    0x7e: 'hidkey_Find',
    0x7f: 'hidkey_AudioVolumeMute',
    0x80: 'hidkey_AudioVolumeUp',
    0x81: 'hidkey_AudioVolumeDown',
    0x85: 'hidkey_NumpadComma',
    0x87: 'hidkey_IntlRo',
    0x88: 'hidkey_KanaMode',
    0x89: 'hidkey_IntlYen',
    0x8a: 'hidkey_Convert',
    0x8b: 'hidkey_NonConvert',
    0x90: 'hidkey_Lang1',
    0x91: 'hidkey_Lang2',
    0x92: 'hidkey_Lang3',
    0x93: 'hidkey_Lang4',
    0x94: 'hidkey_Lang5',
    0x9b: 'hidkey_Abort',
    0xa3: 'hidkey_Props',
    0xb6: 'hidkey_NumpadParenLeft',
    0xb7: 'hidkey_NumpadParenRight',
    0xbb: 'hidkey_NumpadBackspace',
    0xd0: 'hidkey_NumpadMemoryStore',
    0xd1: 'hidkey_NumpadMemoryRecall',
    0xd2: 'hidkey_NumpadMemoryClear',
    0xd3: 'hidkey_NumpadMemoryAdd',
    0xd4: 'hidkey_NumpadMemorySubtract',
    0xd7: 'hidkey_NumpadSignChange',
    0xd8: 'hidkey_NumpadClear',
    0xd9: 'hidkey_NumpadClearEntry',
    0xe0: 'hidkey_ControlLeft',
    0xe1: 'hidkey_ShiftLeft',
    0xe2: 'hidkey_AltLeft',
    0xe3: 'hidkey_MetaLeft',
    0xe4: 'hidkey_ControlRight',
    0xe5: 'hidkey_ShiftRight',
    0xe6: 'hidkey_AltRight',
    0xe7: 'hidkey_MetaRight',
```  
Mouse Keys
```  
    0x01: 'hidmouse_0',     //左键
    0x02: 'hidmouse_1',     //右键
    0x04: 'hidmouse_2',     //中键
    0x08: 'hidmouse_3',     //侧键1
    0x10: 'hidmouse_4',     //侧键2
```  
Multimedia
```  
    01: "hidmedia_BrightnessUp",
    02: "hidmedia_BrightnessDown",
    03: "hidmedia_ToggleCmera",
    04: "hidmedia_BeginScreenCapture",
    05: "hidmedia_OpenGameBar",
    06: "hidmedia_ScreenShot",
    07: "hidmedia_BeginStreaming",
    08: "hidmedia_Mute",
    09: "hidmedia_Bass",
    10: "hidmedia_VolumeUp",
    11: "hidmedia_VolumeDown",
    12: "hidmedia_PlayPause",
    13: "hidmedia_Stop",
    14: "hidmedia_PreviousTrack",
    15: "hidmedia_NextTrack",
    16: "hidmedia_BassUp",
    17: "hidmedia_BassDown",
    18: "hidmedia_TrebleUp",
    19: "hidmedia_TrebleDown",
    20: "hidmedia_MediaSelect",
    21: "hidmedia_Mail",
    22: "hidmedia_Calculator",
    23: "hidmedia_Explorer",
    24: "hidmedia_WWWSearch",
    25: "hidmedia_WWWHome",
    26: "hidmedia_WWWBack",
    27: "hidmedia_WWWForward",
    28: "hidmedia_WWWStop",
    29: "hidmedia_WWWRefresh",
    30: "hidmedia_WWWFavorites",
```  
</details>

## 8. Example Code

<details>  
<summary>Expand details</summary>  

- When the key is pressed, the script sends the A key, and waits for the key to be released to send the B key  
```  
PRESS_GK hidkey_A  
SLEEP 35  
RELEASE_GK hidkey_A  
SLEEP 35  
WAIT_IF_PRESS  
PRESS_GK hidkey_B  
SLEEP 35  
RELEASE_GK hidkey_B  
SLEEP 35  
EXIT  
```  

- Short press sends the A key (233 milliseconds), long press sends the B key
```  
MOV8 R0 233  
label_timeout:  
SLEEP 1  
JNZ KEY_IO label_shortpress  
DJNZ R0 label_timeout  
label_longpress:  
PRESS_GK hidkey_B  
WAIT_IF_PRESS  
RELEASE_GK hidkey_B  
EXIT  
label_shortpress:  
PRESS_GK hidkey_A  
SLEEP 35  
RELEASE_GK hidkey_A  
EXIT  
```

- Randomly output a random number between 65 and 80 (sent directly using HID key value)
```
MODE_JOG ;Prevent interruption by pressing the key again during the output process
MOV8 R1 16
MOD_R R1 RANDOM R1
ADD8 R1 65 ;Calculate the final required value and store it in R1
MOV A R1
loc_000e:
MOV8 B 10
DIV_A
INC R2
JNZ A loc_000e ;Calculate how many bits are stored in R2 in a loop. At this time, the remainder saved in register B is the highest bit and can be directly typed
loc_0018: ;The following is the bit-by-bit key operation.
JNZ B loc_001f
MOV8 B 10 ;If the value is 0, add 10 directly for easy calculation (the value of hidkey_0 is 0x27, hidkey_1 is 0x1e)
loc_001f:
MOV A B
ADD8_A 29 ;Add the value of (hidkey_1 minus 1)
PRESS_GK_VAL A
SLEEP 35
RELEASE_GK_VAL A
SLEEP 35 ;The single digit is now printed
DEC R2 ;The number of bits to be output - 1
JZ R2 loc_0044 ;If there is no more, jump to exit
MOV R0 R2
MOV A R1
loc_0038:
MOV8 B 10
DIV_A
DJNZ R0 loc_0038
JZ R0 loc_0018 ; Jump after calculating the next digit
loc_0044:
```

- Output prime numbers within 10000, and press any key to exit (Coder by DeepSeek)
```
MODE_JOG
PRESS_GK hidkey_2
SLEEP 5
RELEASE_GK hidkey_2
SLEEP 5
PRESS_GK hidkey_Enter
SLEEP 5
RELEASE_GK hidkey_Enter
SLEEP 5
MOV32 R0  2
label_outer:
MOV32 R1  2
MOV R3  R0
DEC R3
label_inner:
MOV A  R0
MOV B  R1
DIV_A
JNZ B  label_not_div  
JMP label_next_num  
label_not_div:
INC R1
CMP R1  R3
JB R1  R3  label_inner
MOV A  R0
CLR R2
label_calc_digits:
MOV8 B  10
DIV_A
INC R2
JNZ A  label_calc_digits
label_output:
JNZ B  label_non_zero
MOV8 B  10
label_non_zero:
MOV A  B
ADD8_A 29
PRESS_GK_VAL A
SLEEP 5
RELEASE_GK_VAL A
SLEEP 5
DEC R2
JZ R2  label_finish_num
MOV R4  R2
MOV A  R0
label_shift:
MOV8 B  10
DIV_A
DJNZ R4  label_shift
JMP label_output
label_finish_num:
PRESS_GK hidkey_Enter
SLEEP 5
RELEASE_GK hidkey_Enter
SLEEP 5
label_next_num:
EXIT_IF_ANYKEY
INC R0
MOV32 R15  10000
JB R0  R15  label_outer
EXIT
```

- Single click to output A key, double click to output B key (interval 150ms)
```
MODE_JOG
WAIT_IF_PRESS
MOV16 A  150
label_timeout:
SLEEP 1
JZ KEY_IO  label_press2
DJNZ A  label_timeout
PRESS_GK hidkey_A
SLEEP 35
RELEASE_GK hidkey_A
EXIT
label_press2:
PRESS_GK hidkey_B
SLEEP 35
RELEASE_GK hidkey_B
EXIT
```

- After pressing the key, "press A every 10 seconds, press B every 15 seconds, and add random delay to prevent game detection", press again to stop (default is in switch mode)
```
MOV R0  SYS_TIME_S
loc_0003:
MOV A  SYS_TIME_S
SUB_A R0
MOV8 B  10
DIV_A
JNZ B  loc_001c
PRESS_GK hidkey_A
SLEEP 35
SLEEP_RAND 20
RELEASE_GK hidkey_A
SLEEP 35
SLEEP_RAND 128
loc_001c:
MOV A  SYS_TIME_S
SUB_A R0
MOV8 B  15
DIV_A
JNZ B  loc_0033
PRESS_GK hidkey_B
SLEEP 35
SLEEP_RAND 20
RELEASE_GK hidkey_B
SLEEP 35
loc_0033:
MOV16 A  1000
SUB_A SYS_TIME_MS
SLEEP_VAL A
SLEEP_RAND 128
JMP loc_0003
EXIT
```

- Automatically press A repeatedly after pressing, stop after releasing the key, add random delay
```
PRESS_GK hidkey_A
SLEEP 35
SLEEP_RAND 20
RELEASE_GK hidkey_A
SLEEP 35
SLEEP_RAND 20
EXIT_IF_RELEAS
RES
```

- Press to switch the keyboard function layer (FN key function), release the key to restore. If it is just a single click, send mute. (Long press to switch layers, if it is a single click to perform other operations)
```
MOV8 SYS_KEY_LAY  1
WAIT_IF_PRESS
MOV8 SYS_KEY_LAY  0
EXIT_IF_ANYKEY
PRESS_MU hidmedia_Mute
SLEEP 35
RELEASE_MU hidmedia_Mute
EXIT
```
</details>

## 9. You can download this document in the upper right corner of the page and let AI help you write it

## X. Special instructions for AI assistants

<details>

<summary></summary>

### X.1 Some points of attention expressed by users

- "Keep pressing" probably means "press-release-press-release..." rather than "keep pressing".

- "Interval duration" probably means the interval duration between "two cycles" rather than the duration of "two operations"; most of the interval duration is waiting for the next cycle.

- If the user does not specify the "press duration", the default is 35 milliseconds; but if the user requires randomness, the default is randomness within the range of 30~60 milliseconds.

- If the user requires random time, please add appropriate amount of randomness in all places with delay; random time does not need to be precise.

### X.2 How device scripts run

- The user has a keyboard that supports programming to implement a series of operations
- The physical keys on the keyboard are switches that trigger the script (no need to consider key jitter)
- Please understand whether the user is describing "physical keys" or "key operations to be implemented"
- If there is an infinite loop in the program, please confirm whether you need to add any key to exit (you need to execute this instruction to make a judgment)

### X.3 Device Description

- The keyboard may have multiple key layers (FN layers), each layer can be customized, and the user may have the need to switch layers
- The keyboard has many functions, and the script is just one of the key modes, which can run the script code
- The keyboard has n keys (n≥1) and m keyboard layers (m≥1)
- The keys of each layer can be customized, each definition is 5 bytes, including 1-byte mode and 4*1-byte optional parameters.
- The script name can be modified
- The script name can use special characters to limit the parameter type passed, making the script more flexible and reusable (binding multiple keys to the same script, implementing different keys through different parameters, etc.)

### X.4 Instruction Description

- Some instructions may not have an immediate version. You can use MOV8, MOV16, MOV32 instructions to load the immediate value into the register first.
- For instructions with immediate versions, please confirm the range of the immediate value; if it is out of range, use the register version of the instruction.
- The HID key value (0x04) is not used in the code, but the alias in the document (hidkey_A); multiple modifier keys can be connected using "|"
- The RANDOM register is generally used only for reading, please do not try to write
- The key delay is recommended to be no less than 16ms
- Random delay is generally not used alone, but used in conjunction with fixed delay. A few examples:
```
;Random 10-30ms
SLEEP 10
SLEEP_RAND 20
```
```
;Random 10-3000ms
SLEEP 10
SLEEP_RAND_U16 2990
```
```
;Random 1000-3000ms
SLEEP_U16 1000
SLEEP_RAND_U16 2000
```
- Modifier keys and normal keys also need to add a smaller delay, such as 16ms, otherwise some software may not recognize it.
```
PRESS_SK 0x04 ; Press left Alt
SLEEP 16
PRESS_GK 0x2B ; Press Tab
SLEEP 35
RELEASE_GK 0x2B ; Release Tab
SLEEP 16
RELEASE_SK 0x04 ; Release Alt
```

Thank you for helping users!

</details>