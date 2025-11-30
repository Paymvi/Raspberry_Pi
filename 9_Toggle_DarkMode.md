

## Batch scripting is your friend  


Make a file called `ToggleDark.sh`  
Paste in this code:
```
#!/bin/bash
# toggle-dark-mode.sh
# Toggle GTK theme + color-scheme (tabs/headerbars included)

# Detect current GTK theme
CURRENT_THEME=$(gsettings get org.gnome.desktop.interface gtk-theme | tr -d "'")

if [[ "$CURRENT_THEME" == "Adwaita-dark" ]]; then
    # Switch to light mode
    gsettings set org.gnome.desktop.interface gtk-theme "Adwaita"
    gsettings set org.gnome.desktop.interface color-scheme "prefer-light"
else
    # Switch to dark mode
    gsettings set org.gnome.desktop.interface gtk-theme "Adwaita-dark"
    gsettings set org.gnome.desktop.interface color-scheme "prefer-dark"
fi

# XFCE / Thunar support (if using XFCE)
xfconf-query -c xsettings -p /Net/ThemeName -s $(gsettings get org.gnome.desktop.interface gtk-theme | tr -d "'") 2>/dev/null

# Restart file manager so GTK theme applies immediately
killall Thunar 2>/dev/null
thunar &

# Optional: restart panel for XFCE (or logout/relogin if needed)
xfce4-panel -r 2>/dev/null
```

Make it executable
```
chmod +x ~/YOUR-PATH-HERE/ToggleDark.sh
```

## Make the Icon for your desktop
Create a .desktop file in your desktop browser
```
nano ~/Desktop/ToggleDark.desktop
```
Paste this in:
```
[Desktop Entry]
Name=ToggleDark
Comment=Switch Raspberry Pi between light and dark GTK theme
Exec=/home/YOUR-USERNAME-HERE/ToggleDark.sh
Icon=/home/YOUR-USERNAME-HERE/icons/FIND-YOUR-IMAGE.png
Terminal=true
Type=Application
Categories=Utility;
```

Use `whoami` if you don't know what your username is.  
Also, I recommend using favicon to find a good icon iamge for your shortcut.


Make it executable:
```
chmod +x ~/Desktop/ToggleDark.desktop
```