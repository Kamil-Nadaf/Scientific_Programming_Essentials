# Vim Editor Basics

Vim is a powerful text editor that operates in different modes, primarily:

- **Normal mode**: For navigation and executing commands (default mode when Vim starts).
- **Insert mode**: For inserting or editing text.


## Basic Operations

- **Open or create a file**: Opens an existing file or creates a new one. 
  ```bash
  vim file.extension
  ```
  **Example** vim file.txt, file.py etc.

- **Enter insert mode**: Starts editing text at the cursor’s position.
  ```bash
  i
  ```

- **Exit insert mode**: Returns to normal mode.
  ```bash
  Esc
  ```

- **Save the file**: Saves changes without exiting (use in normal mode).
  ```bash
  :w
  ```

- **Save and exit**: Saves changes and quits Vim (use in normal mode).
  ```bash
  :wq
  ```

- **Exit without saving**: Discards changes and quits Vim (use in normal mode).
  ```bash
  :q!
  ```

## Additional Commonly Used Commands

These commands enhance your efficiency in Vim:

### Navigation
- `h`: Move cursor left
- `j`: Move cursor down
- `k`: Move cursor up
- `l`: Move cursor right
- `w`: Jump to the start of the next word
- `b`: Jump to the start of the previous word

### Editing
- `x`: Delete the character under the cursor
- `dd`: Delete the current line
- `u`: Undo the last action
- `Ctrl + r`: Redo the last undone action

### Copy and Paste
- `yy`: Copy (yank) the current line
- `p`: Paste copied text after the cursor
- `P`: Paste copied text before the cursor

### Search and Replace
- `/pattern`: Search for "pattern" in the file (press Enter, then `n` for next occurrence)
- `:s/old/new/g`: Replace all occurrences of "old" with "new" in the current line
- `:%s/old/new/g`: Replace all occurrences of "old" with "new" in the entire file

### Visual Mode
- `v`: Enter visual mode to select text (use `h`, `j`, `k`, `l` to highlight)
- In visual mode:
  - `y`: Copy the selected text
  - `d`: Delete the selected text

### Help
- `:help`: Open Vim’s built-in help system
- `:help command`: Get help on a specific command (e.g., `:help :w`)

### Final Remarks
Vim’s learning curve can be steep, but these commands provide a solid foundation. 