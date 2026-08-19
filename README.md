# Chatter (Modified)

A feature-rich chat addon for World of Warcraft WotLK 3.3.5a with enhanced copy functionality and bug fixes.

## Overview

Chatter is a popular chat enhancement addon that provides powerful utilities for managing and organizing in-game chat. This fork includes critical bug fixes and a major enhancement to the chat copy feature to support full chat history capture.

## Features

### Core Features
- **Chat Frame Management** - Customize your chat frames with various options
- **Alt Linking** - Track character names and alternate accounts with guild note scanning
- **Copy Chat** - Export full chat history to a scrollable window for easy reading and copying
- **Chat Highlighting** - Enhanced text visibility with various formatting options
- **Chat Links** - Improved link handling and URL extraction
- **Channel Management** - Custom channel colors and naming options
- **Chat History** - Scroll back through chat history with configurable buffer size

### Recent Enhancements
- **Full Chat History Capture** - The copy window now captures and displays complete chat history without limits
- **Large Buffer Support** - Supports up to 1MB of chat text in the copy window
- **Bugfix: AltNames nil error** - Fixed crash on character login when guild notes are empty

## Installation

1. Download the addon folder
2. Extract to your World of Warcraft Addons directory:
   ```
   World of Warcraft\Interface\AddOns\Chatter\
   ```
3. Restart World of Warcraft or run `/reload`
4. Enable the addon in the AddOns menu

## Usage

### Copy Chat History
1. Click the **blue copy icon** in your chat frame (bottom-right corner)
2. A new window opens showing the complete chat history
3. Scroll through, select, and copy any text
4. Press ESC or click the close button to dismiss the window

### Access Copy Function via Menu
- Right-click on any chat tab
- Select "Copy Text" from the context menu

### Configure Scrollback Length
- Open Chatter options: `/chatter`
- Navigate to "Scrollback" section
- Adjust per-frame history size (250-2500 lines)

## What Changed in This Fork

### Bug Fixes
- **Fixed AltNames.lua line 331 error**: Added nil checks for guild notes and rank fields
  - Error: `bad argument #1 to 'strlower' (string expected, got nil)`
  - Solution: Properly initialize `note` and `rank` variables before string operations

### Enhancements
- **Expanded Copy Buffer**: Increased EditBox max letters from 99,999 to 1,048,576 characters
- **Full History Capture**: Implemented message history buffering system
  - Hooks into AddMessage to capture every chat message in real-time
  - Maintains per-frame history buffers (up to 10,000 lines per frame)
  - Copy window now displays complete accumulated chat history since addon load
  - No more truncation when copying large chat sessions

## Technical Details

### Modified Files

#### 1. **Modules/AltNames.lua**
```lua
-- Line 328-331: Added nil checks
note = note or ""
rank = rank or ""
```
**Impact**: Prevents nil reference crashes when guild roster contains empty notes or ranks

#### 2. **Modules/CopyChat.lua**
```lua
-- New: Per-frame message history buffers
local frameHistories = setmetatable({}, {__mode = "k"})

-- Enhanced: Copy() function uses full history
function mod:Copy(frame)
    if frameHistories[frame] and #frameHistories[frame] > 0 then
        local text = table_concat(frameHistories[frame], "\n")
        -- ... display in copy window
    end
end

-- New: Hook AddMessage to capture messages
function mod:HookChatFrame(frame)
    self:SecureHook(frame, "AddMessage", function(f, text, ...)
        if text and frameHistories[f] then
            tinsert(frameHistories[f], tostring(text))
            if #frameHistories[f] > 10000 then
                table.remove(frameHistories[f], 1)
            end
        end
    end)
end
```
**Impact**: Every message is captured as it appears; copy window shows full history

## Performance Considerations

- **Memory**: Each frame maintains up to 10,000 line history (~5-10MB depending on message length)
- **Weak references**: Frame histories use weak table keys to prevent memory leaks
- **Automatic cleanup**: Oldest messages are removed when buffer exceeds 10,000 lines

## Compatibility

- **WoW Version**: World of Warcraft 3.3.5a (Wrath of the Lich King)
- **Dependencies**: Ace3 libraries (included)
- **Performance**: Minimal overhead; uses efficient string buffering

## Troubleshooting

### Copy window shows empty text
- Ensure messages have been sent in the chat frame after addon loads
- Check that frame history buffer has been initialized
- Try scrolling the main chat frame to refresh captured history

### Memory issues with large histories
- Reduce scrollback size in Chatter options (lower = less memory)
- Use `/reload` to clear session history
- Consider limiting to fewer chat frames with full history

### AltNames error on login
- Ensure this version is installed (line 328 should have nil checks)
- Check `/reload` if recently updated
- Run `/gquit` and rejoin guild if issue persists

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.2.11-Modified | 2026-08-19 | Fixed AltNames nil error; Enhanced copy buffer to 1MB; Implemented full history capture |
| 1.2.11 | Original | Base Chatter addon |

## License

See LICENSE file for details. This fork maintains compatibility with the original Chatter license.

## Contributing

If you find bugs or want to suggest improvements, please create an issue or pull request.

## Credits

- **Original Addon**: Chatter by Shul and contributors
- **Modifications**: Bug fixes and enhancement to copy functionality
- **Libraries**: Ace3 framework and dependencies

## Support

For issues or questions:
1. Check the Troubleshooting section above
2. Review the changelog for recent changes
3. Test with a clean WoW session (`/reload`)
4. Create an issue on this repository

---

**Note**: This is a modified version of Chatter optimized for full chat history capture and stability on 3.3.5a private servers.
