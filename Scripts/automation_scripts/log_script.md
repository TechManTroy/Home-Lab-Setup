# Scripts for Automation
A. Logging Script (log_script.sh)
This script will log actions and timestamps to a file (automation_log.txt) for tracking automated tasks.

Create/Edit log_script.sh:


```bash
nano ~/automation/log_script.sh
```
------

## Script Contents:


```
bash
#!/bin/bash

# Define log file location
LOG_FILE="/home/troyedmonds/automation_log.txt"

# Function to log messages with timestamp
log_message() {
    echo "$(date) - $1" >> $LOG_FILE
}

# Example usage:
log_message "Started automation task"

```
-----
## Make the script executable:

```
bash
chmod +x ~/automation/log_script.sh
```

