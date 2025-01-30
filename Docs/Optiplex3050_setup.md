# Dell OptiPlex 3050 Home Lab Setup

## **1. Install Ubuntu Linux on SATA SSD (256GB)**

### **System Update & Upgrade**
```bash
sudo apt update && sudo apt dist-upgrade -y
```

### **Create a Non-Root User**
```bash
sudo adduser <your-username>
sudo passwd <your-username>
sudo usermod -aG sudo <your-username>
```
Verify the user was created:
```bash
ls /home
```

### **Set Hostname**
```bash
sudo hostnamectl set-hostname <new-hostname>
```
Verify:
```bash
hostname
```
Update hosts file:
```bash
sudo nano /etc/hosts
```

### **Setup SSH Access**
Generate SSH key:
```bash
ssh-keygen
```
Copy key to server:
```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub <your-username>@<server-ip>
```
Log in via SSH:
```bash
ssh <your-username>@<server-ip>
```
Disable password authentication for security:
```bash
sudo nano /etc/ssh/sshd_config
```
Set:
```plaintext
PermitRootLogin no
PasswordAuthentication no
Port <custom-port>
AddressFamily inet
```
Restart SSH service:
```bash
sudo systemctl restart sshd
```

### **Enable & Configure Firewall**
```bash
sudo ufw enable
sudo ufw allow <custom-port>/tcp
sudo ufw deny 22/tcp
```
Disable ICMP ping requests:
```bash
sudo nano /etc/ufw/before.rules
```
Add:
```plaintext
-A ufw-before-input -p icmp --icmp-type echo-request -j DROP
```
Or update sysctl:
```bash
sudo nano /etc/sysctl.conf
```
Add:
```plaintext
net.ipv4.icmp_echo_ignore_all=1
```
Apply changes:
```bash
sudo sysctl -p
```

### **Enable Automatic Updates**
```bash
sudo apt install unattended-upgrades -y
sudo dpkg-reconfigure --priority=low unattended-upgrades
```

---

## **2. Partition & Mount Drives**
### **Install GParted**
```bash
sudo apt install gparted -y
```

### **Partition & Label Drives**
#### **NVMe SSD (1TB)**
- **ISO Storage** (100GB) → `~/Drives/iso_storage`
- **VM Storage** (800GB) → `~/Drives/vm_storage`
- **High-Speed Storage** (71.51GB) → `~/Drives/highspeed_storage`

#### **SATA SSD (256GB) [Primary OS]**
- Root (`/`)
- EFI Boot (`/boot/efi`)
- General Storage (20GB) → `~/Drives/general`

#### **HDD (500GB)**
- **Backup Storage** (300GB) → `~/Drives/backup`
- **Media Storage** (165.76GB) → `~/Drives/media`

### **Create Mount Points**
```bash
mkdir -p ~/Drives/iso_storage
mkdir -p ~/Drives/vm_storage
mkdir -p ~/Drives/highspeed_storage
mkdir -p ~/Drives/backup
mkdir -p ~/Drives/media
mkdir -p ~/Drives/general
```

### **Update /etc/fstab for Persistent Mounting**
```bash
sudo nano /etc/fstab
```
Add:
```plaintext
/dev/nvme0n1p1  /home/<your-username>/Drives/iso_storage       ext4    defaults 0 2
/dev/nvme0n1p2  /home/<your-username>/Drives/vm_storage        ext4    defaults 0 2
/dev/nvme0n1p3  /home/<your-username>/Drives/highspeed_storage ext4    defaults 0 2
/dev/sda1       /home/<your-username>/Drives/backup            ext4    defaults 0 2
/dev/sda2       /home/<your-username>/Drives/media             ext4    defaults 0 2
/dev/sdb1       /home/<your-username>/Drives/general           ext4    defaults 0 2
```
Save & Exit.

### **Verify Mounts**
```bash
sudo mount -a
df -h
```

### **Set Ownership & Permissions**
```bash
sudo chown -R <your-username>:<your-username> ~/Drives/*
sudo chmod -R 775 ~/Drives/*
```

### **Reload System Daemon**
```bash
sudo systemctl daemon-reload
```

### **Test Setup**
```bash
touch ~/Drives/vm_storage/testfile
```

