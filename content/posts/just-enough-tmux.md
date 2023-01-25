+++
title = "Just Enough tmux"
date = "2023-01-24T15:34:42-06:00"
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["tmux", "terminal"]
keywords = ["", ""]
description = "Learn just enough tmux to improve terminal efficiency."
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
ToC = true
+++

## Why tmux?
Many terminal emulators offer ways to create multiple tabs and multiple panes within each tab.

However, each emulator has its own particular keyboard shortcuts, which are not transferrable.

Using tmux lets you always have easy keyboard access to the functionality you need in any terminal emulator, on any platform.

There have been entire books published on tmux, but this post is all you need to get a ton of utility from this tool.

## Auto-starting tmux
To start a new tmux session automatically when opening a new terminal window, add the following to your `.bashrc` (or relevant shell startup file).

```bash
if [[ -z "$TMUX" ]]; then
  tmux new-session
fi
```

Alternatively, just use `tmux new-session` to start a tmux session in the current terminal window.

You can exit your tmux session by using the `exit` command or entering `Ctrl + d` (on Unix).

## A basic config
The config file goes in your `$HOME` directory and is named `.tmux.conf`.

All tmux keyboard shortcuts start with the "bind key", which defaults to `Ctrl + b`.

This line will let you quickly reload your tmux config while making tweaks:
```bash
# Reload tmux config file with shortcut Ctrl + b, r
bind r source-file ~/.tmux.conf \; display-message "tmux.conf reloaded"
```

## Adding vim-like shortcuts
To make tmux behave more like Vim, I like to add the following:
```bash
# Switch panes with vim directional shortcuts
bind h select-pane -L # Move to left pane with Ctrl + b, h
bind j select-pane -D # Move to lower pane with Ctrl + b, j
bind k select-pane -U## Move to upper pane with Ctrl + b, k
bind l select-pane -R # Move to right pane with Ctrl + b, l

# Resize panes with vim directional shortcuts
# In contrast to pane switching shortcuts, keep holding Ctrl or press it again
bind -r C-h resize-pane -L # Shrink left pane with Ctrl + b, Ctrl + h
bind -r C-j resize-pane -D # Shrink lower pane with Ctrl + b, Ctrl + j
bind -r C-k resize-pane -U # Shrink upper pane with Ctrl + b, Ctrl + k
bind -r C-l resize-pane -R # Shrink right pane with Ctrl + b, Ctrl + l

# Use vim movement keys when in copy mode
set-window-option -g mode-keys vi

# Emulate vim's visual mode in tmux copy mode
bind -T copy-mode-vi 'v' send -X begin-selection
bind -T copy-mode-vi 'V' send -X select-line
```


## Plugin manager
I like to install a plugin manager, mostly just to get `tmux-yank`, which lets me copy to the system clipboard from tmux's copy mode. You can install the `tpm` plugin manager using the official docs.

```bash
# tmux plugin manager
set -g @plugin 'tmux-plugins/tpm'

# tmux plugin to allow copying selected text in copy mode to system clipboard
set -g @plugin 'tmux-plugins/tmux-yank'

# Initialize tmux plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'
```

## Customizing the styles and the status bar
You can tweak the status bar to your heart's content. I like to keep it simple:
```bash
# Using Dracula theme colors

# Set status line background color (green)
set-option -g status-style fg=black,bg=#50fa7b

# Set active pane border (purple)
set-option -g pane-active-border-style fg=#bd93f9

# Set status line background when receiving message (red)
set-option -g message-style fg=black,bg=#ff5555

# Set emoji to appear on right side of status line
set -g status-right '💾 '
```

## Useful shortcuts

### Windows
Think of windows like "tabs" in your terminal.

Create new window: `Ctrl + b, n`

Rename current window: `Ctrl + b, ,`

Next window: `Ctrl + b, n`

Previous window: `Ctrl + b, p`

Select window by number: `Ctrl + b, 0..9`

Toggle last active window: `Ctrl + b, l`

### Panes
Split into vertical panes: `Ctrl + b, %`

Split into horizontal panes: `Ctrl + b, "`

Temporarily make pane take up whole window: `Ctrl + b, z`

Toggle pane layouts (resize/reorganize): `Ctrl + b, space`

Make pane into a new window: `Ctrl + b, !`

Kill pane: `Ctrl + b, x`

### General
List shortcuts: `Ctrl + b, ?`
