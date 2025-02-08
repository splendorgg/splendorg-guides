---
title: Wezterm Config
---


Use an editor to change your config file. It should be located in your Home directory. 

To include an image in your Wezterm configuration, simply provide the path to the image for ````config.window_background_image````

Change this with your config file and edit to your preferences.
```lua
local wezterm = require 'wezterm'

local config = wezterm.config_builder()

config.keys = {
  {
    key = 'w',
    mods = 'CMD',
    action = wezterm.action.CloseCurrentTab { confirm = false },
  },
}

config.color_scheme = 'Adventure'

config.animation_fps = 144

config.max_fps = 144

config.default_cursor_style = 'BlinkingBlock'

config.enable_wayland = true

config.initial_cols = 130

config.initial_rows = 28

config.window_decorations = "RESIZE"

config.window_background_opacity = 0.9


config.colors = {
  foreground = "#07fa54",  -- Text Color (green)
}


config.window_background_image = "<change here>"

config.window_background_image_hsb = {
    brightness = 0.5,
    hue = 1.0,        
    saturation = 1.0, 
  }

config.font =
  wezterm.font('JetBrains Mono', { weight = 'Bold' }) -- MesloLGM Nerd Font
  

return config
```