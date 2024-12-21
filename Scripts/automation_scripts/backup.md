# Backup Script (backup.sh)
This script automates backups of the /mnt/storage directory to /mnt/backup.

-----

## Create/Edit backup.sh:

```
nano ~/automation/backup.sh
```

-----
## Script Contents:

```

#!/bin/bash

# Define source and destination directories
SOURCE_DIR="/mnt/storage"
DEST_DIR="/mnt/backup"

# Log the start of the backup process
~/automation/log_script.sh "Starting backup from $SOURCE_DIR to $DEST_DIR"

# Perform backup using rsync
rsync -av --delete $SOURCE_DIR $DEST_DIR >> /home/troyedmonds/automation_log.txt 2>&1

# Log the completion of the backup process
~/automation/log_script.sh "Backup from $SOURCE_DIR to $DEST_DIR completed"

```
----

## Make the script executable:

```
chmod +x ~/automation/backup.sh
```
