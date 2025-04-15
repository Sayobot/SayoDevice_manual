# Script Editing Guide

This section provides detailed instructions on how to create, edit, and manage scripts for your SayoDevice.

## Script Editor Interface

![Script Editor Interface](img/script_editor.jpg)

The script editor interface consists of the following components:
- **Script List**: Shows all available scripts in your device
- **Script Name**: Edit field for naming your script
- **Command List**: Shows the sequence of commands in your script
- **Command Editor**: Interface for modifying specific commands
- **Script Operations**: Buttons for testing, saving, and other operations

## Creating a New Script

To create a new script:

1. Navigate to the Script section in the application
2. Click the **+** button in the script list
3. Enter a descriptive name for your script
4. Start adding commands using the command editor
5. Click **Save** when you've finished creating your script

## Adding Commands

There are several ways to add commands to your script:

### Adding Individual Commands

1. Position your cursor where you want to insert the command
2. Click the **Add Command** button
3. Select the command type from the dropdown menu
4. Configure the parameters for the command
5. Click **Insert** to add the command to your script

### Adding Command Sequences

For common command sequences (like key press and release with delays):

1. Click the **Add Sequence** button
2. Select the type of sequence (e.g., Key Press/Release)
3. Configure the parameters for the sequence
4. Click **Insert** to add the entire sequence to your script

## Editing Commands

To edit an existing command:

1. Select the command in the command list
2. Modify the parameters in the command editor
3. Click **Update** to apply your changes

## Removing Commands

To remove a command:

1. Select the command you want to remove
2. Click the **Delete** button
3. Confirm the deletion when prompted

## Testing Scripts

Before finalizing your script, you should test it to ensure it works as expected:

1. Click the **Test** button
2. Observe the script execution
3. Press **Stop** to end the test if needed
4. Make any necessary adjustments based on the test results

## Copying and Pasting Commands

To copy and paste commands:

1. Select the command(s) you want to copy
2. Click the **Copy** button or use Ctrl+C
3. Select the position where you want to paste
4. Click the **Paste** button or use Ctrl+V

## Organizing Scripts

To keep your scripts organized:

1. Use descriptive names that indicate the script's function
2. Group related scripts together by using naming conventions
3. Delete unused scripts to avoid clutter
4. Export important scripts as backups

## Working with Parameters

Scripts can accept parameters that modify their behavior:

1. Determine which aspects of your script should be parameterized
2. Use register operations to load and use parameters
3. Document the expected parameters in the script name or comments
4. Test your script with different parameter values

## Advanced Editing Features

### Using Variables

Variables (registers) allow for more dynamic scripts:

1. Initialize registers at the beginning of your script
2. Use operations to modify register values as needed
3. Reference registers in commands that support variable input

### Creating Loops

To create a loop in your script:

1. Place a label at the start of the loop (using SET_FLAG)
2. Add the commands to be repeated
3. Add a jump command back to the label (using JMP or conditional jumps)
4. Ensure you have an exit condition to prevent infinite loops

### Error Handling

To make your scripts more robust:

1. Check for conditions that might cause errors
2. Include alternative paths for handling unexpected situations
3. Use timeouts to prevent the script from hanging

## Saving and Exporting Scripts

Always remember to:

1. Save your script after making changes
2. Export important scripts as backup
3. Document any special requirements or behaviors