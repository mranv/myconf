# MyConfig Repository

This repository contains the configuration file for setting up a Zsh environment with various plugins and enhancements. The primary configuration file is `.zshrc`, which initializes and configures the Zsh shell with various plugins, themes, and settings.

## Repository URL

[https://github.com/mranv/myconfig](https://github.com/mranv/myconfig)

## Overview

The `.zshrc` file includes the following main sections:

1. **Powerlevel10k Instant Prompt**: Enables instant prompt for Powerlevel10k.
2. **Homebrew Initialization**: Initializes Homebrew if available.
3. **Zinit Configuration**: Sets up Zinit for managing Zsh plugins.
4. **Plugin and Snippet Loading**: Loads various Zsh plugins and Oh-My-Zsh snippets.
5. **Keybindings**: Custom keybindings for easier navigation and editing.
6. **History Settings**: Configures Zsh history behavior.
7. **Completion Styling**: Customizes the appearance and behavior of command completion.
8. **Aliases**: Defines useful command aliases.
9. **Shell Integrations**: Integrates additional tools like `fzf` and `zoxide`.
10. **Path Configuration**: Adds Node.js binaries to the PATH.
11. **Zinit Annexes**: Loads additional Zinit annexes for extended functionality.

## Detailed Configuration

### Powerlevel10k Instant Prompt

Enables instant prompt for Powerlevel10k, which should be placed close to the top of the `.zshrc` file to minimize prompt latency.

```zsh
if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi
```

### Homebrew Initialization

Initializes Homebrew shell environment if Homebrew is installed.

```zsh
if [[ -f "/opt/homebrew/bin/brew" ]]; then
  eval "$(/opt/homebrew/bin/brew shellenv)"
fi
```

### Zinit Configuration

Sets the directory for Zinit and clones it if not already present.

```zsh
ZINIT_HOME="${XDG_DATA_HOME:-${HOME}/.local/share}/zinit/zinit.git"

if [ ! -d "$ZINIT_HOME" ]; then
   mkdir -p "$(dirname $ZINIT_HOME)"
   git clone https://github.com/zdharma-continuum/zinit.git "$ZINIT_HOME"
fi

source "${ZINIT_HOME}/zinit.zsh"
```

### Plugin and Snippet Loading

Loads various plugins and snippets using Zinit.

```zsh
zinit ice depth=1; zinit light romkatv/powerlevel10k
zinit light zsh-users/zsh-syntax-highlighting
zinit light zsh-users/zsh-completions
zinit light zsh-users/zsh-autosuggestions
zinit light Aloxaf/fzf-tab

zinit snippet OMZP::git
zinit snippet OMZP::sudo
zinit snippet OMZP::archlinux
zinit snippet OMZP::aws
zinit snippet OMZP::kubectl
zinit snippet OMZP::kubectx
zinit snippet OMZP::command-not-found

autoload -Uz compinit && compinit

zinit cdreplay -q
```

### Keybindings

Custom keybindings for navigation and text manipulation.

```zsh
bindkey -e
bindkey '^p' history-search-backward
bindkey '^n' history-search-forward
bindkey '^[w' kill-region
```

### History Settings

Configures the shell history behavior for better usability.

```zsh
HISTSIZE=5000
HISTFILE=~/.zsh_history
SAVEHIST=$HISTSIZE
HISTDUP=erase
setopt appendhistory
setopt sharehistory
setopt hist_ignore_space
setopt hist_ignore_all_dups
setopt hist_save_no_dups
setopt hist_ignore_dups
setopt hist_find_no_dups
```

### Completion Styling

Customizes the appearance and behavior of command completion.

```zsh
zstyle ':completion:*' matcher-list 'm:{a-z}={A-Za-z}'
zstyle ':completion:*' list-colors "${(s.:.)LS_COLORS}"
zstyle ':completion:*' menu no
zstyle ':fzf-tab:complete:cd:*' fzf-preview 'ls --color $realpath'
zstyle ':fzf-tab:complete:__zoxide_z:*' fzf-preview 'ls --color $realpath'
```

### Aliases

Defines useful command aliases for common tasks.

```zsh
alias ls='ls --color'
alias vim='nvim'
alias c='clear'
```

### Shell Integrations

Integrates additional tools like `fzf` and `zoxide` into the shell.

```zsh
eval "$(fzf --zsh)"
eval "$(zoxide init --cmd cd zsh)"
```

### Path Configuration

Adds Node.js binaries to the system PATH.

```zsh
export PATH="/opt/homebrew/opt/node@20/bin:$PATH"
```

### Zinit Annexes

Loads additional Zinit annexes for extended functionality.

```zsh
zinit light-mode for \
    zdharma-continuum/zinit-annex-as-monitor \
    zdharma-continuum/zinit-annex-bin-gem-node \
    zdharma-continuum/zinit-annex-patch-dl \
    zdharma-continuum/zinit-annex-rust
```

## Customizing the Prompt

To customize the prompt, run `p10k configure` or edit `~/.p10k.zsh`.

## Conclusion

This `.zshrc` file is designed to provide a powerful and flexible Zsh environment with minimal setup. Feel free to customize it further to suit your needs. For more details, visit the repository at [MyConfig](https://github.com/mranv/myconfig).
