# Backup Script (backup.sh)
This script automates backups of the /mnt/storage directory to /mnt/backup.

-----

## Create/Edit backup.sh:

```
bash
nano ~/automation/backup.sh
```

-----
## Script Contents:

```
bash
#!/bin/bash

# Backup source and destination
SOURCE_DIR="/mnt/storage"
DEST_DIR="/mnt/backup"

# Perform backup using rsync
rsync -av --delete $SOURCE_DIR $DEST_DIR >> /home/troyedmonds/automation_log.txt 2>&1
log_message "Backup from $SOURCE_DIR to $DEST_DIR completed"

```
----

Make the script executable:

```
bash
chmod +x ~/automation/backup.sh
```
