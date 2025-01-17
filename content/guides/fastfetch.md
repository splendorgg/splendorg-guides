---
title: Fastfetch Config File
---

Use an editor to change your config file. It should be located in ````~/.config/fastfetch/config.jsonc ````. 
If you don't have this config fiel you can create it with ```` fastfetch --gen-config ````


To include an image in your Fastfetch configuration, simply provide the path to the image in the source field of the logo section.

Change this with your config file and edit to your preferences.
```
{
    "$schema": "https://github.com/fastfetch-cli/fastfetch/raw/dev/doc/json_schema.json",
    "logo": {
        "type": "kitty-direct",
        "source":"<change here>",
        "width":25,
        "height":15,
        "padding":{
            "left":1,
            "top":3,
        }
    },
    "display": {
        "separator": "->   ",
        "color": {
            "separator": "1"
        }
    },
    "modules": [
        {
            "type": "title",
            "format": "                                {6}{7}{8}"
        },
        "break",
        {
            "type": "custom",
            "format": "┌───────────────────────────── {#1}System Information{#} ─────────────────────────────┐"
        },
        "break",
        {
            "key": "    OS           ",
            "keyColor": "blue",
            "type": "os"
        },
        {
            "key": "    󰌢 Machine      ",
            "keyColor": "green",
            "type": "host"
        },
        {
            "key": "     Kernel       ",
            "keyColor": "magenta",
            "type": "kernel"
        },
        {
            "key": "    󰅐 Uptime       ",
            "keyColor": "red",
            "type": "uptime"
        },
        {
            "key": "     Packages     ",
            "keyColor": "cyan",
            "type": "packages",
        },
        {
            "key": "    󰍹 Resolution   ",
            "keyColor": "yellow",
            "type": "display",
            "compactType": "original-with-refresh-rate"
        },
        {
            "key": "     WM           ",
            "keyColor": "blue",
            "type": "wm"
        },
        {
            "key": "     DE           ",
            "keyColor": "green",
            "type": "de"
        },
        {
            "key": "     Shell        ",
            "keyColor": "cyan",
            "type": "shell"
        },
        {
            "key": "     Terminal     ",
            "keyColor": "red",
            "type": "terminal"
        },
        {
            "key": "    󰻠 CPU          ",
            "keyColor": "yellow",
            "type": "cpu"
        },
        {
            "key": "    󰍛 GPU          ",
            "keyColor": "blue",
            "type": "gpu"
        },
        {
            "key": "    󰑭 Memory       ",
            "keyColor": "magenta",
            "type": "memory"
        },
        "break",
        {
            "type": "custom",
            "format": "└──────────────────────────────────────────────────────────────────────────────┘"
        },
        "break",
        {
            "type": "colors",
            "paddingLeft": 34,
            "symbol": "circle"
        }
    ]
}
```

