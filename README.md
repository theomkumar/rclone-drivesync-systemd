# rclone-drivesync-systemd

//Automate local file backup to google drive using rclone and systemd timer.

STEPS:-
1. rclone.sh (required script) 

2. Add the following files in /etc/systemd/system/
  (i) rclone.timer 
  (ii)rclone.service 
  
3. (i) systemctl enable rclone.timer 
   (ii)systemctl enable rclone.service
