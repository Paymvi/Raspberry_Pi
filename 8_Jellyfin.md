

## Part 1 - Prepare Your Raspberry Pi (5)
You need
- Raspberry Pi 5
- SSD (recommended, not SD card)
- Ethernet (recommended)
- Raspberry Pi OS (Lite or Desktop, doesn’t matter)

Update system first:
```
sudo apt update
sudo apt upgrade -y
sudo reboot
```


## Part 2 - Install Jellyfin (Native ARM APT Repository)
Jellyfin ARM64 builds fully support hardware acceleration.
1. Add Jellyfin repo key
```
Jellyfin ARM64 builds fully support hardware acceleration.
```
2. Install Jellyfin
```
sudo apt install jellyfin -y
```
3. Start the server
```
sudo systemctl enable jellyfin
sudo systemctl start jellyfin
```
4. Check that it's running
```
http://<PI-IP>:8096
```
<img src="./img/pi-jellyfin-1.jpg" alt="pi screen" width="400"/>  

## Part 3 - Make a media library for YouTube Videos
If you haven't already:
```
sudo apt install yt-dlp
```
This is how you are going to get the videos from youtube into .mp4 or .webm

Now...
1. Library type
Choose "Home Videos & Photos"  
Why not “Movies” or “TV Shows”?  
- YouTube videos usually don’t match movie databases
- And they are not in S01E01 format
Home Videos = perfect category for random videos.

2. Display Name... put `YouTube`

3. Content Folder
Navigate to the folder you will put your videos in.  
Mine looks like:
```
/mnt/ssd/YouTube
```
(Because that is my mounted SSD... instructions on how to mount an SSD is also in this github repo)
Anyway, choose the folder and choose "Ok".  
This tells Jellyfin where to scan for files

<br>

<img src="./img/pi-jellyfin-2.jpg" alt="pi screen" width="400"/>  
<br>
4. Check & Uncheck  
This is the optimized setup for minimal CPU load, correct thumbnails, and not breaking it  

✔️ Enable the library  
❌ Display the photos  
❌ Prefer embedded titles over filenames  
✔️ Enable real-time monitoring  
❌ METADATA SAVERS [uncheck everything]  
✔️ Embedded Image Extractor  
✔️ Screen Grabber  
❌ Save artwork into media folders  
✔️ Enable trickplay image extraction  
❌ Extract trickplay images during the library scan  
❌ Save trickplay images next to media  
❌ Enable chapter image extraction  
❌ Extract chapter images during the library scan  

5. Putting the file into the main folder `/mnt/ssd/YouTube`
What is tricky about this whole process is the permissions.  
First check your username using:
```
whoami
```

Make sure you have ownership so you can write into the folder
```
sudo chown -R "YOUR-USERNAME":*YOUR-USERNAME* /media/ssd/YouTube
```
Once you are done, change the ownership to jellyfin
```
sudo chown -R jellyfin:jellyfin /media/ssd/YouTube
```
(It might be a good idea to just give yourself write permission but I havne't gotten there yet)

6. Library Scan (important!)
```
Dashboard → Libraries → YouTube → Scan Library
```
```
sudo systemctl restart jellyfin
```
Then refresh

## Part 4 - Enable Remote Streaming (Tailscale)
This is needed so you can watch your Jellyfin away from home
```
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up
```
Then Jellyfin URL becomes:
```
http://<your-tailscale-ip>:8096
```
This allows:
- secure remote access
- no port forwarding
- no DNS
- accessible anywhere
Highly recommended.

<br>
<img src="./img/pi-jellyfin-3.jpg" alt="pi screen" width="400"/>  

So you log in to prove you are who you are.  
Then you can connect your other devices.  

What is going on here?
You created a **private, encrypted network** that ONLY your devices can join.
This is called a **Tailnet**.  
It is like your own secret wifi. Your raspberry pi is now part of that private network.





## Part ? - Enable Hardware Acceleration (Pi 5 = fast)
This helps the videos run smoother
1. Install VAAPI Drivers
```
sudo apt install libva2 libva-drm2 libva-x11-2 vainfo mesa-va-drivers -y
```
2. Check hardware decode
```
vainfo
```
You should see something like:
```
h264_rpi5
hevc_rpi5
```
3. Enable in Jellyfin (Important)

## Part ? -
This is how you convert from asdflsdf to saldfjsldkf
```
ffmpeg -i yourfile.webm -c:v copy -c:a aac yourfile.mp4
```