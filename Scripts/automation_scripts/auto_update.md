# Step 1: Create a Script for Updates
Open terminal and create a new script file:

```
nano /home/troyedmonds/auto_update.sh
```

---

## Add the following commands to the script to update and upgrade the system:

```
#!/bin/bash

# Update package list
sudo apt update -y

# Upgrade packages
sudo apt upgrade -y

# Dist-upgrade (handles dependencies, new packages, and removals)
sudo apt dist-upgrade -y

# Perform a full upgrade
sudo apt full-upgrade -y

# Clean up unused packages
sudo apt autoremove -y
sudo apt autoclean -y
```
---

## Make the script executable:

```
chmod +x /home/troyedmonds/auto_update.sh
```
