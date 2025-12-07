
Install the official yt-dlp binary
```
sudo apt update
sudo apt install curl -y
sudo curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp
sudo chmod a+rx /usr/local/bin/yt-dlp
```

Breakdown of curl command:
- `curl` is a tool for downloading content form the internet
- `L` leamsn to follow redirects if the URL redirects somewhere else
- `https:...` is the link to the binary file
- `o` /usr/local/bin/-dlp means 'save the downloaded file as this file name in this location'
    - Note: since `/usr/local/bin/yt-dlp` is in your systems $PATH, you can run `yt-dlp` from anywhere (and the file will show up in the same directory)


check with:
```
yt-dlp --version
```


to make an mp3... go to the folder you want the file to show up and: 
```
yt-dlp -x --audio-format mp3 "YOUR-LINK-HERE"
```