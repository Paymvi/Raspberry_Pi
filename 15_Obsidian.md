Obsidian is a local-first, markdown-based knowledge system.
Think of it as a personal “second brain” where every note is just a .md file stored on your computer.

It’s basically:
- A folder full of markdown files
- an insanely powerful editor
- graph view
- plugins that let you turn it into whatever you want (wiki, todo manager, Zettelkasten, code vault, academic research hub, planner, etc.)

It's lightweight, fast,  and extremely customizable.


Install with Pi-Apps (GUI installer for ARM)

Since you’re on a Pi, there’s also a “Pi-Apps” GUI that installs Obsidian for ARM64 for you (handles paths/menu entries/etc). 
Pi-Apps

Install Pi-Apps:
```
wget -qO- https://raw.githubusercontent.com/Botspot/pi-apps/master/install | bash
```

Then:

1. Open Pi-Apps from your menu
2. Go to Office → Obsidian → Install


---


# How to have remote access to your Obsidian Files?
(If you want to have your laptop edit for example even if the files are on the pi)

Here are your options:
Option 1: Tailscale Sync
    - Free
    - Completely encryptied (WireGuard under the hood)
    - Zero firewall or port fort-foward headaches
    - Works over mobile data
    - Works anywhere in the world
    - No vendor lock in
Option 2: Obsidian Git Plugin
    - Good for version history (but nto real time sync)
Option 3: Official Obsidian Sync (paid)
    - I donn't recommend becuase it costs money and is not self hosted (which ruins the point)

## I will be going over the Tailscale sync

Prerequisitie: Put tailscale on all your devices
(Directions on how to do this is in part 4 of Jellyfin)

### FIRST: Install Syncing on the Pi
```
sudo apt install syncthing
syncthing &
```
(The last one will open up 127.0.0.1:8384)

Syncthing's web UI **by default only listens to localhost** for safety.
Your tailscale IP will not work becuase of this... it is not configured to allow remote access.

To fix this you need to allow Synthing to listen on Tailscale
1. Go to:  
Actions -> Settings -> Gui  
2. Then change the "GUI Listen Addresses" field to this:  
```
0.0.0.0:8384  
```
This means "Accept connections on any network interface this machine (the pi) has. This includes:
- your Pi's local network IP
- your Pi's localhost
- your Pi's Tailscale IP
It is still protected... by tailscale, by the username and password, and by encryption
3. Then (IMPORTANT) Set a GUI Username + Password

### NEXT: Install Syncthing on your other devices
(I will be going over windows)
1. Go here:
```
https://syncthing.net/downloads/
```
2. Download for Windows (64 bit, Intel/AMD)... you will be given a zip file
3. Extract and then click on syncthing.exe
4. Then get Device ID from Windows
```
http://localhost:8384
```
Then:  
Actions --> Show ID  
Copy the long ID text (looks like `ABCD!@#$-WXYZ...)  
Leave this window open  
5. Add deviced to your Pi syncthing
On your `Pi`, open Syncthing:
```
127.0.0.1:8384
```
Now:  
- Click "Add Remote Device"
- Paste the Device ID
- Leave everything default, then **save**
6. Now check your new device (windows) again.  
It will be like:
```
"Device 'Pi' wants to connect. Add device?"
```
Click, `Add Device`.

Now on your Pi will now see your Windows laptip in the sharing tab (when you make a shared folder).  
Now, when you make a shared folder, select the device you want to share obsidian with.
Also, make a folder you want the files to go and then paste the folder location/path into the box.

Then save... then you are done!!!