# backup-system-drive-to-meganz
Backup your linux system drive directly to your mega.nz account. 


You need to have megacmd already working in your system. 
https://mega.nz/linux/repo/ <--download repo 
if you're only in command line you can use curl. For example: `curl -O https://mega.nz/linux/repo/xUbuntu_23.04/amd64/megacmd_1.6.3-1.1_amd64.deb`
https://mega.io/cmd <--choose your system and run command with proper path

or you can check their github repo: https://github.com/meganz/MEGAcmd

after installation, try to login
check out their manual:
https://github.com/meganz/MEGAcmd/blob/master/UserGuide.md#login-logout-whoami-mkdir-cd-get-put-du-mount-example

Be sure to have megacmd working at this point.


Make note of your system drive device name. You can check it by running:
`lsblk -o NAME,TYPE,MOUNTPOINT`
Look for drives that have some partitions with names like boot boot/efi
```nvme3n1                   disk
├─nvme3n1p1               part  /boot/efi
├─nvme3n1p2               part  /boot
└─nvme3n1p3               part
  └─ubuntu--vg-ubuntu--lv lvm   /```
In this case, the proper name for system drive will be `/dev/nvme3n1`

Run `su` to place system_backup_to_mega.sh file to some safe spot that only root have access. I have dedicated place for scripts.

Make chmod on the file
`chmod +x /path/to/system_backup_to_mega.sh`

Make edits in the file `nano system_backup_to_mega.sh` in order to put your credentials, your disk drive path and folders for keeping temporary backups. Do it right.
Run this script manually by using `sh system_backup_to_mega.sh`

It's good to take a look on your active processes to confirm that everything is working. 
Try using `bashtop` for doing that. 
If you see DD in the first part of the process, that means that system drive clone to iso is working.



If everything worked as it should and you can see your file in your mega account you can try to put this file to automatic executing by using `crontab -e`
Put a new line in there:
`0 3 * * * ~/path/to/system_backup_to_mega.sh` that will execute this script every day at 3am

If you don't know how to setup cron times: https://tool.crontap.com/cronjob-debugger this one is kinda nice to spit or just ask chatgpt
