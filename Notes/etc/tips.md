# [!important] Shortcuts & Commands

## Obsidian

### Common Shortcuts

- **Quick find file:** `Ctrl + O`
- **Command template:** `Ctrl + P`
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
  git log --reverse --oneline (get commit history)
  ```

- **Export Git commit history:**

  ```sh
  git log --pretty=format:"%H|%an|%ad|%s" --date=iso > git-log-export.txt
  ```

- **Initialize Git Repository:**

  ```sh
  git init
  ```

- **Add Remote Repository:**

  ```sh
  git remote add origin https://github.com/your-username/your-repo.git
  ```

- **Stage All Files:**

  ```sh
  git add .
  ```

- **Commit Changes:**

  ```sh
  git commit -m "Initial commit"
  ```

- **Push to Remote Repository (Main Branch):**

  ```sh
  git push -u origin main
  ```

- **Push repo**
  - go to [token](https://github.com/settings/tokens) add then set repo permission
  - after git remote set-url origin https://<NEW-TOKEN>@github.com/

- **difference**

| Feature        | **SSH**                                                         | **GPG**                                                |
| -------------- | --------------------------------------------------------------- | ------------------------------------------------------ |
| **Purpose**    | Secure login/authentication                                     | Verifying commit authorship                            |
| **Usage**      | Used to authenticate **you** to GitHub (e.g., for pushing code) | Used to prove that **a commit** or tag was made by you |
| **Keys**       | SSH key pair (`id_rsa` / `id_ed25519`)                          | GPG key pair (used for signing)                        |
| **Where used** | Cloning, pushing, fetching (i.e., repository access)            | Signing commits/tags (i.e., author authenticity)       |

## Zotero

- zolit

## Anki

(No content yet)

## Neovim

### Tmux

- **Capitalize first letter of each word in selection:** ([Reference](https://stackoverflow.com/questions/17440659/capitalize-first-letter-of-each-word-in-a-selection-using-vim))

  ```sh
  s/\<./\u&/g
  ```

- **Toggle full pane in Tmux:** `<leader> + z` (toggle with same shortcut)
- **Check function documentation:** `Shift + K`
- **search current word:** `*`
- **use ) to move mouse outside** `)`
- **w go to next word start**
- **capital w e b for space**
- **snack manage buffer use** `ctrl + x`
- **zf for fold**
- **]] go to method**
- **mark use ' to destination**
- **sp and vsp**
- **resize**

### Plugins

- **Refresh:** `:luafile %` or `:Lazy reload plugin-name` or `Lazy sync`

### LSP

[nvim-lspconfig](https://github.com/neovim/nvim-lspconfig/blob/master/doc/configs.md)

#### close popup

```sh

local _select = vim.ui.select
function vim.ui.select(items, opts, on_choice)
    if
        opts
        and opts.prompt
        and type(opts.prompt) == "string"
        and string.match(opts.prompt, [[^You've reached.*limit.*Upgrade.*$]]) -- ...
    then
        vim.notify("Copilot: " .. opts.prompt, vim.log.levels.ERROR) --you can also delete this notify
        vim.cmd("Copilot disable")
    else
        return _select(items, opts, on_choice)
    end
end


```

## Ollama

- **Update model**

```sh
ollama ls | awk '{ print $1}' | grep -v NAME | xargs -I {} sh -c 'echo "Updating model: {}"; ollama pull {}; echo "—" && echo "All models updated."
```

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
- `Alt + Shift + .` → Increase font size
- `Alt + Shift + ,` → Decrease font size

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

## Qt

**gcc and clang**

```sh
cmake -B build -S . \
  -DCMAKE_C_COMPILER=clang \
  -DCMAKE_CXX_COMPILER=clang++ \
  -DCMAKE_EXPORT_COMPILE_COMMANDS=ON
```

**#ifdef error**

add .clangd

```sh
CompileFlags:
  Remove: [-mno-direct-extern-access]
Diagnostics:
  ClangTidy:
    Add: modernize-*,performance-*
```

## MPV

### **Playback Controls**

- `SPACE` → Pause/Resume
- `.` → Step forward one frame (pause mode)
- `,` → Step backward one frame (pause mode)
- `← / →` → Seek 5 seconds backward/forward
- `↑ / ↓` → Seek 1 minute backward/forward
- `Shift + ← / →` → Seek 1 second backward/forward
- `Ctrl + ← / →` → Seek 10 seconds backward/forward
- `Ctrl + ↑ / ↓` → Seek 10 minutes backward/forward
- `Backspace` → Restart video from beginning

### **Volume and Audio**

- `9 / 0` → Decrease/Increase volume
- `m` → Mute audio
- `#` → Cycle through audio tracks

### **Subtitles**

- `v` → Toggle subtitles
- `j / J` → Cycle forward/backward through subtitle tracks
- `z / Z` → Adjust subtitle delay (-/+ 0.1 sec)
- `r / t` → Increase/Decrease subtitle size

### **Video Settings**

- `f` → Toggle fullscreen
- `o` → Show playback time & progress
- `i` → Show video frame info
- `w / e` → Decrease/Increase contrast
- `s / d` → Decrease/Increase brightness
- `3 / 4` → Decrease/Increase gamma
- `5 / 6` → Decrease/Increase saturation
- `Ctrl + s` → Take a screenshot
- `Shift + s` → Screenshot without subtitles

### **Speed Control**

- `[` → Decrease playback speed
- `]` → Increase playback speed
- `{` → Halve playback speed
- `}` → Double playback speed
- `Backspace` → Reset playback speed

### **Looping and Playlist**

- `l` → Toggle looping current file
- `Shift + l` → Loop AB (start/end)
- `>` → Next file in playlist
- `<` → Previous file in playlist

### **Advanced**

- `p` → Show playlist
- `q` → Quit MPV
- `Shift + q` → Quit and remember playback position

## Other Tools

### rime

- **change input:** Type ctrl + ` to select

### Moze (Japanese Input)

- **Small characters:** Type `x` before the character (e.g., `x ょ` → `ょ`)
- **Type ん：** Double `n`
- **Transform あ->ア：** f6 or shift + alt then enter

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

### ffmpeg

- **Merge mp4 and m4a**

```sh
ffmpeg -i video.mp4 -i audio.m4a -acodec copy -vcodec copy output.mp4
 ```

### tar

- tar.gz

```sh
tar -xzvf filename.tar.gz
tar -czvf filename.tar.gz filename
```

### pid

```sh
btm # find cpu memory occupy
htop # find detailed information
```

## linux kernel

```sh
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

### ChatGPT

Program Prompt:
You are a top-tier programming expert known for clear, precise answers. When analyzing a provided text, identify complex or unclear sections and rewrite them for better clarity. Use relatable analogies to explain unfamiliar terms or concepts to a general audience. After answering, suggest at least one deep-dive question to help further explore the topic. Let’s think step by step to ensure accuracy. If a perfect solution is found, there’s a $200 tip! Thanks to the AI whisperers.

Economic Prompt:
You are an experienced financial advisor. Guide users through financial market concepts like inflation and return estimates, using long-term stock data to inform safe, tailored investment options based on their needs and interests. Begin with: “What is currently the best way to invest money from a short-term perspective?”

Academic Prompt:
Act as a scholar. Research a user-specified topic, structure the content clearly, and cite trustworthy sources. Your goal is to write an informative article or paper suitable for the audience. Start with: “I need help writing an article on modern trends in renewable energy generation targeting college students aged 18–25.”
