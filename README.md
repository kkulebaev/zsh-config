# zsh-config

Personal zsh configuration for Fedora Linux, built on Oh My Zsh with the Spaceship prompt.

## Stack

- **Shell:** zsh 5.9+
- **Framework:** [Oh My Zsh](https://ohmyz.sh/)
- **Theme:** [Spaceship Prompt](https://spaceship-prompt.sh/)
- **Plugins:** `git`, `zsh-autosuggestions`, `zsh-completions`, `zsh-syntax-highlighting`

## Installation

### 1. Install zsh and Oh My Zsh

```bash
sudo dnf install zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
chsh -s "$(which zsh)"
```

### 2. Install the Spaceship theme

Run inside a zsh session (so `$ZSH_CUSTOM` resolves):

```bash
git clone https://github.com/spaceship-prompt/spaceship-prompt.git \
  "$ZSH_CUSTOM/themes/spaceship-prompt" --depth=1
ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" \
  "$ZSH_CUSTOM/themes/spaceship.zsh-theme"
```

### 3. Install completion / suggestion plugins

```bash
git clone --depth=1 https://github.com/zsh-users/zsh-autosuggestions \
  "$ZSH_CUSTOM/plugins/zsh-autosuggestions"
git clone --depth=1 https://github.com/zsh-users/zsh-completions \
  "$ZSH_CUSTOM/plugins/zsh-completions"
git clone --depth=1 https://github.com/zsh-users/zsh-syntax-highlighting.git \
  "$ZSH_CUSTOM/plugins/zsh-syntax-highlighting"
```

`zsh-syntax-highlighting` must stay last in the `plugins=(...)` list.

### 4. Link this `.zshrc`

```bash
git clone git@github.com:kkulebaev/zsh-config.git ~/develop/zsh-config
ln -sf ~/develop/zsh-config/.zshrc ~/.zshrc
exec zsh
```

## Aliases

### Files

| Alias   | Command                  |
| ------- | ------------------------ |
| `scp`   | `scp -r`                 |
| `mkdir` | `mkdir -p`               |
| `ls`    | `ls -F --color=auto`     |
| `la`    | `ls -A --color=auto`     |
| `ll`    | `ls -l --color=auto -h`  |
| `lla`   | `ll -A --color=auto -h`  |
| `grep`  | `grep --color=auto`      |
| `open`  | `xdg-open .`             |

### System info

| Alias | Command                  |
| ----- | ------------------------ |
| `n`   | `neofetch`               |
| `k`   | `uname -rs`              |
| `g`   | `gnome-shell --version`  |
| `f`   | `lsb_release -sd`        |

### Music

| Alias  | Command                                                  |
| ------ | -------------------------------------------------------- |
| `lofi` | `mpv --volume=40 https://play.streamafrica.net/lofiradio` |

Requires `mpv` (`sudo dnf install mpv`). Controls during playback: `9`/`0` — volume down/up, `m` — mute, `q` — quit.

## Toolchain PATH

The config exports PATHs for these tools. Each block is harmless if you never use the tool, but the cargo line expects Rust to be installed via `rustup`:

| Tool  | PATH / source             |
| ----- | ------------------------- |
| Bun   | `$HOME/.bun/bin`          |
| pnpm  | `$HOME/.local/share/pnpm` |
| Cargo | `$HOME/.local/bin/env`    |

If you don't have Rust, either install rustup or guard the line:

```bash
[ -f "$HOME/.local/bin/env" ] && . "$HOME/.local/bin/env"
```

## Updating

```bash
cd ~/develop/zsh-config
git pull
exec zsh
```
