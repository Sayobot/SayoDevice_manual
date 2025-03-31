# Screen Configuration

This section explains how to customize the display on SayoDevice models equipped with screens.

## Setting Up Custom Screen Images

### Adding New Images

1. Navigate to the **Images** tab in the application
2. Click the **Add** (+) button in the upper left corner

![Main Screen Interface](/img_screen/main.jpg)

### Preparing Your Images

1. In the popup window, click the icon in the upper left corner to open an image file
2. Adjust the output resolution in the right toolbar:
   - **Important**: For O3C devices, maximum screen resolution is 160x80 pixels
   - Exceeding this resolution will cause display abnormalities

3. Scale and crop your image:
   - Enter specific resolution values directly, or
   - Use the + and - buttons to adjust size incrementally
   - Drag the selection frame to capture the desired portion of the image

4. Click the checkmark (✓) to confirm your selection

![Image Selection](/img_screen/1.jpg)
![Image Scaling](/img_screen/2.jpg)

### Uploading to Your Device

1. Click **Submit** to send the image to your device
2. Wait for the download to complete
   - The device screen will display a progress bar during this process

![Upload Progress](/img_screen/3.jpg)

## Configuring Screen Layers

1. Navigate to the **Screen** tab
2. In the upper left corner, select the screen type you want to configure:
   - **Main Screen**: Normal operation display
   - **Boot Screen**: Displayed during device startup
   - **Idle Screen**: Displayed when device is inactive

3. Work with layers in the left panel:
   - Layers are drawn in order from top to bottom
   - Top layers may obscure elements on lower layers
   - Select a layer to edit its properties

![Screen Configuration Interface](/img_screen/4.jpg)

4. When creating a new configuration, select a layer (avoid the first layer if it's set to "Clean Screen" as this is typically needed)
5. Modify the layer parameters in the right panel according to your needs

![Layer Configuration](/img_screen/5.jpg)

## Troubleshooting Screen Issues

If your device doesn't function properly after modifying screen settings, you have two recovery options:

### Method 1: Soft Reset
1. Press and hold the knob while reconnecting the USB data cable
2. Without exiting the menu page, reopen the software
3. Modify the screen settings again with correct parameters

### Method 2: Factory Reset
1. Press and hold the knob while reconnecting the USB data cable
2. Navigate to Menu → Device → Factory Recovery
3. This will restore all default settings, including screen configurations

## Layer Types and Parameters

### Empty Layer
Creates a blank placeholder layer with no visible elements

### Pure Color
Displays a solid rectangular color area
- Parameters: Color, Size, Position

### Widget
Displays built-in functional elements:
- 1: Empty (no widget)
- 2: Key Strength Bar (Vertical)
- 3: Key Strength Bar (Horizontal)
- 4: CPU Load Monitor
- 5: Bongo Cat Animation

### Key Count
Displays a counter for key presses
- Parameters: Position, Style, Counter Limit

### ASCII String
Displays custom text on the screen
- Parameters: Text content, Font, Position, Color

### Built-in Image
Uses pre-installed system images
- Parameters: Image selection, Position

### Custom Image
Displays your uploaded custom images
- Parameters: Image selection, Position, Scaling

### Clean Screen
Clears all screen content
- **Important**: Typically placed as the first (bottom) layer

## Parameter Descriptions

### Offset X/Y
Sets the position of elements relative to the top-left corner
- Values must keep the element within screen boundaries

### Key Number
Associates the layer with a specific key on your device
- Used for dynamic elements that respond to key actions

### Show Condition
Controls when the layer is visible based on key states
- Options: Always, When Pressed, When Released

### Max Digits
For numeric displays, sets the maximum number of digits to show
- Useful for counters and numeric indicators