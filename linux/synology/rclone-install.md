# Rclone - Install

#### 群晖开机自动挂载脚本

```bash
#!/bin/bash
#!/usr/bin/rclone
# Make script executable with: chmod a+x /root/scripts/nas-mountOnStartup.sh

/usr/bin/rclone mount driveteamspacesh: /volume1/video/DriveSpaceSH \--config=/root/.config/rclone/rclone.conf \--allow-other \--dir-cache-time 672h \--vfs-cache-max-age 675h \--vfs-read-chunk-size 64M \--vfs-read-chunk-size-limit 1G \--buffer-size 32M &
	
exit
```



