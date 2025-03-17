> [!important] shortcuts
> command palette can hint it

# obsidian

## common shortkeys

quick find file: ctrl + o
quick delete file : use command  terminal then choose delete current file
open outline: in command palette: enter outline
disable spell check:  go settings then editer find spell check

## plugins

git
linter

# anki

# neovim with tmux

[Capitalize first letter of each word in a selection](https://stackoverflow.com/questions/17440659/capitalize-first-letter-of-each-word-in-a-selection-using-vim)

```bash
s/\<./\u&/g
```

document ouline: leader + l + s
specifying Full Pane in Tmux Window: leader + z recovery is same

check code document: capital k

# vscode

quick open file: ctrl+p
fold sidebar: ctrl+b
quick focus: command then focus terminal

# other

# moze

x then  small like ょ
double type n then ん

## iwgtk

check wifi password
```bash
ls /var/lib/iwd
```

## pacman

mannul install

```bash
yay -G package
updpkgsums
makepkg -si
```

yay occur curl: (33) HTTP server does not seem to support byte ranges. Cannot resume.

the error occurs because yay is trying to resume a partial download of the Elasticsearch package, but the server does not support byte ranges, leading to a failure.

```shell
yay -Scc
```

## python

**uv** instead **conda**

torch (cpu)
```shell
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu
```

### Hp printer

[Arch install](https://unix.stackexchange.com/questions/359531/installing-hp-printer-driver-for-arch-linux)
