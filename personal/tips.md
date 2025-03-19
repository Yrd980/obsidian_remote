
# [!important] Shortcuts & Commands

## Obsidian

### Common Shortcuts
- **Quick find file:** `Ctrl + O`
- **Quick delete file:** Open command palette, search `Delete current file`
- **Open outline:** Open command palette, enter `Outline`
- **Disable spell check:** Go to `Settings` → `Editor` → Disable `Spell check`

### Plugins
- **Git**
- **Linter**

### Git Commands
- **Remove Ignored Files from Git Tracking:**
  ```sh
  git rm -r --cached .
  ```
- **Export Git commit history:**
  ```sh
  git log --pretty=format:"%H|%an|%ad|%s" --date=iso > git-log-export.txt
  ```

## Anki

(No content yet)

## Neovim with Tmux

- **Capitalize first letter of each word in selection:** ([Reference](https://stackoverflow.com/questions/17440659/capitalize-first-letter-of-each-word-in-a-selection-using-vim))
  ```sh
  s/\<./\u&/g
  ```
- **Document outline:** `<leader> + l + s`
- **Toggle full pane in Tmux:** `<leader> + z` (toggle with same shortcut)
- **Check function documentation:** `Shift + K`

## VSCode

- **Quick open file:** `Ctrl + P`
- **Fold sidebar:** `Ctrl + B`
- **Quick focus terminal:** Open command palette, search `Focus terminal`

## JetBrains IDEs

### General Shortcuts
- `Ctrl + Shift + A` → Find Action (search for commands/settings)
- `Shift` (twice) → Search Everywhere
- `Ctrl + E` → Recent Files
- `Ctrl + Shift + E` → Recent Edited Files
- `Alt + Enter` → Show Intention Actions / Quick Fix
- `Ctrl + Space` → Basic Code Completion
- `Ctrl + Shift + Space` → Smart Code Completion

### Navigation
- `Ctrl + N` → Go to Class
- `Ctrl + Shift + N` → Go to File
- `Ctrl + Alt + Shift + N` → Go to Symbol
- `Ctrl + B` / `Ctrl + Click` → Go to Definition
- `Ctrl + U` → Go to Super Method/Class
- `Ctrl + [ / Ctrl + ]` → Navigate to Code Block Start/End

### Editing
- `Ctrl + W` → Expand Selection
- `Ctrl + Shift + W` → Shrink Selection
- `Ctrl + D` → Duplicate Line
- `Ctrl + Y` → Delete Line
- `Ctrl + Shift + Up/Down` → Move Line Up/Down
- `Ctrl + /` → Toggle Line Comment
- `Ctrl + Shift + /` → Toggle Block Comment

### Refactoring
- `Shift + F6` → Rename
- `Ctrl + Alt + V` → Extract Variable
- `Ctrl + Alt + M` → Extract Method
- `Ctrl + Alt + F` → Extract Field

### Running & Debugging
- `Shift + F10` → Run
- `Shift + F9` → Debug
- `F8` → Step Over
- `F7` → Step Into
- `Shift + F8` → Step Out

## Other Tools

### Moze (Japanese Input)
- **Small characters:** Type `x` before the character (e.g., `x ょ` → `ょ`)
- **Type ん：** Double `n`

### iwgtk (WiFi Management)
- **Check WiFi passwords:**
  ```sh
  ls /var/lib/iwd
  ```

### Pacman (Arch Linux Package Manager)

- **Manually install a package:**
  ```sh
  yay -G package
  updpkgsums
  makepkg -si
  ```
- **Fix `yay` curl error (`HTTP server does not support byte ranges`):**
  ```sh
  yay -Scc
  ```

### Python
- **Use `uv` instead of `conda`**
- **Install PyTorch (CPU-only version):**
  ```sh
  pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu
  ```

### HP Printer Setup
- [Arch Linux Installation Guide](https://unix.stackexchange.com/questions/359531/installing-hp-printer-driver-for-arch-linux)

