# Waybar

> code ~/.config/waybar/config.jsonc

```
{
    "layer": "top",
    "position": "top",
    "mode": "dock",
    "exclusive": true,
    "passthrough": false,
    "gtk-layer-shell": true,
    "height": 0,
    "modules-left": [
        "clock",
        "hyprland/workspaces",
        "cpu",
        "memory",
        "network"
    ],
    "modules-center": ["hyprland/window"],
    "modules-right": [
        "tray",
        "hyprland/language",
        "battery",
        "backlight",
        "pulseaudio#microphone",
        "pulseaudio"
    ],

    "hyprland/window": {
        "format": "󰣇 {}"
    },
    
    "hyprland/workspaces": {
        "disable-scroll": true,
        "all-outputs": false,
        "on-click": "activate"
        //"format": "{icon}",
    },

    "tray": {
        "icon-size": 13,
        "spacing": 10
    },

    "clock": {
        "format": "{:%I:%M:%S %p}",
        "interval": 1,
        "rotate": 0,
        "tooltip-format": "<tt>{calendar}</tt>",
        "calendar": {
            "mode": "month",
            "mode-mon-col": 3,
            "on-scroll": 1,
            "on-click-right": "mode",
            "format": {
                "months": "<span color='#a6adc8'><b>{}</b></span>",
                "weekdays": "<span color='#a6adc8'><b>{}</b></span>",
                "today": "<span color='#a6adc8'><b>{}</b></span>",
                "days": "<span color='#555869'><b>{}</b></span>"
            }
        }
    },

    "backlight": {
        "device": "intel_backlight",
        "format": "{icon} {percent}%",
        "format-icons": ["󰃞", "󰃟", "󰃠"],
        "on-scroll-up": "brightnessctl set 5%+",
        "on-scroll-down": "brightnessctl set 5%-",
        "min-length": 6
    },

    "battery": {
        "states": {
            "good": 95,
            "warning": 30,
            "critical": 20
        },
        "format": "{icon} {capacity}%",
        "format-charging": " {capacity}%",
        "format-plugged": " {capacity}%",
        "format-alt": "{time} {icon}",
        "format-icons": ["󰂃", "󰁺", "󰁻", "󰁼", "󰁽", "󰁾", "󰁿", "󰂀", "󰂁", "󰂂", "󰁹"]
    },

    "pulseaudio": {
        "format": "{icon}  {volume}%",
        "tooltip": false,
        "format-muted": "  Muted",
        "on-click-right": "pamixer -t",
        "on-click": "pavucontrol",
        "on-scroll-up": "pamixer -d 5",
        "on-scroll-down": "pamixer -i 5",
        "scroll-step": 5,
        "format-icons": {
            "headphone": "",
            "hands-free": "",
            "headset": "",
            "phone": "",
            "portable": "",
            "car": "",
            "default": ["","", "", ""]
        }
    },

    "pulseaudio#microphone": {
        "format": "{format_source}",
        "format-source": " {volume}%",
        "format-source-muted": "  Muted",
        "on-click": "pamixer --default-source -t",
        "on-scroll-up": "pamixer --default-source -i 5",
        "on-scroll-down": "pamixer --default-source -d 5",
        "scroll-step": 5
    },

    "memory": {
        "states": {
            "c": 90, // critical
            "h": 60, // high
            "m": 30 // medium
        },
        "interval": 10,
        "format": "󰾆 {used}GB",
        "format-m": "󰾅 {used}GB",
        "format-h": "󰓅 {used}GB",
        "format-c": " {used}GB",
        "format-alt": "󰾆 {percentage}%",
        "max-length": 10,
        "tooltip": true,
        "tooltip-format": "󰾆 {percentage}%\n {used:0.1f}GB/{total:0.1f}GB"
    },

    "cpu": {
        "interval": 10,
        "format": "󰍛 {usage}%",
        "format-alt": "{icon0}{icon1}{icon2}{icon3}",
        "format-icons": ["▁", "▂", "▃", "▄", "▅", "▆", "▇", "█"]
    },

    "network": {
        "tooltip": true,
        "format-wifi": "  {essid}",
        "format-ethernet": "󰈀 ",
        "tooltip-format": "Network: <big><b>{essid}</b></big>\nSignal strength: <b>{signaldBm}dBm ({signalStrength}%)</b>\nFrequency: <b>{frequency}MHz</b>\nInterface: <b>{ifname}</b>\nIP: <b>{ipaddr}/{cidr}</b>\nGateway: <b>{gwaddr}</b>\nNetmask: <b>{netmask}</b>",
        "format-linked": "󰈀 {ifname} (No IP)",
        "format-disconnected": "󰖪 ",
        "tooltip-format-disconnected": "Disconnected",
        "format-alt": "<span foreground='#99ffdd'> {bandwidthDownBytes}</span> <span foreground='#ffcc66'> {bandwidthUpBytes}</span>",
        "interval": 2
    },

    "hyprland/language": {
		"format": "<span color='#cdd6f4'>󰌏 {}</span>",
		"format-en": "EN",
		"format-ru": "RU"
	}

}
```

> code ~/.config/waybar/style.css

```
* {
    border: none;
    border-radius: 0;
    font-family: JetBrainsMono Nerd Font, monospace;
    font-weight: bold;
    font-size: 14px;
    min-height: 0;
}

window#waybar {
    background: rgba(21, 18, 27, 0);
    color: #cdd6f4;
}

#workspaces button {
    padding: 5px;
    color: #555869;
    margin-right: 0px;
}
#workspaces button.active {
    color: #a6adc8;
}
#workspaces button.focused {
    color: #a6adc8;
    background: #eba0ac;
    border-radius: 10px;
}
#workspaces button.urgent {
    color: #11111b;
    background: #a6e3a1;
    border-radius: 10px;
}
#workspaces button:hover {
    background: #cdd6f4;
    color: #11111b; 
    border-radius: 10px;
}
#workspaces {
    background: #1e1e2e;
    padding: 0px 20px;
    margin: 3px 0px;
    margin-top: 5px;
    margin-right: 10px;
}

#window,
#clock,
#battery,
#pulseaudio,
#network,
#cpu,
#memory,
#tray,
#backlight,
#language  {
    background: #1e1e2e;
    padding: 0px 10px;
    margin: 3px 0px;
    margin-top: 5px;
    /* border: 1px solid #181825; */
}

#tray {
    border-radius: 10px;
    margin-right: 10px;
}

#workspaces {
    background: #1e1e2e;
    border-radius: 10px;
    margin-left: 10px;
    padding-right: 5px;
    padding-left: 5px;
}

#cpu {
    border-radius: 10px 0px 0px 10px;
}

#memory {
    border-radius: 0px;
}

#window {
    border-radius: 10px;
    margin-left: 60px;
    margin-right: 60px;
}

#clock {
    color: #a6adc8;
    border-radius: 10px 10px 10px 10px;
    margin-left: 5px;
    border-right: 0px;
}

#network {
    color:  #a6adc8;
    border-radius: 0px 10px 10px 0px;

}

#pulseaudio {
    color: #a6adc8;
    border-left: 0px;
    border-right: 0px;
    margin-right: 5px;
    border-radius: 0px 10px 10px 0px;
}

#pulseaudio.microphone {
    color: #a6adc8;
    border-left: 0px;
    border-right: 0px;
    border-radius: 0px;
    margin-right: 0px;
}

#battery {
    color:#a6adc8;
}

#language {
    color: #a6adc8;
    border-left: 0px;
    border-right: 0px;
    border-radius: 10px 0px 0px 10px;
}
```

# Hyprconfig

> code ~/.config/hypr/hyprland.conf

cp from file

# to set en layout on lock

make script `/home/username/.local/share/bin/switch-to-us.sh`

```
#!/bin/bash
# switch-to-us.sh

# change layout
setxkbmap us
```

> chmod +x switch-to-us.sh

edit hypridle

```
on-timeout = /home/username/.local/share/bin/switch-to-us.sh && loginctl lock-session
```