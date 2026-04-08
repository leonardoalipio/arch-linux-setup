# 🐧 Arch Linux — Dev Setup

> Personal development environment setup guide.

## Prerequisites:
* ### Update system first:
```bash
sudo pacman -Syu
```

* ### Base Tools:
```bash
sudo pacman -S --needed git base base-devel git sudo vim curl wget unzip zip htop fastfetch tree jq ripgrep fd bat fzf exa direnv
```

## If is for WSL
* ### Criar usuário (não usa root, óbvio)
```bash
useradd -m -G wheel -s /bin/bash leonardo
passwd leonardo
```

* ### Libera sudo:
```bash
EDITOR=vim visudo
```
* ### Descomenta:
```bash
%wheel ALL=(ALL:ALL) ALL
```

* ### Definir usuário padrão no WSL
```bash
echo "[user]
default=leonardo" > /etc/wsl.conf
```

* ### Depois no Windows:
```bash
wsl --shutdown
```

# Package Managers:

* ### yay (AUR Helper)
```bash
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
cd .. && rm -rf yay
```

## Git - Global Config

```bash
git config --global user.name "Leonardo Alípio"
git config --global user.email "leo.alipio@live.com"
git config --global core.editor "code --wait"
git config --global init.defaultBranch main
git config --global pull.rebase false
git config --global core.autocrlf input
```

## SSH
```bash
ssh-keygen -t ed25519 -C "your@email.com" -f ~/.ssh/id_ed25519
```

```bash
eval "(ssh-agent -c)"
ssh-add ~/.ssh/id_ed25519
```

## Shell & Terminal
* ### Zsh Shell

```bash
sudo pacman -S zsh
chsh -s /usr/bin/zsh
```

* ### Basic Config

```bash
# ~/.zshrc
#loop to add n folders contains bin to run

for dir in "$HOME/.local/bin" "$HOME/bin"; do
  if [[ ":$PATH:" != *":$dir:"* ]]; then
    PATH="$dir:$PATH"
  fi
done
export PATH

```

* ### Config Plugins Zsh + oh-my-zsh + pk10
```bash
# oh my zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

#PowerLevel10K
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git \
${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

#Edita ~/.zshrc:
echo 'ZSH_THEME="powerlevel10k/powerlevel10k"' >>~/.zshrc

# autosuggestions
git clone https://github.com/zsh-users/zsh-autosuggestions \
${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# syntax highlighting
git clone https://github.com/zsh-users/zsh-syntax-highlighting \
${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

# completions
git clone https://github.com/zsh-users/zsh-completions \
${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-completions

#No ~/.zshrc:
plugins=(
  git
  zsh-autosuggestions
  zsh-syntax-highlighting
  zsh-completions
)
```

* ### Fonts
```bash
sudo pacman -S ttf-jetbrains-mono-nerd
```


* ### asdf (Version Manager)
```bash
yay -S asdf-vm
```


## Docker

```bash
sudo pacman -S docker docker-compose
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker $USER
newgrp docker
```


## Go

```bash
sudo pacman -S go
```

## .NET SDK

```bash
sudo pacman -S dotnet-sdk aspnet-runtime
```

## Node.js
* ### via asdf

```bash
asdf plugin add nodejs
asdf install nodejs lts
asdf global nodejs lts
```

## Editors & IDEs

```bash
yay -S visual-studio-code-bin
```

## Kubernetes

```bash
sudo pacman -S kubectl k9s helm
```

## Dev Utilities

```bash
sudo pacman -S curl wget httpie tmux make
```

## User Configuration

* ### bindkeys (zsh)

```bash
#the end of file .zshrc:
bindkey -e

# delete
bindkey '^[[3~' delete-char

# home/end
bindkey '^[[H' beginning-of-line
bindkey '^[[F' end-of-line

# ctrl arrows (opcional)
bindkey '^[[1;5C' forward-word
bindkey '^[[1;5D' backward-word

# prevents timing bug
export KEYTIMEOUT=50
```

* ### Aliases (zsh)

```bash
# Performance
DISABLE_UPDATE_PROMPT=true
DISABLE_AUTO_UPDATE=true

# Histórico melhor
HISTSIZE=10000
SAVEHIST=10000
setopt HIST_IGNORE_ALL_DUPS
setopt SHARE_HISTORY

# Melhor navegação
setopt AUTO_CD
setopt CORRECT

# Alias úteis
alias ll='ls -lah'
alias gs='git status'
alias ga='git add'
alias gc='git commit'
alias gp='git push'
alias gl='git pull'

# .NET
alias build='dotnet build'
alias run='dotnet run'

# Node
alias ni='npm install'
alias ns='npm start'
```