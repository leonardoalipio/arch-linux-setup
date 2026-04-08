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
# Add to fish
mkdir -p ~/.config/fish
echo 'source /opt/asdf-vm/asdf.fish' >> ~/.config/fish/config.fish
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

---

## Shell & Terminal

### Fish Shell

```bash
sudo pacman -S fish
chsh -s /usr/bin/fish
```

### Basic Config

```fish
# ~/.config/fish/config.fish

set -gx EDITOR "code --wait"
set -gx DOTNET_CLI_TELEMETRY_OPTOUT 1
set -gx ASPNETCORE_ENVIRONMENT Development
set -gx NODE_ENV development
```

### Plugins (Fisher)

```bash
curl -sL https://git.io/fisher | source && fisher install jorgebucaran/fisher
```

### Recommended Plugins

```bash
# autosuggestions + completions already built-in
fisher install IlanCosman/tide@v6   # prompt
fisher install PatrickF1/fzf.fish   # fzf integration
```

---

## SSH

```bash
ssh-keygen -t ed25519 -C "your@email.com" -f ~/.ssh/id_ed25519
```

```bash
eval "(ssh-agent -c)"
ssh-add ~/.ssh/id_ed25519
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

```fish
set -gx GOPATH $HOME/go
set -gx GOBIN $GOPATH/bin
set -gx PATH $PATH $GOBIN
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

### Aliases (fish)

```fish
alias update="sudo pacman -Syu"
alias cleanup="sudo pacman -Rns (pacman -Qtdq)"

alias g="git"
alias d="docker"

alias ..="cd .."
alias ll="ls -lah"
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
* [ ] Fish ready
