# SSH Server Configuration for OptiPlex 3050 and 7050 Communication

This guide outlines the process to configure SSH server settings on the OptiPlex 3050 and 7050, ensuring secure communication between the two machines.

## Step 1: Edit SSH Configuration

### 1. Open the SSH configuration file:

```bash
sudo nano /etc/ssh/sshd_config
```
Ensure the following settings are enabled in the file:
  

    PubkeyAuthentication yes
    AuthorizedKeysFile .ssh/authorized_keys
    PasswordAuthentication yes  # Optional, for fallback if needed
Save and close the file (CTRL + X, then Y to confirm).

### Step 2: Restart SSH Service

After making changes, restart the SSH service to apply the new configuration:

 ```
sudo systemctl restart ssh
```

### Step 3: Copy Public Key to Authorized Keys

Display the public key to copy from each machine:

```
cat ~/.ssh/id_ed25519.pub
```

Copy the output and append it to the
```
~/.ssh/authorized_keys
```
 file on both the OptiPlex 3050 and 7050.

### Step 4: Set Correct Permissions

Ensure that the .ssh directory and authorized_keys file have the correct permissions:
```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

### Step 5: Test SSH Access

To test access between the two machines:

From OptiPlex 3050 to OptiPlex 7050:

```
ssh user@192.168.1.142 -p [custom port]
```

From OptiPlex 7050 to OptiPlex 3050:
```
ssh user@192.168.1.181 -p [custom port]
```
