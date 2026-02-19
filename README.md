# bootstrap

A public repo to contain bootstrapping snippets.


- This will use [Chezmoi](https://www.chezmoi.io) to manage dotfiles, and continue the rest of the bootstrapping process.
- Some initialy depenencies are need, e.g. `git` to be able to retrieve the repository, ssh keys for authentication, and
  sshd for continuing the process remotely.

## Setup

### Dependencies

Install

```shell
sudo apt -qq update
sudo apt -qq install -y \
  git \
  openssh-server
``

Minimum configuration

```shell
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

### SSH key

Generate public/private key and output to add to GitLab/GitHub:

```shell
EMAIL="$USERNAME@$(hostname)"
ssh-keygen -t ed25519 -C "$EMAIL"

# < passphrase etc>

cat ~/.ssh/id_ed25519.pub
```

Add to:

- [GitHub: Add new SSH key](https://github.com/settings/ssh/new)

### Chezmoi

First use see [Quick start - chezmoi](https://www.chezmoi.io/quick-start/)

Subject to curl or wget availability:

```shell
sh -c "$(curl -fsLS get.chezmoi.io)" -- -b $HOME/.local/bin
sh -c "$(wget -qO- get.chezmoi.io)" -- -b $HOME/.local/bin

# Ensure chezmoi will be on the $PATH
export PATH="$PATH:/$HOME/.local/bin"
```

## Usage

```shell
GITHUB_USERNAME=mikegeeves
chezmoi init git@github.com:$GITHUB_USERNAME/dotfiles.git
```
