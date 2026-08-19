# Installation Guide

## Prerequisites

- World of Warcraft 3.3.5a (Wrath of the Lich King)
- Admin access to WoW installation folder (for some installations)

## Installation Steps

### Option 1: Manual Installation (Recommended)

1. **Download the addon**
   - Clone or download this repository as a ZIP file
   - Extract the ZIP file

2. **Locate your AddOns folder**
   - **Windows**: `C:\Program Files (x86)\World of Warcraft\Interface\AddOns\`
   - **macOS**: `/Applications/World of Warcraft/Interface/AddOns/`
   - **Linux**: Varies by installation (check your WoW folder)

3. **Copy the addon folder**
   - Copy the `Chatter` folder into your `AddOns` folder
   - Final path should look like: `.../Interface/AddOns/Chatter/`

4. **Verify installation**
   ```
   AddOns/
   ├── Chatter/
   │   ├── Chatter.lua
   │   ├── Chatter.toc
   │   ├── Modules/
   │   ├── Libs/
   │   └── Localization/
   ```

5. **Launch WoW**
   - Start the game
   - On login screen, click **AddOns** button
   - Enable "Chatter" addon
   - Log in to a character

6. **Verify it loaded**
   - Type `/addon list` in chat to see all loaded addons
   - Look for "Chatter" in the list
   - Should show no errors in BugSack (if installed)

### Option 2: Using Git (For Updates)

If you want to stay updated via git:

```bash
# Navigate to your AddOns folder
cd "C:\Program Files (x86)\World of Warcraft\Interface\AddOns"

# Clone the repository
git clone https://github.com/YourUsername/Chatter.git

# Navigate into Chatter folder
cd Chatter

# Check for updates anytime
git pull origin main
```

## Upgrading from Previous Version

### From Original Chatter 1.2.11

1. **Backup your settings** (optional but recommended)
   - Copy `WTF/Account/YourAccount/SavedVariables/Chatter.lua` to a safe location

2. **Replace addon folder**
   - Delete old Chatter folder (or rename to Chatter.old)
   - Copy new Chatter folder into AddOns

3. **Reload in-game**
   - Type `/reload` to reload addons
   - Settings are preserved automatically

### From Other Chat Addons

If switching from another chat addon:
1. Disable the old addon
2. Install Chatter
3. `/reload`
4. Reconfigure chat tabs as needed

## Configuration

### First Launch

1. Type `/chatter` or go to Addons menu → Chatter
2. Configure modules as desired:
   - **Chat Copy**: Toggle the blue copy icon visibility
   - **Scrollback**: Set history size (250-2500 lines)
   - **Alt Linking**: Enable guild note scanning
   - And more...

### Default Settings

- Copy Icon: Enabled by default
- Scrollback per frame: 250 lines
- Guild Notes: Enabled (if in guild)

### Chat Tabs Setup

1. Right-click on chat tab
2. Select "Settings"
3. Configure channels, colors, font size, etc.
4. Close window to save

## Troubleshooting Installation

### Addon Not Appearing in Addons Menu

**Problem**: Chatter doesn't show up in the AddOns list

**Solution**:
1. Verify folder name is exactly `Chatter` (case-sensitive on some systems)
2. Check that `Chatter.toc` file exists in the folder
3. Ensure all files were extracted (not just the parent folder)
4. Verify `Interface/AddOns/` path is correct
5. Restart WoW completely (not just `/reload`)

### Error on Login

**Problem**: Lua error appears on character login (BugSack)

**Solution**:
1. This version fixes the nil error in AltNames.lua - ensure you're using the latest
2. If error persists: `/gquit` and rejoin guild, then `/reload`
3. Report the error at GitHub issues with full error message

### Copy Icon Missing

**Problem**: Can't find the copy icon in chat frame

**Solution**:
1. Open `/chatter` options
2. Go to "Chat Copy" section
3. Toggle "Show copy icon" to ON
4. Icon should appear at bottom-right of chat frame

### Settings Reset After Reload

**Problem**: Options revert to defaults after `/reload`

**Solution**:
1. Check that SavedVariables file exists:
   - `WTF/Account/YourAccount/SavedVariables/Chatter.lua`
2. Verify file is not read-only
3. Check WTF folder permissions
4. Re-save settings in options menu

## Uninstallation

### Clean Removal

1. **Delete addon folder**
   ```
   Delete: Interface/AddOns/Chatter/
   ```

2. **Remove saved settings** (optional)
   ```
   Delete: WTF/Account/YourAccount/SavedVariables/Chatter.lua
   ```

3. **Reload WoW**
   - `/reload` or restart game

### Keep Settings for Reinstall

If you might reinstall later:
1. Keep the `Chatter.lua` file from SavedVariables folder
2. When reinstalling, place it back in the same location
3. Settings will be restored

## Compatibility

### WoW Versions
- ✅ WoW 3.3.5a (Wrath of the Lich King) - **Fully Supported**
- ❌ WoW Retail (Current) - Not compatible
- ❌ WoW Classic - Not tested (may need modifications)
- ⚠️ Other expansions - Untested

### Conflicting Addons

Chatter should work with most chat-related addons, but potential conflicts:
- **Prat 3.0** - Alternative chat addon; use one or the other
- **ChatTabs** - Chatter includes tab functionality; may conflict
- **Copycat** - Alternative copy addon; similar features

### Performance

- **Memory usage**: ~5-15MB depending on chat history size
- **CPU usage**: Minimal (< 1% most of the time)
- **Safe for**: 20+ other addons running simultaneously

## Getting Help

If you encounter issues after following this guide:

1. **Check FAQ section** in README.md
2. **Search existing issues** on GitHub
3. **Create a new issue** with:
   - WoW version
   - Full error message
   - Steps to reproduce
   - Screenshot if applicable

4. **Contact**
   - GitHub Issues: Best for bug reports
   - Discord (if available): For quick help

## Advanced: Installing from Source

For developers who want to modify the addon:

```bash
git clone https://github.com/YourUsername/Chatter.git
cd Chatter
# Make your changes...
# Test with: /reload in-game
# Commit and push to your fork
```

See CONTRIBUTING.md for development guidelines.

---

**Installation complete!** 🎉

Type `/chatter` to get started, or join a chat channel to see the addon in action.
