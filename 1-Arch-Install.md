# download iso

download distro and boot from usb
https://archlinux.org/download/

from windows use rufus or balenaetcher to make bootable usb

# connect to wifi

Internet required for installation, set up Wi-Fi or skip this step if you use Ethernet

```bash
iwctl
device list
# if wi-fi powered off, replace NAME and ADAPTER
device NAME set-property Powered on
adapter ADAPTER set-property Powered on
# scan and connect, replace NAME and SSID
station NAME scan
station NAME get-networks
station NAME connect SSID
exit
```

# pacman

prepare pacman and mirrors to fix possible errors

> gpg --refresh-keys

> pacman-key --init

> pacman-key --populate archlinux

> pacman -Sy archlinux-keyring

> pacman -Su (optional)

# mirrors

> pacman -S reflector rsync

> reflector --verbose --latest 15 --sort rate --save /etc/pacman.d/mirrorlist

# installer

install python

> pacman -S python

run automatic installer

> archinstall

set the settings:

	profile > type > desktop > Hyprland (polkit)

the rest is as you like, but I recommend:

	bootloader: systemd-boot or limine
	unified kernel images: false
	audio driver: pipeware
	kernel: linux-zen
	network: networkmanager
	repositories: multilib

install and

> reboot

or 

> exit

> reboot