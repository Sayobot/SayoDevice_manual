# Device Options

This section explains the various configuration options available for your SayoDevice. Note that different device models may support different functions.

## Key Debounce Time

> Controls the time required between key releases to register as separate keypresses

**Default Value**: 10 milliseconds

The debounce time prevents a single physical keypress from being registered as multiple presses due to mechanical switch bounce. Increasing this value can help if you experience unwanted double-clicks.

!> **Note**: This setting does not affect hall effect keys, as they use a different technology that doesn't require debounce.

---

## Device Functions

> Extended functionality options that can be enabled based on your needs

### Relative Mouse Control

Enables your device to control cursor movement and mouse button clicks.

**Use this when you want to**: 
- Use keys to move the mouse cursor
- Configure mouse button functionality
- Create scripts that control mouse movement

!> **Important**: After changing this setting, you must save and reconnect the data cable. If using Bluetooth, you'll need to delete the device and re-pair.

---

### Multimedia Control

Enables multimedia functions such as volume adjustment, media playback controls, and application launching.

**Use this when you want to**:
- Control audio volume
- Play/pause media
- Skip tracks
- Launch specific applications

!> **Important**: After changing this setting, you must save and reconnect the data cable. If using Bluetooth, you'll need to delete the device and re-pair.

---

### Joystick Function

Enables your device to function as a game controller.

**Setup Process**:
1. Enable "Joystick" in the device options
2. Change the key mode to "Game Controller"
3. Select the desired key number

**Notes**:
- The assigned keys aren't directly mapped to physical controller buttons
- Games must support custom controller button mapping

!> **Warning**: This function is only compatible with Windows. Do not enable this on macOS as it may cause your device to become unusable. If accidentally enabled on macOS, use a Windows system to disable it.

!> **Important**: After changing this setting, you must save and reconnect the data cable. If using Bluetooth, you'll need to delete the device and re-pair.

---

### Dial Mode

This option is specifically designed for SayoDevice models with knobs.

**Configuration**: Navigate to Device Options → Device Function → Dial

**Windows-Specific Feature**: In Windows, you can configure different dial functions for different software applications.

!> **Important**: After changing this setting, you must save and reconnect the data cable. If using Bluetooth, you'll need to delete the device and re-pair.

---

### Absolute Mouse Positioning

Enables precise cursor positioning features for scripts and macro recording.

**Benefits**:
- Allows scripts to move the cursor to specific screen coordinates
- Enables recording and playback of mouse operations
- Creates more precise automated workflows

!> **Note**: Recording functionality is limited to Windows systems.

!> **Important**: After changing this setting, you must save and reconnect the data cable. If using Bluetooth, you'll need to delete the device and re-pair.

---

### Game Controller Emulation

Enables comprehensive game controller simulation, including:
- 8 axes of movement
- Hat switch (D-pad)
- Multiple buttons
- Pressure sensitivity (where supported)

**Use this when you want to**:
- Create a fully-featured game controller from your device
- Use advanced controller features in games
- Set up complex gaming macros

!> **Important**: After changing this setting, you must save and reconnect the data cable. If using Bluetooth, you'll need to delete the device and re-pair.

---

### Additional Options

#### Power-on Delay
Adds a 0.5-second delay before USB recognition after connection.

**Use this when**: Your computer is slower to recognize USB devices or you experience connectivity issues.

#### AZERTY Keyboard Layout
Optimizes one-key password functionality for French AZERTY keyboard layouts.

**Use this when**: You're using a French keyboard layout and the password feature.

#### Disable Lighting
Turns off all RGB and indicator lighting on the device.

**Use this when**: You prefer no lighting or want to extend battery life in wireless mode.

#### KVM Compatibility Mode
*Deprecated - no longer needed in current firmware versions*

---

## Language Selection

> Changes the display language on devices with built-in screens

Available languages depend on your device model and firmware version.

---

## Screen Resolution Settings

> Sets the reference resolution for cursor positioning in scripts

These values are typically configured automatically by the software based on your computer's display settings. Manual adjustment is only necessary for multi-monitor setups or custom resolutions.

---

## USB Report Rate

> Controls how frequently the device sends updates to the computer

**Default**: 1000Hz (1ms)

Higher values provide more responsive input but may use more power. Lower values can extend battery life in wireless mode but may introduce slight input lag.

Available options:
- 125Hz (8ms)
- 250Hz (4ms)
- 500Hz (2ms)
- 1000Hz (1ms)

---

## Encoder Channel

> Advanced setting for knob-equipped devices

**Recommendation**: Do not modify this setting unless specifically instructed by support.

---

## Sleep Timeout

> Controls how long the device waits before entering sleep mode when inactive

This setting only applies in wireless mode and helps conserve battery power.

**Adjustment**: Connect your device using a USB data cable, make the change, and then disconnect to apply.

---

## Indicator Light Timeout

> Controls how long indicator lights remain illuminated after a key press

This setting only applies in wireless mode and helps conserve battery power.

**Adjustment**: Connect your device using a USB data cable, make the change, and then disconnect to apply.

---

## Keyboard Layout

> Selects the appropriate key mapping for the one-key password function

Choose the layout that matches your physical keyboard to ensure passwords are entered correctly.
