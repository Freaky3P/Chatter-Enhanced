# Contributing to Chatter (Modified)

Thank you for your interest in contributing to this project! This document provides guidelines for contributions.

## Code of Conduct

- Be respectful and constructive in all interactions
- Focus on the code, not the person
- Help others learn and improve

## How to Contribute

### Reporting Bugs

**Before reporting**, check if the issue already exists.

**Include in your bug report:**
1. WoW version (e.g., 3.3.5a)
2. Server type (private/retail)
3. Steps to reproduce
4. Expected behavior vs. actual behavior
5. Screenshots or error messages (use BugSack for Lua errors)
6. Addon list if you suspect conflicts

**Example:**
```
Title: Copy window truncates at 1MB
- WoW Version: 3.3.5a (Wrath)
- Server: Private server
- Steps:
  1. Generate ~5000 chat messages
  2. Click copy icon
  3. Copy window cuts off
- Expected: Full message history
- Actual: Only first 1MB visible
```

### Suggesting Enhancements

**Provide context:**
1. What problem does this solve?
2. Is this widely requested?
3. How would a user access this feature?
4. Performance considerations?

**Example:**
```
Title: Add export to .txt file
Description: Some players want to save chat logs. 
Proposed: Add "Export to File" button in copy window
```

### Submitting Pull Requests

1. **Fork** the repository
2. **Create a branch**: `git checkout -b feature/your-feature-name`
3. **Make changes** with clear commit messages
4. **Test thoroughly** in WoW before submitting
5. **Submit PR** with description of changes

**PR Guidelines:**
- One feature per PR (keep it focused)
- Add comments for complex logic
- Follow existing code style
- Test on 3.3.5a before submitting
- Reference related issues

**PR Template:**
```
## Description
Brief summary of changes

## Related Issues
Fixes #(issue number)

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Enhancement
- [ ] Documentation

## Testing
How was this tested? Include steps to reproduce.

## Performance Impact
Any performance considerations?
```

## Development Setup

### File Structure
```
Chatter/
├── Chatter.lua              # Main addon file
├── Chatter.toc              # Table of contents
├── Modules/                 # Feature modules
│   ├── CopyChat.lua         # Copy functionality
│   ├── AltNames.lua         # Alt linking
│   └── ...
├── Libs/                    # Ace3 libraries
└── Localization/            # Language files
```

### Testing Checklist
Before submitting changes:
- [ ] Test on clean 3.3.5a WoW install
- [ ] No Lua errors in BugSack
- [ ] All related features work
- [ ] No memory leaks (check addmemoryusage)
- [ ] No performance degradation
- [ ] Test with other popular addons

### Code Style

**Follow existing patterns:**
```lua
-- Use 'local' for all variables
local mod = Chatter:NewModule("Module Name")

-- Comment non-obvious logic
function mod:SomeFunction()
    -- This is necessary because...
    if condition then
        -- Do something
    end
end

-- Use meaningful variable names
local chatFrame = _G["ChatFrame" .. i]

-- Avoid globals unless necessary
local function privateHelper()
    -- Only used internally
end
```

## Branches

- `main` - Stable releases, production-ready
- `develop` - Development branch for next release
- `feature/*` - Individual features
- `bugfix/*` - Bug fixes
- `docs/*` - Documentation updates

## Commit Messages

```
[Type] Brief description (50 chars max)

Detailed explanation if needed.
- Point 1
- Point 2

Fixes #(issue number)
```

**Types:**
- `[Fix]` - Bug fixes
- `[Feature]` - New features
- `[Enhance]` - Improvements to existing features
- `[Docs]` - Documentation
- `[Refactor]` - Code cleanup without behavior change

## Review Process

1. **Automated checks** (linting, style)
2. **Code review** (functionality, performance, style)
3. **Testing verification** (manual testing on 3.3.5a)
4. **Merge** once approved

## Questions?

- Check existing issues and discussions first
- Ask in comments on related issues
- Be patient - maintainers are volunteers

## License

By contributing, you agree that your contributions will be licensed under the same license as the project.

---

**Thank you for helping make Chatter better!** 🎉
