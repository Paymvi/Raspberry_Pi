I just wanted to make an FYI page


So I wanted to check the model of my monitor so I ran:
```
xrandr --verbose
```

And I was looking for something like:
```
EDID:
    ModelName: "Acer XF240H"
```

What is `xrandr --verbose`?  
`xrandr --verbose` is a Linux command (specifically for systems running X11—like Raspberry Pi OS Desktop) that shows detailed information about your display, including:  
- What monitors are connected
- Their resolution(s)
- Refresh rates
- Connection ports (HDMI-1, HDMI-2, etc.)
- **EDID data** → which often includes the actual monitor model name

But the thing is...
xrander is an X11 tool, and I am not running X11  
I was running **Wayland** (which is a fake virtual monitor)  
This hides a lot of physical information.  

<br><br>



### Another FYI
You cannot copy and paste in the terminal so either do:  
Ctrl + Shift + C  
Ctrl + Shift + V  

or  

Right-click → Copy  
Right-click → Paste