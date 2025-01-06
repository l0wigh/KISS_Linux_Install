# The struggle to install xorg-server on KISS

- Add the xorg repo
- Remove (not for ever) repo/extra since it collide with the mesa package from xorg repo
- `kiss b xorg-server`
    - if it fails : `kiss b libepoxy`
- `kiss b xinit setxkbmap`

You should be fine now. Just compile your prefered X11 WM !
