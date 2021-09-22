---
Title: Artix Configuration Guide (WIP)
Author: S
---
# Artix Configuration 

## Users and groups

### Create new user

```sh
useradd -m -g wheel usr #add user 'usr' to group 'wheel'
passwd usr #gives user 'usr' a password
```

### Set Privileges

Open `visudo` and uncomment desired values.

#### Defaults

```sh
root ALL=(ALL) ALL
%wheel ALL=(ALL) ALL
```

#### Exclude password for certain commands

```sh
%wheel ALL=(ALL) NOPASSWD: /usr/bin/shutdown,/usr/bin/reboot,/usr/bin/mount,/usr/bin/umount,/usr/bin/pacman -Syu
```

### Password eligible for all terminals

```sh
Defaults !tty_tickets
```

### Other

Check out `man` for `useradd`, `userdel`, `groupadd`, `groupdel`, etc.

## Graphical Enviroment Requirements

### xorg

Install xorg by running the following command:

```sh
pacman -S xorg-server xorg-xinit
```

Start X by running:

```sh
exec startx
```

Configuration can be found at `~/.xinitrc`

A common error involves the intel video drivers. Resolve this by installing `xf86-video-intel`.

### Desktop Environemt

```sh
pacman -S xfce4
```

### Window Manager

#### Installation

In this example we will be using i3 as the window manager.
We can install this and its requirements by running:

```sh
pacman -S i3-gaps i3-status rxvt-unicode dmenu
```

Make the X server run i3 when it starts by adding `exec i3` in file `~/.xinitrc`

#### Things you might need

* Network Manager applet: `pacman -S nm-applet`
* Fonts: `pacman -S ttf-linux-libertine ttf-inconsolata` or `pacman -S noto-fonts` .
* You can set fonts manually in `~/.config/fontconfig/fonts.conf`

## Customizing user startup & user settings

Check out files like `~/.profile` or `~/.bash_profile`.

Example for `~/.profile`:

```sh
export EDITOR="vim"
export TERMINAL="st"
export BROWSER="firefox"

if [[ "$(tty)" = "/dev/tty1" ]]; then
        pgrep i3 || exec startx
fi
```