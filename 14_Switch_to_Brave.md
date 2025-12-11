
The default browser on raspberry pi is DuckDuckGo.  
Duckduckgo isn't bad its a very simple privacy browser.  

But Brave is better:
- Built in tracking blocking
- Built in ad blocking
- Option for incognito with Tor
- Its faster and stronger: Brave is built on chromium, so it runs smooths and faster than DDG on a Pi 5
- Hardware accelerations: Brave can use the Pi's GPU for video decoding more reliably than DDG. So its better for video
- Better extension support
- Better UI

## 🛠️ How to Install Brave on Raspberry Pi OS
You only need 3 commands. 
1. Add Brave’s key
```
sudo apt install curl -y
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg \
  https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
```

2. Add Brave repo
```
echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] \
https://brave-browser-apt-release.s3.brave.com/ stable main" | \
sudo tee /etc/apt/sources.list.d/brave-browser-release.list
```

3. Install Brave
```
sudo apt update
sudo apt install brave-browser -y
```


## Now to set it up as your default broswer (using the terminal):
Run:
```
xdg-settings set default-web-browser brave-browser.desktop
```

If you want to verify:
```
xdg-settings get default-web-browser
```