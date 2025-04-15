# Backup Management

The backup feature allows you to save your device configuration settings and restore them later. This is particularly useful for:
- Creating safety backups before making significant changes
- Transferring configurations between multiple devices
- Sharing your setup with other users
- Recovering after a firmware update or device reset

## Creating a Backup

1. Navigate to the Backup tab in the application
2. Select which data components you want to include in your backup:
   - Key mappings
   - Lighting profiles
   - Macros and scripts
   - Device settings
3. Click "Export" to save the backup file
4. Choose a location and filename for your backup

![Setting backup](./img/backup-config.gif)

## Restoring from a Backup

1. Navigate to the Backup tab
2. Click "Recovery Mode" to initiate the import process
3. Select the backup file you wish to restore
4. Choose which components you want to restore:
   - Select all components, or
   - Choose specific elements to restore
5. Click "Start Recovery" to apply the settings

![Restore backup](./img/restore-config.gif)

## Backup Compatibility

**Device Compatibility**:
- Same model: Full compatibility for all settings
- Different models with similar features: Partial compatibility (common features only)
- Different model types: Limited compatibility (basic features only)

**Firmware Version Considerations**:
- Restoring to the same firmware version: Recommended for best results
- Restoring to a newer firmware version: Generally compatible, but some settings may need adjustment
- Restoring to an older firmware version: Not recommended, may cause unexpected behavior

## Backup File Management

**Organizing Backups**:
- Use descriptive filenames including device model and date
- Example: "SayoDevice_KB01_March2025.sayo"
- Store backups in a dedicated folder for easy access

**Backup Security**:
- Keep backups in a secure location
- Consider creating redundant copies of critical configurations
- Remember that backups may contain sensitive information like macros and scripts

## Troubleshooting Backup Issues

**If Restoration Fails**:
1. Verify your device is properly connected
2. Ensure the backup file is not corrupted
3. Check that your firmware version is compatible
4. Try restoring only basic settings first, then add more complex settings

**If Settings Don't Apply Correctly**:
1. Restart the application
2. Reconnect your device
3. Consider updating your firmware to the latest version
4. Try restoring settings individually rather than all at once