## Home Lab Storage and Partition Setup

### 1. Directory Creation
To ensure proper organization, I created directories for mounting the partitions:
```bash
sudo mkdir -p /mnt/backup /mnt/vm_storage /mnt/ios_storage /mnt/storage
```

---

### 2. Partition Identification
I used `blkid` to verify the UUIDs of the partitions, which are necessary for setting up `/etc/fstab`:
```bash
blkid
```

Here are the identified partitions and their intended purposes:
- `/dev/nvme0n1p1` -> `/mnt/ios_storage` (ISO storage for system images)
- `/dev/nvme0n1p3` -> `/mnt/vm_storage` (Virtual Machine storage)
- `/dev/sda1` -> `/mnt/backup` (Backup storage)
- `/dev/nvme0n1p2` -> `/mnt/storage` (General storage)

---

### 3. Editing `/etc/fstab`
I updated the `/etc/fstab` file to enable automatic mounting of these partitions at boot. Here's the content of my `/etc/fstab` file:
```fstab
UUID=be6e25ce-6ff5-4555-ba6f-6028f006db7a /               ext4    defaults        0       1
UUID=A6FF-13DA        /boot/efi       vfat    umask=0077      0       1
UUID=a286ff93-f911-45af-aeef-66f84ccde69b /mnt/ios_storage ext4    defaults        0       2
UUID=72b2eaa9-acf7-4d80-ab0e-3dd63320072e /mnt/vm_storage  ext4    defaults        0       2
UUID=9d80bf8f-2f5-4136-84fd-1c76c70b82ee /mnt/backup      ext4    defaults        0       2
UUID=cf874947-b9eb-443e-a226-d308e14b2f90 /mnt/storage     ext4    defaults        0       2
```

---

### 4. Applying Changes
After editing the `/etc/fstab` file, I ran the following commands to apply the changes:
```bash
sudo mount -a
sudo systemctl daemon-reload
```

---

### 5. Verifying Mounts
To confirm that all partitions were mounted correctly, I used the `df -h` command:
```bash
df -h
```

The output was as follows:
```plaintext
Filesystem      Size  Used Avail Use% Mounted on
/dev/sdb2       233G   18G  204G   8% /
/dev/nvme0n1p1  254G   28K  241G   1% /mnt/ios_storage
/dev/nvme0n1p3  601G   28K  570G   1% /mnt/vm_storage
/dev/sda1       458G   28K  435G   1% /mnt/backup
/dev/nvme0n1p2   61G   24K   58G   1% /mnt/storage
```

---

### 6. Testing and Usage
Finally, I tested read/write permissions on the mounted directories to ensure they were functioning correctly:
```bash
sudo touch /mnt/backup/testfile
ls -l /mnt/backup/testfile
sudo rm /mnt/backup/testfile
```

I repeated this process for `/mnt/ios_storage`, `/mnt/vm_storage`, and `/mnt/storage` to verify everything worked as expected.

---

### Conclusion
This setup optimizes my home lab for VM storage, backups, and general use. With everything correctly mounted and verified, my system is now ready for advanced projects and experiments. This documentation will also serve as a reference for future modifications.


