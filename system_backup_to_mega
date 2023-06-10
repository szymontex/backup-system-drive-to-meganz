#!/bin/bash
DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_NAME="system_backup_$DATE"
BACKUP_FILE="$BACKUP_NAME.iso"
MEGA_FOLDER="/path/to/your/desired/backup/folder"
MEGA_USER="<USERNAME>"
MEGA_PASS="<PASSWORD>"


# Download latest backup name
LATEST_BACKUP=$(ls -t /path/to/your/desired/backup/folder/ | head -1)

# Check if the newest backup is new enough
if [ -n "$LATEST_BACKUP" ]; then
    LATEST_BACKUP_TIME=$(stat -c %Y /path/to/your/desired/backup/folder/$LATEST_BACKUP)
    CURRENT_TIME=$(date +%s)
    TIME_DIFF=$((CURRENT_TIME-LATEST_BACKUP_TIME))

    # If file is older than hour change 3600 as desired time in seconds
    if [ $TIME_DIFF -gt 3600 ]; then
        sudo dd if=/dev/<YOURSYSTEMDRIVE> of=/path/to/your/desired/backup/folder/$BACKUP_FILE bs=1M
    else
        BACKUP_FILE=$LATEST_BACKUP
    fi
else
    sudo dd if=/dev/<YOURSYSTEMDRIVE> of=/path/to/your/desired/backup/folder/$BACKUP_FILE
    fi

# Send file to mega.nz . Ofc you need to have your mega-cmd app configured in your system
if mega-put /path/to/your/desired/backup/folder/$BACKUP_FILE $MEGA_FOLDER; then
    echo "Mega.nz upload successful, removing local backup file..."
    rm /path/to/your/desired/backup/folder/$BACKUP_FILE
else
    echo "Mega.nz upload failed, keeping local backup file..."
