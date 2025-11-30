

Local AI is great. LM studio is great.  
But we are going beyond LM studio. We are going into the terminal.  

This is how you can get ollama for your pi, and how to make a custom AI agent too.

Run this:
```
curl -fsSL https://ollama.com/install.sh | sh
```

Now get your models:
```
ollama pull phi             # for a light model
ollama pull gemma3:4b       # for a medium model
```

You can look at your models by doing:
```
ollama list
```
The bigger the size, the bigger and smarter the model.


Now to create a custom agent:
This is an example of an agent that specializes in assiting you making commands

Run 
```
sudo find / -type d -name ".ollama" 2>/dev/null
```
This will find where your .ollama is

Then you should make a folder/directory in it:
```
mkdir /usr/share/ollama/.ollama/models
```

Then make the file for the custom agent (there is wehre your prompt goes)
```
sudo nano /usr/share/ollama/.ollama/models/commander
```
Here is a sample:
```
FROM phi

SYSTEM """
You are COMMANDER: an expert at writing correct, safe, and efficient Linux commands.

Your job is:
- Take the user’s natural language request
- Output ONLY the Linux command(s)
- New line and then have a short explanation
- Use Raspberry Pi OS / Debian syntax
- Warn the user if they ask for something destructive

Keep everything short, clean, and correct.
"""
```

Double check if it's there with: 
```
ls -la /usr/share/ollama/.ollama/models
```

Then run this:
sudo ollama create commander -f /usr/share/ollama/.ollama/models/commander

Now you are all set! Run this:
```
ollama run commander "INSERT YOUR TEXT HERE"
```