*Pre-Requisite : Installed [Rclone](https://rclone.org/install/) & Google Drive [configuration](https://rclone.org/drive/).*


## Automate local file backup to google drive using rclone and systemd timer

* rclone.sh (script - source followed by destination)
```
#!/bin/bash
/usr/bin/rclone sync /home/omi/learning-cpp/ remote:backup/learning-cpp --verbose 
```
# Add the following files in /etc/systemd/system/

* rclone.service 
```
[Unit]
Description=RClone Backup

[Service]
Type=simple
User=omi
ExecStart=/usr/local/bin/rclone.sh

[Install]
WantedBy=timers.target
```
* rclone.timer 
```
[Unit]
Description=RClone Backup Timer

[Timer]
#Execute job if it missed a run due to machine being off
Persistent=true
User=omi
#Run 120 seconds after boot for the first time
OnBootSec=120
#Run every 1 hour thereafter
OnUnitActiveSec=3800
#File describing job to execute
Unit=rclone.service

[Install]
WantedBy=timers.target
```

* Enable timer and service
```
systemctl enable rclone.timer 
systemctl enable rclone.service
```
