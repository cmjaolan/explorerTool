# AI Assistant Instructions

This document provides guidance for AI coding assistants working with ExplorerBgTool, a Windows Explorer background customization tool.

## Project Overview

ExplorerBgTool is a Windows shell extension that:
- Enables custom background images for File Explorer in Windows 10/11
- Supports file dialog customization
- Implements background image positioning and transparency control
- Allows path-specific background configurations

### Key Components
- Shell Extension DLL (`ExplorerBgTool.dll`) - Core functionality
- Configuration System (`config.ini`) - User settings management
- Image Management (`Image/` directory) - Background resource handling
- Registration Scripts (`注册_Register.cmd`, `卸载_Uninstall.cmd`) - Installation handling

## Development Workflow

### Building
The project requires:
1. Windows SDK for shell extension development
2. C++ development environment
3. Resource compilation tools for DLL resources

### Testing
Test changes by:
1. Unregistering existing DLL: `regsvr32 /u "path/to/ExplorerBgTool.dll"`
2. Building new DLL
3. Registering new version: `regsvr32 "path/to/ExplorerBgTool.dll"`
4. Restarting Explorer windows

## Code Patterns

### Configuration Format
Config files use INI format with sections:
```ini
[load]
folderExt=true/false  # Dialog extension
noerror=true/false    # Error handling

[style]
posType=1-6          # Position types (3=bottom-right, 4=center, 6=zoom/fill)
imgAlpha=0-255       # Transparency
```

### Image Handling
- Place images in `Image/` directory
- Support multiple images for random selection
- Handle transparency and positioning via `posType` settings

## Integration Points

### Shell Extension Integration
- COM registration via `regsvr32`
- Explorer interface implementation
- Dialog extension handling through `folderExt` setting

### File System Integration
- Path-specific background configuration support
- Image file loading and caching
- Directory monitoring for changes

## Key Files
- `ExplorerBgTool.dll` - Main extension binary
- `config.ini` - Configuration settings
- `Image/` - Background image resources
- Registration scripts for installation management

## Debugging Tips
1. Enable error popups by setting `noerror=false`
2. Test in isolated Explorer windows
3. Check Windows Event Viewer for COM registration issues
4. Use Process Monitor to verify DLL loading

---
Note: Update this document as new features or patterns are added to the codebase.