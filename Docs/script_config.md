# Home Lab Partition Configuration and Automation Scripts

## Partition Overview

This document outlines the configured partitions and their intended purposes in the home lab setup.

### Partition Mapping

| Partition         | Mount Point           | Purpose                              |
|-------------------|-----------------------|--------------------------------------|
| /dev/nvme0n1p1    | /mnt/ios_storage      | ISO storage for system images        |
| /dev/nvme0n1p3    | /mnt/vm_storage       | Virtual Machine storage              |
| /dev/sda1         | /mnt/backup           | Backup storage                       |
| /dev/nvme0n1p2    | /mnt/storage          | General storage                      |

---

## Automation Scripts Overview

### 1. Logging Script

**Path:** `~/automation/log_script.sh`

**Log File:** `~/automation/automation_log.txt`

**Purpose:** Logs automated activities and system tasks for review and debugging.

---

### 2. Backup Script

**Path:** `~/automation/back_up.sh`

**Log File:** `~/automation/automation_log.txt`

**Purpose:** Performs automated backups of important files and directories to `/mnt/backup`.

---

### 3. Auto-Update Script

**Path:** `~/automation/auto_update.sh`

**Log File:** `~/automation/auto_update.log`

**Purpose:** Automatically updates the system and software packages, logging the update process for auditing.

---

### 4. VM Management Script

**Path:** `~/automation/manage_vms.sh`

**Status:** Written but not yet deployed (pending VM setup).

**Purpose:** Manages virtual machines, including start, stop, and configuration operations.

---

### 5. VM Snapshot Script

**Path:** `~/automation/snapshot_vm.sh`

**Status:** Written but not yet deployed (pending VM setup).

**Purpose:** Creates snapshots of virtual machines for backup and recovery purposes.

---

### 6. Mount Partitions Script

**Path:** `~/automation/mount_partitions.sh`

**Purpose:** Mounts all specified partitions automatically at boot or on demand. Ensures proper access to each storage location.

---

## Next Steps

1. Test and debug scripts related to VM management and snapshots.
2. Deploy and integrate the VM scripts once the VM environment is ready.
3. Push the finalized scripts and documentation to GitHub for version control and sharing.

---

## Notes

- Ensure all scripts have executable permissions:

```bash
chmod +x ~/automation/*.sh
```

- Add cron jobs for periodic execution if required:

```bash
crontab -e
```

Example entry for auto-update script:

```bash
0 2 * * * ~/automation/auto_update.sh
```

- Verify mount points before running scripts to avoid data loss.

