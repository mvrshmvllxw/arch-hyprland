# Install dependencies

> sudo pacman -S pipewire wireplumber gdb ninja gcc cmake libxcb xcb-proto xcb-util xcb-util-keysyms libxfixes libx11 libxcomposite xorg-xinput libxrender pixman wayland-protocols cairo pango seatd libxkbcommon xcb-util-wm xorg-xwayland cmake wlroots mesa git meson polkit fmt spdlog gtkmm3 libdbusmenu-gtk3 upower libmpdclient sndio gtk-layer-shell scdoc clang awesome-terminal-fonts jq xdg-desktop-portal-hyprland polkit-kde-agent qt5-wayland qt6-wayland qt5ct qt6ct kvantum kvantum-qt5 kconfig kde-cli-tools qt5-tools papirus-icon-theme hypridle hyprlock

> paru -S network-manager-applet pipewire-alsa pipewire-pulse gst-plugin-pipewire pavucontrol pamixer bluez bluez-utils blueman brightnessctl udiskie xdg-desktop-portal-gtk nautilus dolphin gnome-text-editor waybar dunst swww nwg-shell tela-circle-icon-theme-all bibata-cursor-theme tofi wlogout pipewire-audio pipewire-jack gst-plugin-pipewire

> paru -S --needed  polkit-gnome xdg-desktop-portal-hyprland pacman-contrib python-pyamdgpuinfo parallel jq imagemagick qt5-imageformats ffmpegthumbs kde-cli-tools kservice5 libnotify


# icons

apply icons (tela-circle-icon-theme-all) for kde apps

> kwriteconfig6 --file ~/.config/kdeglobals --group Icons --key Theme 'Tela-circle-pink'

apply for gnome apps

> gsettings set org.gnome.desktop.interface icon-theme 'Tela-circle-pink'

! instead of 'Tela-circle-pink' you can specify any other color from this package

# install gnome apps theme

you can use gui `nwg-look` to check or change gtk theme

download repo

> cd ~/Downloads

> git clone https://github.com/mvrshmvllxw/arch-hyprland.git

copy folders:

> cp -r ~/Downloads/arch-hyprland-manual-install/.config/gtk-3.0 ~/.config/gtk-3.0

> cp -r ~/Downloads/arch-hyprland-manual-install/.config/gtk-4.0 ~/.config/gtk-4.0

> cp -r ~/Downloads/arch-hyprland-manual-install/.config/nwg-look ~/.config/nwg-look

> cp -r ~/Downloads/arch-hyprland-manual-install/.themes ~/.themes

and apply theme from terminal (or use `nwg-look`)

> gsettings set org.gnome.desktop.interface gtk-theme 'Rose-Pine'

if you need to turn on gnome dark scheme 

> gsettings set org.gnome.desktop.interface color-scheme 'prefer-dark'

# install kde apps theme

copy kvantum theme and qt6ct settings

> cp -r ~/Downloads/arch-hyprland-manual-install/.config/Kvantum ~/.config/Kvantum

> cp -r ~/Downloads/arch-hyprland-manual-install/.config/qt6ct ~/.config/qt6ct

set kde theme to Kvantum

> kwriteconfig6 --file kdeglobals --group KDE --key widgetStyle kvantum-dark

> kwriteconfig6 --file kdeglobals --group General --key ColorScheme Kvantum

now you can use `kvantummanager` and `qt6ct` for gui theming (use qt6ct if icons didn't set)

# cursor

apply for kde (bibata-cursor-theme)

> kwriteconfig6 --file ~/.config/kcminputrc --group Mouse --key cursorTheme Bibata-Original-Ice

apply for gnome

> gsettings set org.gnome.desktop.interface cursor-theme 'Bibata-Original-Ice'

apply for hyprland

> hyprctl setcursor Bibata-Original-Ice 24

apply to..? (just need)

> sudo nano /usr/share/icons/default/index.theme 

    [Icon Theme]
    Inherits=Bibata-Original-Ice

apply to sddm 

> sudo nano /etc/sddm.conf

add

    [Theme]
    CursorSize=24
    CursorTheme=Bibata-Original-Ice

if any bugs try:

    copy folder from /usr/share/icons/Bibata-Original-Ice

    to ~/.local/share/icons and  ~/.icons

or install

    plasma-desktop gnome

# wallpapers

use swww, hyperconfig already have autostart (xec-once = swww-daemon)

set image:

> swww img path/to/img

repeat 'sww img' if two monitors 

# enable bluetooth

> sudo systemctl enable bluetooth.service 

> sudo systemctl restart bluetooth.service

# set up tofi (launch menu)

> code ~/.config/tofi/configA

paste

```
width = 100%
height = 100%
border-width = 0
outline-width = 0
padding-left = 33%
padding-top = 33%
result-spacing = 25
num-results = 5

font = JetBrainsMono Nerd Font
font-size = 24

text-color = #4e4e5f

prompt-text = " : "

background-color = #11111bd9
selection-color = #83A4E7
```

> code ~/.config/tofi/configV

paste

```
width = 100%
height = 100%
border-width = 0
outline-width = 0
padding-top = 33%
padding-left = 10%
padding-right = 10%
result-spacing = 25
num-results = 5

font = JetBrainsMono Nerd Font
font-size = 24

text-color = #4e4e5f

prompt-text = " : "

background-color = #11111bd9
selection-color =  #83A4E7
```

# dunst (notifications)

> code ~/.config/dunst/dunstrc

paste

```
[global]
    follow = mouse
    indicate_hidden = yes

    offset = 10x10

    notification_height = 0

    separator_height = 2

    padding = 8
    horizontal_padding = 8
    text_icon_padding = 0
    frame_width = 2

    frame_color = "#a6adc8"
    separator_color = frame

    sort = yes
    idle_threshold = 120
    font = monospace 10
    line_height = 0
    markup = full
    alignment = left
    vertical_alignment = center
    show_age_threshold = 60
    word_wrap = yes
    stack_duplicates = true
    hide_duplicate_count = false

    show_indicators = yes

    min_icon_size = 0
    max_icon_size = 64

    icon_path = /usr/share/icons/Papirus-Dark/16x16/status/:/usr/share/icons/Papirus-Dark/16x16/devices/:/usr/share/icons/Papirus-Dark/16x16/actions/:/usr/share/icons/Papirus-Dark/16x16/animations/:/usr/share/icons/Papirus-Dark/16x16/apps/:/usr/share/icons/Papirus-Dark/16x16/categories/:/usr/share/icons/Papirus-Dark/16x16/emblems/:/usr/share/icons/Papirus-Dark/16x16/emotes/:/usr/share/icons/Papirus-Dark/16x16/devices/mimetypes:/usr/share/icons/Papirus-Dark/16x16/panel/:/usr/share/icons/Papirus-Dark/16x16/places/

    dmenu = /usr/bin/wofi -p dunst:
    browser = /usr/bin/firefox --new-tab

    title = Dunst
    class = Dunst

    corner_radius = 10
    timeout = 5

[urgency_low]
    background = "#1e1e2e"
    foreground = "#CDD6F4"

[urgency_normal]
    background = "#1e1e2e"
    foreground = "#CDD6F4"

[urgency_critical]
    background = "#1e1e2e"
    foreground = "#CDD6F4"
    frame_color = "#FAB387"
```

# wlogout (log out menu)

> code ~/.config/wlogout/layout

```
{
    "label" : "exit",
    "action" : "",
    "text" : "Exit",
    "keybind" : "h"
}
{
    "label" : "shutdown",
    "action" : "systemctl poweroff",
    "text" : "Shutdown",
    "keybind" : "s"
}

{
    "label" : "suspend",
    "action" : "systemctl suspend-then-hibernate",
    "text" : "Suspend",
    "keybind" : "u"
}
{
    "label" : "lock",
    "action" : "hyprlock",
    "text" : "Lock",
    "keybind" : "l"
}
{
    "label" : "logout",
    "action" : "hyprctl dispatch exit",
    "text" : "Logout",
    "keybind" : "e"
}
{
    "label" : "reboot",
    "action" : "systemctl reboot",
    "text" : "Reboot",
    "keybind" : "r"
}
```

also

> code ~/.config/wlogout/style.css

```
* {
    font-family: JetBrains Mono, Symbols Nerd Font;
    font-size: 24px;
    transition-property: background-color;
    transition-duration: 0.7s;
}

window {
    background-color: #11111b;
    /* border-radius: 10px; */
}

button {
    background-color: #11111b;
    border-style: solid;
    /* border-width: 2px; */
    border-radius: 50px;
    background-repeat: no-repeat;
    background-position: center;
    background-size: 15%;
    margin: 15px;
}

button:active,
button:hover {
    background-color: #cdd6f4;
}

button:focus {
    border-color: #cdd6f4;
}

#lock {
    background-image: image(url("./assets/lock.png"), url("./assets/lock.png"));
}

#lock:hover {
    background-image: image(url("./assets/lock-hover.png"), url("./assets/lock-hover.png"));
    color: #11111b;
}

#logout {
    background-image: image(url("./assets/logout.png"), url("./assets/logout.png"));
}

#logout:hover {
    background-image: image(url("./assets/logout-hover.png"), url("./assets/logout-hover.png"));
    color: #11111b;
}

#suspend {
    background-image: image(url("./assets/sleep.png"), url("./assets/sleep.png"));
}

#suspend:hover {
    background-image: image(url("./assets/sleep-hover.png"), url("/assets/sleep-hover.png"));
    color: #11111b;
}

#shutdown {
    background-image: image(url("./assets/power.png"), url("./assets/power.png"));
}

#shutdown:hover {
    background-image: image(url("./assets/power-hover.png"), url("./assets/power-hover.png")); 
    color: #11111b;
}

#reboot {
    background-image: image(url("./assets/restart.png"), url("./assets/restart.png"));
}

#reboot:hover {
    background-image: image(url("./assets/restart-hover.png"), url("./assets/restart-hover.png"));
    color: #11111b;
}

#exit {
    background-image: image(url("./assets/restart.png"), url("./assets/restart.png"));
    background-color: #11111b;

}

#exit:hover {
    background-image: image(url("./assets/restart-hover.png"), url("./assets/restart-hover.png"));
    color: #11111b;
    background-color: #cdd6f4;
}
```

and copy images

> cp -r ~/Downloads/arch-hyprland-manual-install/.config/wlogout/assets ~/.config/wlogout/assets


# hyprlock

> code ~/.config/hypr/hyprlock.conf

(cganhe image path)

```
background {
    monitor =
    path = ~/Pictures/System/anime-girl-tattoo-4k-wallpaper.png # only png supported for now
}

input-field {
    monitor =
    size = 200, 50
    outline_thickness = 3
    dots_size = 0.33 # Scale of input-field height, 0.2 - 0.8
    dots_spacing = 0.15 # Scale of dots' absolute size, 0.0 - 1.0
    dots_center = true
    dots_rounding = -1 # -1 default circle, -2 follow input-field rounding
    outer_color = rgb(a6adc8)
    inner_color = rgb(11111b)
    font_color = rgb(a6adc8)
    fade_on_empty = true
    fade_timeout = 1000 # Milliseconds before fade_on_empty is triggered.
    placeholder_text = <i>Input Password...</i> # Text rendered in the input box when it's empty.
    hide_input = false
    rounding = -1 # -1 means complete rounding (circle/oval)
    check_color = rgb(204, 136, 34)
    fail_color = rgb(204, 34, 34) # if authentication failed, changes outer_color and fail message color
    fail_text = <i>$FAIL <b>($ATTEMPTS)</b></i> # can be set to empty
    fail_transition = 100 # transition time in ms between normal outer_color and fail_color
    capslock_color = -1
    numlock_color = -1
    bothlock_color = -1 # when both locks are active. -1 means don't change outer color (same for above)
    invert_numlock = false # change color if numlock is off
    swap_font_color = false # see below
    position = 0, -20
    halign = center
    valign = center
}

label {
    monitor =
    text = cmd[update:1000] echo "$TIME"
    color = rgba(a6adc8)
    font_size = 55
    font_family = Fira Semibold
    position = -100, 40
    halign = right
    valign = bottom
    shadow_passes = 5
    shadow_size = 10
}

label {
    monitor =
    text = 
    color = rgba(a6adc8)
    font_size = 20
    font_family = Fira Semibold
    position = -100, 160
    halign = right
    valign = bottom
    shadow_passes = 5
    shadow_size = 10
}

# image {
#     monitor =
#     path = ~/Pictures/System/anime-girl-tattoo-4k-wallpaper.png
#     size = 280 # lesser side if not 1:1 ratio
#     rounding = -1 # negative values mean circle
#     border_size = 4
#     border_color = rgb(a6adc8)
#     rotate = 0 # degrees, counter-clockwise
#     reload_time = -1 # seconds between reloading, 0 to reload with SIGUSR2
# #    reload_cmd =  # command to get new path. if empty, old path will be used. don't run "follow" commands like tail -F
#     position = 0, 200
#     halign = center
#     valign = center
# }
```

# hypridle 

> code ~/.config/hypr/hyprlock.conf

(edit settings)

```
general {
    lock_cmd = pidof hyprlock || hyprlock       # avoid starting multiple hyprlock instances.
    before_sleep_cmd = loginctl lock-session    # lock before suspend.
    after_sleep_cmd = hyprctl dispatch dpms on  # to avoid having to press a key twice to turn on the display.
}

listener {
    timeout = 60                                 # 1min.
    on-timeout = brightnessctl -s set 5          # set monitor backlight to minimum, avoid 0 on OLED monitor.
    on-resume = brightnessctl -r                 # monitor backlight restore.
}

listener {
    timeout = 120                                 # 2min
    on-timeout = loginctl lock-session            # lock screen when timeout has passed
}

listener {
    timeout = 300                                 # 5min
    on-timeout = hyprctl dispatch dpms off        # screen off when timeout has passed
    on-resume = hyprctl dispatch dpms on          # screen on when activity is detected after timeout has fired.
}

listener {
    timeout = 900                                 # 30min
    on-timeout = systemctl suspend                # suspend pc
}
```

# sddm theme

> sudo git clone https://github.com/keyitdev/sddm-astronaut-theme.git /usr/share/sddm/themes/sddm-astronaut-theme

> sudo cp /usr/share/sddm/themes/sddm-astronaut-theme/Fonts/* /usr/share/fonts/

> sudo nano /etc/sddm.conf

    [Theme]
    Current=sddm-astronaut-theme

to change login background add image to

    /usr/share/sddm/themes/sddm-astronaut-theme/

example

> sudo cp ~/Pictures/System/anime-girl-tattoo-4k-wallpaper.png /usr/share/sddm/themes/sddm-astronaut-theme/

and edit

    /usr/share/sddm/themes/sddm-astronaut-theme/theme.conf








# hyprconf 

download and set the hyprland config

> curl -o ~/.config/hypr/hyprland.conf https://raw.githubusercontent.com/mvrshmvllxw/arch-hyprland-manual-install/main/.config/hypr/hyprland.conf

use nano to edit it 

> nano ~/.config/hypr/hyprland.conf

first of all, edit the settings for the monitor, window control keys and application launch key

default: 

    win+q - close, win+w - fullscreen,
    win+z - terminal (kitty), win+s - nautilus, win+f - firefox,
    win+1,+2,+3 - change desktop,
    win+right_mouse - change window size
    capslock - switch keyboard layout (en/ru)


