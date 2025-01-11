# The struggle (not really) to install xorg-server on KISS

- Add the xorg repo on top of the default repos
- `kiss b xorg-server xinit setxkbmap libinput xf86-input-libinput`

You should be fine now. Just compile your prefered X11 WM ! (and install the required deps)
