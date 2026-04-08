# 🐧 Arch Linux — Dev Setup

> Personal development environment setup guide.

---

## 📋 Index

* [Prerequisites](#prerequisites)
* [Package Managers](#package-managers)
* [Base Tools](#base-tools)
* [Git](#git)
* [Shell & Terminal](#shell--terminal)
* [SSH](#ssh)
* [Docker](#docker)
* [Go](#go)
* [.NET SDK](#net-sdk)
* [Node.js](#nodejs)
* [Editors & IDEs](#editors--ides)
* [Kubernetes](#kubernetes)
* [Dev Utilities](#dev-utilities)
* [User Configuration](#user-configuration)

---

## Prerequisites

Update system first:

```bash
sudo pacman -Syu
```

---

## Package Managers

### yay (AUR Helper)

```bash
sudo pacman -S --needed git base-devel
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
cd .. && rm -rf yay
```

### asdf (Version Manager)

```bash
yay -S asdf-vm
# Add to bash
echo '. /opt/asdf-vm/asdf.sh' >> ~/.bashrc
```

---

## Base Tools

```bash
sudo pacman -S --needed \
  base-devel \
  curl \
  wget \
  unzip \
  zip \
  htop \
  neofetch \
  tree \
  jq \
  ripgrep \
  fd \
  bat \
  fzf
```

---

## Git

```bash
sudo pacman -S git
```

### Global Config

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
git config --global core.editor "code --wait"
git config --global init.defaultBranch main
git config --global pull.rebase false
git config --global core.autocrlf input
```

### Useful Aliases

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.lg "log --oneline --graph --decorate --all"
git config --global alias.undo "reset --soft HEAD~1"
```

---

## Shell & Terminal

### Bash + Oh My Bash

```bash
sudo pacman -S bash

# Oh My Bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)"
```

### Plugins

Oh My Bash uses plugins via ~/.bashrc:

```bash
plugins=(git docker kubectl)
```

### Extra Plugin (autosuggestions-like)

```bash
# bash-completion (essential)
sudo pacman -S bash-completion

# ble.sh (advanced line editor + autosuggestions)
git clone --depth=1 https://github.com/akinomyoga/ble.sh.git ~/.ble.sh

echo '[[ $- == *i* ]] && source ~/.ble.sh/ble.sh' >> ~/.bashrc
```

### Starship Prompt (optional)

```bash
sudo pacman -S starship
echo 'eval "$(starship init bash)"' >> ~/.bashrc
```

---

## SSH

### Generate SSH Key

```bash
ssh-keygen -t ed25519 -C "your@email.com" -f ~/.ssh/id_ed25519
```

### SSH Agent

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

Auto start:

```bash
if [ -z "$SSH_AUTH_SOCK" ]; then
  eval "$(ssh-agent -s)" > /dev/null
  ssh-add ~/.ssh/id_ed25519 2>/dev/null
fi
```

---

## Docker

```bash
sudo pacman -S docker docker-compose
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker $USER
newgrp docker
```

---

## Go

```bash
sudo pacman -S go
```

### Env

```bash
export GOPATH=$HOME/go
export GOBIN=$GOPATH/bin
export PATH=$PATH:$GOBIN
```

---

## .NET SDK

```bash
sudo pacman -S dotnet-sdk aspnet-runtime
```

---

## Node.js

### via asdf

```bash
asdf plugin add nodejs
asdf install nodejs lts
asdf global nodejs lts
```

---

## Editors & IDEs

### VS Code

```bash
yay -S visual-studio-code-bin
```

---

## Kubernetes

```bash
sudo pacman -S kubectl k9s helm
```

---

## Dev Utilities

```bash
sudo pacman -S curl wget httpie tmux make
```

---

## User Configuration

### Env Vars

```bash
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8

export EDITOR="code --wait"

export DOTNET_CLI_TELEMETRY_OPTOUT=1
export ASPNETCORE_ENVIRONMENT=Development

export NODE_ENV=development
```

### Aliases

```bash
alias update="sudo pacman -Syu"
alias cleanup="sudo pacman -Rns $(pacman -Qtdq)"

alias g="git"
alias d="docker"

alias ..="cd .."
alias ll="ls -lah --color=auto"
```

### Reload

```bash
source ~/.bashrc
```

---

## ✅ Post-install Checklist

* [ ] System updated
* [ ] yay installed
* [ ] git configured
* [ ] SSH working
* [ ] docker without sudo
* [ ] Go configured
* [ ] .NET installed
* [ ] Node via asdf
* [ ] VS Code installed
* [ ] Bash + Oh My Bash ready
