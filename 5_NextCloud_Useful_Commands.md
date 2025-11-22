## How do I check where nextcloud currently stores its data?

### Check via the `config.php` file (recommended)
Nextcloud stores the data directory in its config file
1. SSH into your Raspberry Pi (or open terminal)
2. Navigate to Nextcloud config folder (usually `/var/www/nextcloud/config)`:
```
cd /var/www/nextcloud/config
```
3. Open `config.php`:
```
sudo nano config.php
```
4. Look for this line:
```
'datadirectory' => '/path/to/your/data',
```