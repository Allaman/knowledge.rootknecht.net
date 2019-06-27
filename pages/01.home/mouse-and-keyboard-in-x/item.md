---
title: 'Mouse and Keyboard in X'
---

! Does not apply to Wayland and assumes `f86-input-libinput`

## Configuring mouse and trackpoint

List devices with `xinput --list`

List props of a device with `xinput --list-props <DEVICE_ID>`

Set acceleration with `xinput --set-prop <DEVICE ID> 'libinput Accel Speed' <ACC FACTOR>`
    
In `/etc/X11/xorg.conf.d/99-libinput-custom-config.conf` persist configuration:
    
```
Section "InputClass"
  Identifier "Trackpoint AccelSpeed"
  MatchDriver "libinput"
  MatchProduct "TPPS/2 Elan TrackPoint" # adjust to your needs
  Option "AccelSpeed" "0.5"
EndSection
```

## Configuring keyboard

Keyboard layout in `/etc/X11/xorg.conf.d/00-keyboard.conf`

```
Section "InputClass"
        Identifier "system-keyboard"
        MatchIsKeyboard "on"
        Option "XkbLayout" "de"
        Option "XkbModel" "pc105"
        Option "XkbVariant" "nodeadkeys"
EndSection
```
    
Remap some buttons (needs [xcape](https://github.com/alols/xcape))
```sh
echo "Set Caps to CTRL modifier"
setxkbmap -option caps:ctrl_modifier
echo "Set menu key to compose key"
setxkbmap -option compose:menu
echo "Set Ctrl Alt Bksp to terminate X session"
setxkbmap -option terminate:ctrl_alt_bksp
echo "Set Caps_Lock to ESC with xcape"
xcape -e "Caps_Lock=Escape"
```