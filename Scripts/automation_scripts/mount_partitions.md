# Mount Partitions Script (mount_partitions.sh)

This script ensures that the necessary storage partitions are mounted at startup.

## Create/Edit mount_partitions.sh:

```

nano ~/automation/mount_partitions.sh
```
----

## Script Contents:

```

#!/bin/bash

# Mount partitions if not mounted
if ! mount | grep -q "/mnt/ios_storage"; then
    sudo mount /dev/nvme0n1p1 /mnt/ios_storage
    log_message "Mounted /dev/nvme0n1p1 to /mnt/ios_storage"
fi

if ! mount | grep -q "/mnt/vm_storage"; then
    sudo mount /dev/nvme0n1p3 /mnt/vm_storage
    log_message "Mounted /dev/nvme0n1p3 to /mnt/vm_storage"
fi

if ! mount | grep -q "/mnt/backup"; then
    sudo mount /dev/sda1 /mnt/backup
    log_message "Mounted /dev/sda1 to /mnt/backup"
fi

if ! mount | grep -q "/mnt/storage"; then
    sudo mount /dev/nvme0n1p2 /mnt/storage
    log_message "Mounted /dev/nvme0n1p2 to /mnt/storage"
fi
```

----

## Make the script executable:

```

chmod +x ~/automation/mount_partitions.sh
```
