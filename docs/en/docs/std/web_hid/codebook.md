# Script Examples

This section provides practical examples of scripts that you can use with your SayoDevice. These examples demonstrate common use cases and can serve as starting points for your own custom scripts.

## Example 1: Simple Copy-Paste Operation

This script performs a standard copy and paste operation:

```
# Press Ctrl+C (Copy)
S_SK Left_Control      # Press Left Control
SLEEP 10               # Wait 10ms
S_GK c                 # Press C key
SLEEP 20               # Wait 20ms
S_UGK c                # Release C key
SLEEP 10               # Wait 10ms
S_USK Left_Control     # Release Left Control
SLEEP 100              # Wait 100ms

# Press Ctrl+V (Paste)
S_SK Left_Control      # Press Left Control
SLEEP 10               # Wait 10ms
S_GK v                 # Press V key
SLEEP 20               # Wait 20ms
S_UGK v                # Release V key
SLEEP 10               # Wait 10ms
S_USK Left_Control     # Release Left Control
```

## Example 2: Gaming Macro (Rapid Fire)

This script simulates rapid clicking for gaming applications:

```
# Enter Momentary Mode (script only runs while key is held)
MOD_MOMENTARY

# Set up rapid clicking loop
LABEL loop_start
S_MK Left_Button       # Press left mouse button
SLEEP 20               # Wait 20ms
S_UMK Left_Button      # Release left mouse button
SLEEP 30               # Wait 30ms

# Check if button is still pressed, if yes continue loop
READ IO A              # Read IO state into register A
TEST_E A 0             # Test if key is still pressed (A equals 0)
JNE loop_start         # If still pressed, jump back to loop_start
```

## Example 3: Application Launcher

This script opens a specific application:

```
# Press Windows key
S_SK Left_GUI          # Press Windows/GUI key
SLEEP 50               # Wait 50ms
S_USK Left_GUI         # Release Windows/GUI key
SLEEP 100              # Wait 100ms

# Type the application name
S_GK n                 # Press N key
SLEEP 20               # Wait 20ms
S_UGK n                # Release N key
SLEEP 20               # Wait 20ms
S_GK o                 # Press O key
SLEEP 20               # Wait 20ms
S_UGK o                # Release O key
SLEEP 20               # Wait 20ms
S_GK t                 # Press T key
SLEEP 20               # Wait 20ms
S_UGK t                # Release T key
SLEEP 20               # Wait 20ms
S_GK e                 # Press E key
SLEEP 20               # Wait 20ms
S_UGK e                # Release E key
SLEEP 20               # Wait 20ms
S_GK p                 # Press P key
SLEEP 20               # Wait 20ms
S_UGK p                # Release P key
SLEEP 20               # Wait 20ms
S_GK a                 # Press A key
SLEEP 20               # Wait 20ms
S_UGK a                # Release A key
SLEEP 20               # Wait 20ms
S_GK d                 # Press D key
SLEEP 20               # Wait 20ms
S_UGK d                # Release D key
SLEEP 100              # Wait 100ms

# Press Enter to launch
S_GK Return            # Press Enter/Return key
SLEEP 20               # Wait 20ms
S_UGK Return           # Release Enter/Return key
```

## Example 4: Volume Control Script

This script demonstrates how to control system volume:

```
# Volume Up
S_MU Volume_Increment  # Increase volume
SLEEP 50               # Wait 50ms
S_UMU Volume_Increment # Release volume up control
SLEEP 200              # Wait 200ms

# Volume Down
S_MU Volume_Decrement  # Decrease volume
SLEEP 50               # Wait 50ms
S_UMU Volume_Decrement # Release volume down control
SLEEP 200              # Wait 200ms

# Mute/Unmute
S_MU Mute              # Toggle mute
SLEEP 50               # Wait 50ms
S_UMU Mute             # Release mute control
```

## Example 5: Text Entry with String Function

This script demonstrates using the string function for text entry:

```
# Input text string from string database
S_STR 1                # Send string #1 from string database
SLEEP 100              # Wait 100ms

# Alternative method with direct character input
S_GK h                 # Press H key
SLEEP 20               # Wait 20ms
S_UGK h                # Release H key
SLEEP 20               # Wait 20ms
S_GK e                 # Press E key
SLEEP 20               # Wait 20ms
S_UGK e                # Release E key
SLEEP 20               # Wait 20ms
S_GK l                 # Press L key
SLEEP 20               # Wait 20ms
S_UGK l                # Release L key
SLEEP 20               # Wait 20ms
S_GK l                 # Press L key
SLEEP 20               # Wait 20ms
S_UGK l                # Release L key
SLEEP 20               # Wait 20ms
S_GK o                 # Press O key
SLEEP 20               # Wait 20ms
S_UGK o                # Release O key
```

## Tips for Creating Effective Scripts

1. **Add sufficient delays**: Include appropriate SLEEP commands between actions
2. **Use comments**: Document your script with comments for better readability
3. **Test incrementally**: Develop and test your script in small sections
4. **Optimize for reliability**: Sometimes slower scripts are more reliable
5. **Use variables**: For more complex scripts, use variables to store and manipulate values