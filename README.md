# xkeyboard-config-f13
Modify xkb configuration files to add a layout option mapping the Caps Lock key to F13. The Caps Lock key can then be used, for example, as the prefix  for tmux.

## Overview
Adds a layout option in the xkb configuration which maps Caps Lock to F13. Shift + Caps Lock is used to obtain Caps Lock. This option can be used with any keyboard layout by adding the option "caps:f13" to the list of xkb layout options.

## Installation
On Arch Linux the package can be installed using the provided PKGBUILD by running: `makepkg -s` in the source directory. This will create a package archive xkb-caps-f13-{ver}.pkg.tar.xz. The package can then be installed by running either `makepkg -i` or `pacman -U xkb-caps-f13-{ver}.pkg.tar.xz`. (See [PKGBUILD](https://wiki.archlinux.org/index.php/PKGBUILD).)

## Usage
The option can be activated using the xkb command line syntax: `setxkbmap -option caps:f13` or using X configuration files (see [keyboard configuration in Xorg](https://wiki.archlinux.org/index.php/Keyboard_configuration_in_Xorg#Setting_keyboard_layout)).

For users of the Deepin desktop environment the option can be activated by adding the option 'caps:f13' to the key _com.deepin.dde.keyboard layout-options_.
For the GNOME desktop environment, the relevant key is _org.gnome.libgnomekbd.keyboard options_.
