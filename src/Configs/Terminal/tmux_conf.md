# Tmux

```
#       =====Tmux Plugins w/ tpm=====   #
#       =====Prefix + I to install===== #

set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'tmux-plugins/tmux-resurrect'
set -g @plugin 'tmux-plugins/tmux-continuum'
set -g @plugin 'nhdaly/tmux-better-mouse-mode'
set -g @plugin 'tmux-plugins/tmux-pain-control'
set -g @plugin 'dracula/tmux'


#       =====Plugin Options=====        #

#set -g @resurrect-capture-pane-contents 'on'
#set -g @continuum-restore 'on'

set -g @dracula-cpu-usage true
set -g @dracula-ram-usage true
set -g @dracula-gpu-usage true
set -g @dracula-day-month true
set -g @dracula-show-powerline true
set -g @dracula-show-left-icon session
set -g @dracula-show-location false

#       =====Enable Mouse Mode=====     #

set -g mouse on
#set -g mouse-select-window on
#set -g mouse-select-pane on
#set -g mouse-resize-pane on

#       =====Swap Hot Keys=====         #

set -g prefix C-a
unbind-key C-b
bind-key C-a send-prefix

set -g focus-events on

#bind-key -n C-Tab next-window
#bind-key -n C-S-Tab previous-window

# (Depending on the Tmux Version, these might need to be un-escaped.)
bind \| split-window -h -c '#{pane_current_path}'
bind \\ split-window -h -c '#{pane_current_path}'
bind \- split-window -v -c '#{pane_current_path}'
bind \_ split-window -v -c '#{pane_current_path}'

unbind-key C-z
set -s escape-time 0

# Start windows and panes at 1, not 0
set -g base-index 1
setw -g pane-base-index 1

# Other examples:
# set -g @plugin 'github_username/plugin_name'
# set -g @plugin 'git@github.com/user/plugin'
# set -g @plugin 'git@bitbucket.com/user/plugin'

set -g default-terminal "tmux-256color"

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run -b '~/.tmux/plugins/tpm/tpm'
```
