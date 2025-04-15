# Option Byte Settings

The Option Byte section provides additional configuration settings for your SayoDevice. These settings control various hardware and firmware behaviors.

## Key Debounce Time

> Controls how the device processes rapid key presses

**Default Value**: 6 milliseconds

Debounce time prevents a single physical keypress from registering multiple times due to mechanical switch characteristics. If you experience unwanted double-clicks, try increasing this value to 20 or higher.

**Note**: Hall effect switches don't require debounce adjustments as they use a different sensing technology.

---

## HID Functions

> Hardware Interface Device functions that can be enabled as needed

After enabling any of these functions:
1. Save your settings
2. Reconnect the device using the USB data cable
3. For Bluetooth connections, you must remove the device from your paired devices list and pair it again

### Relative Mouse Control

Enables your device to control cursor movement and mouse button operations.

**Features**:
- Customizable cursor speed and acceleration
- Button mapping for clicks and scrolling
- Scriptable mouse movements

---

### Multimedia Control

Enables media playback and system volume controls.

**Features**:
- Volume adjustment (up/down/mute)
- Media playback (play/pause/next/previous)
- Application controls
- System functions

---

### Joystick Mode

Enables your device to be recognized as a game controller by compatible games.

**Platform Compatibility**: Windows only
!> **WARNING**: Do not enable this feature on macOS systems as it may render your device unusable until reconfigured on a Windows system.

**Setup Process**:
1. Enable "Joystick" in the Option Byte settings
2. Save changes and reconnect the USB data cable
3. Change the button mode to "Game Controller" for desired keys
4. Select the appropriate button number assignment

**Note**: The assigned buttons are virtual inputs that need to be mapped within the game's controller settings. Games must support custom controller configuration.

---

### Absolute Mouse Positioning

Enables precise cursor positioning and mouse operation recording/playback capabilities.

**Platform Compatibility**: Windows only, single-screen setups

**Benefits**:
- Place the cursor at exact screen coordinates via scripts
- Record mouse movements and clicks for later playback
- Create precise automation workflows

---

### Controller Emulation

Simulates a complete game controller device with 6 axes of input and multiple buttons.

**Features**:
- Analog stick emulation
- Multiple button inputs
- Pressure-sensitive controls (where supported)
- Full DirectInput compatibility

---

## Sleep Timeout

> Controls how long the device waits before entering power-saving mode

This setting is only applicable in wireless operation mode and has no effect when the device is connected via USB.

**Adjustment**: You must connect your device via USB data cable to modify this setting.

**Recommendation**: Balance battery life against convenience by setting an appropriate timeout for your usage patterns.

---

## Indicator Timeout

> Controls how long status LEDs remain illuminated after activation

This setting is only applicable in wireless operation mode and has no effect when the device is connected via USB.

**Adjustment**: You must connect your device via USB data cable to modify this setting.

**Note**: Lower timeout values conserve battery power but may make indicators harder to notice.

---

## AZERTY Keyboard Layout

> Enables French AZERTY keyboard layout compatibility for one-key password function

When enabled, the password function will use the AZERTY key mapping instead of the default ANSI layout.

**Use this when**: You're using a French AZERTY keyboard layout and want the password feature to match your physical keyboard.

---

## Screen Resolution Settings

> Configure monitor resolution for accurate cursor positioning in scripts

If you use mouse positioning functions in scripts, you must set the correct screen resolution for accurate cursor placement.

**Setup Process**:
1. Open the configuration tool
2. Verify the automatically detected resolution settings
3. If incorrect, manually adjust to match your display configuration
4. Click "Auto Setup" to apply the settings

**Multi-Monitor Note**: For multi-monitor setups, you may need to adjust these settings based on your primary display or the display where you'll be using mouse positioning scripts.
