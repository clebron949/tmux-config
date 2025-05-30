# Tmux Config

Tmux configuration for me :)

### Install tpm

```shell
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

## Config

```
set -g default-terminal "screen-256color"
set -g mouse on

#set-option -g status-position top
set-option -g base-index 1
set-option -g pane-base-index 1
set-option -g history-limit 10000
set-option -g set-titles on
set-option -g set-titles-string '#{pane_title}'

unbind r
bind r source-file ~/.tmux.conf

set -g prefix C-a
unbind C-b
bind C-a send-prefix

bind c new-window -c "#{pane_current_path}"

unbind %
bind | split-window -h -c "#{pane_current_path}"

unbind '"'
bind - split-window -v -c "#{pane_current_path}"

bind-key -r j resize-pane -D 5
bind-key -r k resize-pane -U 5
bind-key -r l resize-pane -R 5
bind-key -r h resize-pane -L 5

set-option -s focus-events on
set-option -s extended-keys on
set-option -s escape-time 0

bind -r m resize-pane -Z

#Styles
#set-option -g status-style bg=default
#set-option -g status-justify centre

# List of plugins

set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'christoomey/vim-tmux-navigator'
set -g @plugin 'catppuccin/tmux#v2.1.3'

set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-online-status'
set -g @plugin 'tmux-plugins/tmux-battery'
set -g @plugin 'catppuccin/tmux'

# Configure Catppuccin

set -g @catppuccin_flavor "macchiato"
set -g @catppuccin_status_background "none"
set -g @catppuccin_window_status_style "none"
set -g @catppuccin_pane_status_enabled "off"
set -g @catppuccin_pane_border_status "off"

# Configure Online

set -g @online_icon "ok"
set -g @offline_icon "nok"

# status left look and feel

set -g status-left-length 100
set -g status-left ""
set -ga status-left "#{?client_prefix,#{#[bg=#{@thm_red},fg=#{@thm_bg},bold]  #S },#{#[bg=#{@thm_bg},fg=#{@thm_green}]  #S }}"
set -ga status-left "#[bg=#{@thm_bg},fg=#{@thm_overlay_0},none]│"
set -ga status-left "#[bg=#{@thm_bg},fg=#{@thm_maroon}]  #{pane_current_command} "
set -ga status-left "#[bg=#{@thm_bg},fg=#{@thm_overlay_0},none]│"
set -ga status-left "#[bg=#{@thm_bg},fg=#{@thm_blue}]  #{=/-32/...:#{s|$USER|~|:#{b:pane_current_path}}} "
set -ga status-left "#[bg=#{@thm_bg},fg=#{@thm_overlay_0},none]#{?window_zoomed_flag,│,}"
set -ga status-left "#[bg=#{@thm_bg},fg=#{@thm_yellow}]#{?window_zoomed_flag,  zoom ,}"

# status right look and feel

set -g status-right-length 100
set -g status-right ""
set -ga status-right "#[bg=#{@thm_bg}]#{?#{==:#{online_status},ok},#[fg=#{@thm_mauve}] 󰖩 on ,#[fg=#{@thm_red},bold]#[reverse] 󰖪 off }"
set -ga status-right "#[bg=#{@thm_bg},fg=#{@thm_overlay_0}, none]│"
set -ga status-right "#[bg=#{@thm_bg},fg=#{@thm_blue}] 󰭦 %Y-%m-%d 󰅐 %I:%M %p "

# bootstrap tpm

if "test ! -d ~/.tmux/plugins/tpm" \
 "run 'git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm && ~/.tmux/plugins/tpm/bin/install_plugins'"

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)

run '~/.tmux/plugins/tpm/tpm'

# Configure Tmux

set -g status-position top
set -g status-style "bg=#{@thm_bg}"
set -g status-justify "absolute-centre"

# pane border look and feel

setw -g pane-border-status top
setw -g pane-border-format ""
setw -g pane-active-border-style "bg=#{@thm_bg},fg=#{@thm_overlay_0}"
setw -g pane-border-style "bg=#{@thm_bg},fg=#{@thm_surface_0}"
setw -g pane-border-lines single

# window look and feel

set -wg automatic-rename on
set -g automatic-rename-format "Window"

set -g window-status-format " #I#{?#{!=:#{window_name},Window},: #W,} "
set -g window-status-style "bg=#{@thm_bg},fg=#{@thm_rosewater}"
set -g window-status-last-style "bg=#{@thm_bg},fg=#{@thm_peach}"
set -g window-status-activity-style "bg=#{@thm_red},fg=#{@thm_bg}"
set -g window-status-bell-style "bg=#{@thm_red},fg=#{@thm_bg},bold"
set -gF window-status-separator "#[bg=#{@thm_bg},fg=#{@thm_overlay_0}]│"

set -g window-status-current-format " #I#{?#{!=:#{window_name},Window},: #W,} "
set -g window-status-current-style "bg=#{@thm_peach},fg=#{@thm_bg},bold"
```
