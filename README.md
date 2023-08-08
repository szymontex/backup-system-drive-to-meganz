# Backup System Drive to Mega.nz

Automate your Linux system drive backup process, sending it directly to your Mega.nz account using the `backup-system-drive-to-meganz` script.

## Prerequisites

- You need to have `megacmd` already working in your system:
    - Download the repo from [mega.nz linux repo](https://mega.nz/linux/repo/)
    - If you're only in the command line, you can use `curl`. For example: 
      ```
      curl -O https://mega.nz/linux/repo/xUbuntu_23.04/amd64/megacmd_1.6.3-1.1_amd64.deb
      ```
    - Choose your system and run the command with the proper path from [here](https://mega.io/cmd).
    - For more details, you can check their GitHub repo: [MEGAcmd GitHub](https://github.com/meganz/MEGAcmd).
    
- After installation, try to login. Check out their manual on GitHub: [MEGAcmd User Guide](https://github.com/meganz/MEGAcmd/blob/master/UserGuide.md#login-logout-whoami-mkdir-cd-get-put-du-mount-example). Ensure that `megacmd` is working at this point.

## Setup

1. **Determine System Drive Device Name**: 
   - Run `lsblk -o NAME,TYPE,MOUNTPOINT` to check your system drive device name. Look for drives that have some partitions with names like `boot` or `boot/efi`.
   
     Example Output:
     ```
     nvme3n1                   disk
     ├─nvme3n1p1               part  /boot/efi
     ├─nvme3n1p2               part  /boot
     └─nvme3n1p3               part
       └─ubuntu--vg-ubuntu--lv lvm   /
     ```
     In this case, the proper name for the system drive will be `/dev/nvme3n1`.

2. **Script Placement**:
   - Place `system_backup_to_mega.sh` in a directory only accessible by the root user.
   - Run `chmod +x /path/to/system_backup_to_mega.sh` to make the script executable.

3. **Modify the Script**:
   - Edit the script to set your credentials, disk drive path, and folders for temporary backups.
   
     ```bash
     nano system_backup_to_mega.sh
     ```
   
4. **Run Manually**: 
   - Execute the script manually using:
   
     ```bash
     sh system_backup_to_mega.sh
     ```
   
   - Monitor active processes in another terminal window to ensure everything is running correctly. Use `bashtop` or similar tools to do so.

5. **Automate with CRON**:
   - If everything works correctly and you can see your backup file in your Mega.nz account, you can automate the backup process using CRON:
   
     ```bash
     crontab -e
     ```
   
   - Add a new line to execute the script every day at 3 am:
   
     ```bash
     0 3 * * * ~/path/to/system_backup_to_mega.sh
     ```

6. **CRON Timing**:
   - If you're unfamiliar with setting up CRON timings, you can use online tools like [CronTab](https://tool.crontap.com/cronjob-debugger) or simply ask here for guidance.

## Note

Using this script, your system will automatically create a backup of your drive and upload it to your Mega.nz account. Always ensure to test backup scripts in a controlled environment before deploying to ensure data integrity and prevent data loss.

