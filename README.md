# VS Code Custom Keybindings - PyCharm Style

This document summarizes all custom keyboard shortcuts configured for VS Code to match PyCharm workflow.

## Table of Contents
- [Code Editing](#code-editing)
- [Navigation](#navigation)
- [File Management](#file-management)
- [Python Development](#python-development)
- [Panel & View Management](#panel--view-management)
- [Remote Development](#remote-development)
- [Installation](#installation)

---

## Code Editing

### Format Code
**Shortcut:** `Cmd+Option+L`  
**Original:** `Shift+Option+F`  
**Action:** Format the entire document or selected code  
**Requirements:** Black Formatter, autopep8, or yapf extension

### Organize Imports
**Shortcut:** `Cmd+Option+O`  
**Original:** No default binding  
**Action:** Sort and organize Python imports  
**Requirements:** isort extension  
**Conflicts Removed:** 
- `workbench.action.openRecent`
- `workbench.action.remote.showMenu`
- `editor.action.toggleColumnSelection`

### Remove Unused Imports
**Shortcut:** `Cmd+Alt+Shift+O`  
**Original:** No default binding  
**Action:** Organize imports and remove unused ones  
**Requirements:** isort extension

### Duplicate Line
**Shortcut:** `Cmd+D`  
**Original:** `Shift+Option+Down/Up`  
**Action:** Duplicate the current line  
**Conflicts Removed:** `editor.action.addSelectionToNextFindMatch`

### Quick Fix / Import Suggestions
**Shortcut:** `Option+Enter` (Alt+Enter)  
**Original:** `Cmd+.`  
**Action:** Show quick fixes, auto-import missing modules, fix errors  
**Requirements:** Python extension

---

## Navigation

### Go to Line
**Shortcut:** `Cmd+L`  
**Original:** `Ctrl+G`  
**Action:** Jump to a specific line number  
**Conflicts Removed:** `expandLineSelection`

### Go to Definition
**Shortcut:** `Cmd+B`  
**Original:** `F12` or `Cmd+Click`  
**Action:** Navigate to function/class definition  
**Conflicts Removed:** `workbench.action.toggleSidebarVisibility`

### Navigate Back (File History)
**Shortcut:** `Shift+Tab`  
**Original:** `Ctrl+-` (Control+Minus)  
**Action:** Go back to previously accessed file  
**Note:** Works like browser back button

### Navigate Forward (File History)
**Shortcut:** `Tab`  
**Original:** `Ctrl+Shift+-`  
**Action:** Go forward in navigation history  
**Note:** Only active when editor is focused, doesn't break autocomplete/snippets

### Cycle Through Open Files (Backward)
**Shortcut:** `Ctrl+Tab`  
**Original:** `Ctrl+Tab` (but cycled forward)  
**Action:** Cycle to previous file in tab order (left)

### Cycle Through Open Files (Forward)
**Shortcut:** `Ctrl+Shift+Tab`  
**Original:** `Ctrl+Shift+Tab` (but cycled backward)  
**Action:** Cycle to next file in tab order (right)

### Search in Files (Project-Wide)
**Shortcut:** `Cmd+Shift+F`  
**Original:** Same (unchanged)  
**Action:** Search across entire project directory

### Quick Open (File Finder)
**Shortcut:** `Cmd+E`  
**Original:** `Cmd+P`  
**Action:** Quick open file by name  
**Note:** Changed because `Cmd+P` is now used for parameter hints

---

## File Management

### Close Current Editor
**Shortcut:** `Cmd+W`  
**Original:** Same (unchanged)  
**Action:** Close the currently active file

---

## Python Development

### Run Python File
**Shortcut:** `Ctrl+R`  
**Original:** No default binding  
**Action:** Execute current Python file in terminal  
**Requirements:** Python extension

### Start/Continue Debugging
**Shortcut:** `Ctrl+D`  
**Original:** `F5`  
**Action:** Start debugging or continue when paused  
**Conflicts Removed:** `editor.action.addSelectionToNextFindMatch`

### Parameter Hints
**Shortcut:** `Cmd+P`  
**Original:** `Cmd+Shift+Space`  
**Action:** Show function parameter information  
**Conflicts Removed:** `workbench.action.quickOpen` (moved to `Cmd+E`)

---

## Panel & View Management

### Cycle Through Split Panes (Forward)
**Shortcut:** `Cmd+1`  
**Original:** No default binding (original `Cmd+1` opened first editor group)  
**Action:** Move focus to next editor pane (left to right)

### Cycle Through Split Panes (Backward)
**Shortcut:** `Cmd+Shift+1`  
**Original:** No default binding  
**Action:** Move focus to previous editor pane (right to left)

### Toggle Terminal
**Shortcut:** `Cmd+2`  
**Original:** `Ctrl+\`` (Control+Backtick)  
**Action:** Show/hide integrated terminal

### Focus Explorer (Project Tree)
**Shortcut:** `Cmd+3`  
**Original:** `Cmd+Shift+E`  
**Action:** Open and focus on file explorer sidebar

---

## Remote Development

### Rsync Entire Project to Server
**Shortcut:** `Cmd+Alt+Shift+X`  
**Original:** No default binding  
**Action:** Sync entire workspace to remote server  
**Requirements:** 
- SSH access configured
- rsync installed
- `.vscode/tasks.json` configured with server details

### Rsync Current File to Server
**Shortcut:** `Cmd+Alt+Shift+S`  
**Original:** No default binding  
**Action:** Sync only the currently open file to remote server  
**Context:** Only works when Explorer is visible and focused  
**Requirements:** Same as above

---

## Installation

### 1. Install Required Extensions

```bash
# Essential extensions
code --install-extension ms-python.python
code --install-extension ms-python.black-formatter
code --install-extension ms-python.isort

# Optional but recommended
code --install-extension ms-python.autopep8
```

### 2. Install Python Packages

```bash
pip install black isort
# Or if you prefer autopep8:
# pip install autopep8 isort
```

### 3. Apply Keybindings

**Option A: Via VS Code UI**
1. Press `Cmd+Shift+P`
2. Type "Preferences: Open Keyboard Shortcuts (JSON)"
3. Copy the contents of `keybindings.json`
4. Paste into your keybindings file
5. Save and reload VS Code (`Cmd+Shift+P` → "Developer: Reload Window")

**Option B: Direct File Copy**
```bash
# macOS
cp keybindings.json ~/Library/Application\ Support/Code/User/keybindings.json

# Linux
cp keybindings.json ~/.config/Code/User/keybindings.json

# Windows
cp keybindings.json %APPDATA%\Code\User\keybindings.json
```

### 4. Configure Python Path (Optional)

If you need to import from external repositories, add to `.vscode/settings.json`:

```json
{
  "python.analysis.extraPaths": [
    "${workspaceFolder}/../other-repo"
  ]
}
```

### 5. Configure Rsync Tasks (Optional)

Create `.vscode/tasks.json` in your project:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Rsync to Server",
      "type": "shell",
      "command": "rsync",
      "args": [
        "-avz",
        "--progress",
        "--exclude='node_modules'",
        "--exclude='__pycache__'",
        "--exclude='*.pyc'",
        "--exclude='.venv'",
        "--exclude='venv'",
        "${workspaceFolder}/",
        "username@server:/remote/path/${workspaceFolderBasename}/"
      ]
    },
    {
      "label": "Rsync Current File to Server",
      "type": "shell",
      "command": "rsync",
      "args": [
        "-avz",
        "--progress",
        "${file}",
        "username@server:/remote/path/${workspaceFolderBasename}/${relativeFile}"
      ]
    }
  ]
}
```

**Note:** Replace `username@server` and `/remote/path/` with your actual server details.

---

## File Locations

- **Keybindings:** `~/Library/Application Support/Code/User/keybindings.json` (macOS)
- **User Settings:** `~/Library/Application Support/Code/User/settings.json` (macOS)
- **Project Settings:** `<project>/.vscode/settings.json`
- **Project Tasks:** `<project>/.vscode/tasks.json`

---

## Quick Reference Card

| Action | Shortcut | Original |
|--------|----------|----------|
| Format Code | `Cmd+Option+L` | `Shift+Option+F` |
| Organize Imports | `Cmd+Option+O` | None |
| Remove Unused Imports | `Cmd+Alt+Shift+O` | None |
| Duplicate Line | `Cmd+D` | `Shift+Option+Down` |
| Quick Fix/Import | `Option+Enter` | `Cmd+.` |
| Go to Line | `Cmd+L` | `Ctrl+G` |
| Go to Definition | `Cmd+B` | `F12` |
| Navigate Back | `Shift+Tab` | `Ctrl+-` |
| Navigate Forward | `Tab` | `Ctrl+Shift+-` |
| Cycle Files ← | `Ctrl+Tab` | (reversed) |
| Cycle Files → | `Ctrl+Shift+Tab` | (reversed) |
| Search in Files | `Cmd+Shift+F` | Same |
| Quick Open | `Cmd+E` | `Cmd+P` |
| Close File | `Cmd+W` | Same |
| Run Python | `Ctrl+R` | None |
| Debug | `Ctrl+D` | `F5` |
| Parameter Hints | `Cmd+P` | `Cmd+Shift+Space` |
| Cycle Panes → | `Cmd+1` | None |
| Cycle Panes ← | `Cmd+Shift+1` | None |
| Toggle Terminal | `Cmd+2` | `Ctrl+\`` |
| Focus Explorer | `Cmd+3` | `Cmd+Shift+E` |
| Rsync Project | `Cmd+Alt+Shift+X` | None |
| Rsync File | `Cmd+Alt+Shift+S` | None |

---

## Notes

### Remote SSH Behavior
- Keybindings are stored **locally** and work the same in remote SSH sessions
- Extensions may need to be installed on the remote server
- Use `Remote-SSH` extension for seamless remote development

### Custom Variables
The following VS Code variables are used in tasks:
- `${workspaceFolder}` - Full path to workspace
- `${workspaceFolderBasename}` - Just the folder name
- `${file}` - Full path to current file
- `${relativeFile}` - File path relative to workspace
- `${fileBasename}` - Just the filename

### SSH Key Setup (for password-less rsync)
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your_email@example.com"

# Copy to server
ssh-copy-id username@server

# Test connection
ssh username@server
```

---

## Troubleshooting

### Imports not organizing
- Ensure `isort` is installed: `pip install isort`
- Reload VS Code: `Cmd+Shift+P` → "Developer: Reload Window"

### Formatting not working
- Install a formatter: `pip install black`
- Check default formatter in settings: `"[python]": { "editor.defaultFormatter": "ms-python.black-formatter" }`

### Rsync asking for password
- Set up SSH keys (see above)
- Verify SSH key is loaded: `ssh-add -l`

### Parameter hints not showing
- Ensure Python extension is installed
- Check that you're in a Python file
- Verify cursor is inside function parentheses

---

## Version History

- **v1.0** - Initial PyCharm-style keybindings configuration
  - All core editing, navigation, and Python development shortcuts
  - Remote development rsync tasks
  - Panel and view management shortcuts
