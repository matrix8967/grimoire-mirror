# Kitty 😼️

Kitty is an incredibly versatile `GPU` enhanced *Terminal Emulator* with too many useful features to list here.

It's worth going to [Kitty's Docs](https://sw.kovidgoyal.net/kitty/conf.html) and reading through the features of the `config` file yourself - but these are some adjustments I've made over the years of tweaking my config as both `Kitty` and I grow.

It's developed and maintained by [Kovid Goyal](https://github.com/kovidgoyal) who maintains _another_ extremely popular opensource App: `Calibre.` 🤯️

[Kitty Source](https://github.com/kovidgoyal/kitty)

### kitty.conf

```
# 	===== Themes ===== 	#

include themes/Dracula.conf

background_opacity .85

# 	===== Fonts ===== 	#

font_size 16.0

# mononoki Nerd Font Mono
#    mononoki Bold Italic Nerd Font Complete Mono
bold_font    mononoki Bold Nerd Font Complete Mono
italic_font    mononoki Italic Nerd Font Complete Mono
font_family    mononoki-Regular Nerd Font Complete Mono

#       ===== Cursor =====  	#

cursor_shape underline
visual_bell_duration 0.0
enable_audio_bell no
cursor_shape underline
cursor_blink_interval 0
cursor_stop_blinking_after 15.0
wheel_scroll_multiplier 5.0

#       ===== Text =====	#

strip_trailing_spaces smart
focus_follows_mouse yes
rectangle_select_modifiers ctrl+shift
select_by_word_characters :@-./_~?&=%+#
scrollback_pager more

# 	===== URLs =====	#

url_style double
open_url_modifiers ctrl+shift
open_url_with firefox

#       ===== GPU =====		#

sync_to_monitor yes
window_alert_on_bell no

#       ===== Size =====	#

remember_window_size  yes

#       ===== TabBar =====	#

#tab_separator " ┇"
#tab_bar_style fade
tab_bar_min_tabs 2
tab_bar_edge bottom
tab_bar_style powerline
tab_powerline_style angled

active_tab_foreground 	#1e1f28
active_tab_background   #50fa7b
active_tab_font_style   bold-italic
inactive_tab_foreground #1e1f28
inactive_tab_background #44475a
inactive_tab_font_style normal

#       ===== Keys =====	#

map ctrl+tab next_window
map ctrl+shift+tab prev_window

map ctrl+shift+left resize_window narrower
map ctrl+shift+right resize_window wider
map ctrl+shift+up resize_window taller
map ctrl+shift+down resize_window shorter

map ctrl+left previous_tab
map ctrl+right next_tab

#	===== Exec =====	#

close_on_child_death yes
```
