# SyncFolders
This guide explains how to sync folders like notes and other data locally between phone and laptop using GSconnect and rsync

## Steps are:
### Install GSconnect extension from Gnome Extension Manager

### Install KDEconnect application from the Play Store

### Pair and connect the phone and the laptop
Note: You may need to install openssl in fedora to use GSconnect.
sudo dnf install openssl

### Use the pre provided rsync tool to sync notes and folders
The command for this is:
rync -av --delete "/home/USER/PATH/TO/FOLDER" "/run/user/1001/gvfs/sftp:host=192.168.1.5,port=1739/storage/emulated/0/PATH/TO/MOBILE/FOLDER"
Replace USER with user's Home Folder
  & /PATH/TO/FOLDER with the folder that you want to sync with mobile.
  & /PATH/TO/MOBILE/FOLDER with the folder where you want to store the synced files and folders.

Note: You may enable bidirectional syncing just by interchanging the source and the destination paths in the rsync command.

### (OPTIONAL) Automate
Save the following 4 lines as GSconnectRsync.sh
#!/bin/bash
SOURCE=~/PATH/TO/FOLDER
DEST="/run/user/1001/gvfs/sftp:host=192.168.1.5,port=1739/storage/emulated/0/PATH/TO/MOBILE/FOLDER"
rsync -av --delete "$SOURCE" "$DEST"

Now edit the crontab
  crontab-e
Then add the following line
  */15 * * * * /home/your_username/GSconnectRsync.sh >> /home/your_username/scripts/GSconnectRsync.log 2>&1
