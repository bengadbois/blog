---
author: "Ben Gadbois"
date: 2018-04-13
title: "Tmux tricks"
weight: 10
---

<!--more-->

---
There's lots of resources on tmux configuration and commands. Here are some of the lesser known ones.

Note: the examples assume the default tmux config at `~/.tmux.conf`.

## New windows and panes start in the same path

If you are in `$HOME` and run `tmux`, every new window and pane will start in `$HOME`. However, if you `cd /long/path/to/working/area/` and open a new tmux window or pane, you may prefer to start off in `/long/path/to/working/area/`.

Adding this to your tmux config file will change the behavior so every new window will be in the originating window's path.

```
bind '"' split-window -c "#{pane_current_path}"
bind % split-window -h -c "#{pane_current_path}"
bind c new-window -c "#{pane_current_path}"
```

## Live reload the tmux config

If you are experimenting with changes in your tmux config file, you may prefer to not restart your tmux instance every time you make a change.

In your tmux config, add this:

```
unbind r
bind r source-file ~/.tmux.conf
```

Then you can `<tmux prefix> r` and the config will be reloaded. If there's an error, tmux will print something like `~/.tmux.conf:18: unknown command: sset` in the active pane and not apply.

Alternately, if you prefer to just type a shell command, you can run (inside your tmux session) `tmux source-file ~/.tmux.conf`.

## Increase tmux scrollback history

The number of lines saved in your tmux pane defaults to 2000. Sometimes that's not enough.

In your tmux config, add this:

```
set-option -g history-limit 10000
```

Only set it as large as you think you'll actually need, as tmux's RAM usage will be increased per window, even if not utilized (lines are pre-allocated).

## Put the tmux host's ip address in the statusline

If you already customize your status line, be aware you can include the output of arbitrary shell commands.

For example, in your tmux config, this will print your IP address:

```
set-option -g status-right '#(curl icanhazip.com)'
```

Note: there are non-empty default values for `status-left` and `status-right` that the above configuration would overwrite.

## Renaming sessions and windows

If you use multiple sessions and windows, they eventually become more difficult to keep track of.

By default, your tmux statusbar will display something like `[session name] 0:windowname 1:windowname 2:windowname 3:windowname` which may look like `[0] 0:bash 1:bash 2:vim 3:bash`.

You can rename the windows to something more meaningful, such as "code", "testing", "metrics", "notes", etc. The default shortcut to rename the current window is `<tmux prefix> ,` then you will be prompted inside the statusbar.

If you're at shell inside tmux already, you could instead run the command `tmux rename-window <new name>`. As with other shell commands, quote the new name if there's spaces.

Similarly to window renaming, the default session rename shortcut is `<tmux prefix> $`. Inside a shell that is `tmux rename-session <new name>`.

## Synchronize panes

If you have split into two or more panes, you can have your put key commands go to both panes.

For example if you have 3 panes, one in `/path1/`, one in `/path2/`, and one in `/path3/`, and you synchronize panes and run `touch test`, that will run in every pane, resulting in a `/path1/touch`, `/path2/touch`, and `/path3/touch`.

This can be helpful for a variety of cases such as comparing files, editing multiple files, running the same command on multiple hosts, and other one-off tasks that may take longer to script.

To enable via the statusbar run `<tmux prefix> :synchronize-panes on` or within a tmux shell `tmux set-window-option synchronize-panes on`. To disable, do the same but with `off` instead of `on`.

Newly created panes while synchronize-panes is enabled are also active.

## Zooming in on a single pane

Every time you split into a new pane, screen real estate is divided. If you need more space (e.g. long lines are wrapping), you can get a full screen view of a single pane without closing the others. This requires tmux 1.8 or higher.

The default command is `<tmux prefix> z` to zoom and the same command un-zoom.
