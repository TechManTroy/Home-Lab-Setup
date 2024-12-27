# Scripts for Automation
A. Logging Script (log_script.sh)
This script will log actions and timestamps to a file (automation_log.txt) for tracking automated tasks.

Create/Edit log_script.sh:


```
nano ~/automation/log_script.sh
```
------

## Script Contents:


```

#!/bin/bash
# Combined Linux System and Automation Logging Script
# Tracks changes, updates, errors, alerts, and automation tasks.

# --- CONFIGURATION ---
LOG_DIR="$HOME/system_logs"
LOG_FILE="$LOG_DIR/system_activity.log"
ERROR_LOG="$LOG_DIR/system_errors.log"
ALERT_LOG="$LOG_DIR/system_alerts.log"
SYSTEM_INFO_LOG="$LOG_DIR/system_info.log"
AUTOMATION_LOG="$LOG_DIR/automation_log.txt"

# Ensure log directory exists
mkdir -p "$LOG_DIR"

# --- LOGGING FUNCTIONS ---

# General logging function
log_message() {
    echo "$(date) - $1" >> "$AUTOMATION_LOG"
}

# Log system updates
function log_updates() {
    echo "\n[UPDATES] - $(date)" >> "$LOG_FILE"
    sudo apt update &>> "$LOG_FILE"
    sudo apt upgrade -y &>> "$LOG_FILE"
    echo "System updates logged." >> "$LOG_FILE"
    log_message "System updates completed."
}

# Log changes to mounted storage
function log_storage_changes() {
    echo "\n[STORAGE CHANGES] - $(date)" >> "$LOG_FILE"
    df -h | grep '/mnt/' >> "$LOG_FILE"
    echo "Storage changes logged." >> "$LOG_FILE"
    log_message "Storage changes logged."
}

# Log system errors
function log_errors() {
    echo "\n[ERRORS] - $(date)" >> "$ERROR_LOG"
    journalctl -p err --since "1 hour ago" &>> "$ERROR_LOG"
    echo "Errors logged." >> "$ERROR_LOG"
    log_message "Error logs updated."
}

# Log system alerts (high priority logs)
function log_alerts() {
    echo "\n[ALERTS] - $(date)" >> "$ALERT_LOG"
    journalctl -p alert --since "1 hour ago" &>> "$ALERT_LOG"
    echo "Alerts logged." >> "$ALERT_LOG"
    log_message "Alert logs updated."
}

# Log system information
function log_system_info() {
    echo "\n[SYSTEM INFO] - $(date)" >> "$SYSTEM_INFO_LOG"
    echo "Uptime:" >> "$SYSTEM_INFO_LOG"
    uptime >> "$SYSTEM_INFO_LOG"
    echo "Memory Usage:" >> "$SYSTEM_INFO_LOG"
    free -h >> "$SYSTEM_INFO_LOG"
    echo "Disk Usage:" >> "$SYSTEM_INFO_LOG"
    df -h >> "$SYSTEM_INFO_LOG"
    echo "Running Processes:" >> "$SYSTEM_INFO_LOG"
    ps aux --sort=-%mem | head -n 10 >> "$SYSTEM_INFO_LOG"
    echo "System information logged." >> "$SYSTEM_INFO_LOG"
    log_message "System info logged."
}

# Log user activity
function log_user_activity() {
    echo "\n[USER ACTIVITY] - $(date)" >> "$LOG_FILE"
    last -a | head -n 10 >> "$LOG_FILE"
    echo "Recent login activity logged." >> "$LOG_FILE"
    log_message "User activity logged."
}

# Rotate logs if size exceeds 10MB
function rotate_logs() {
    for file in "$LOG_FILE" "$ERROR_LOG" "$ALERT_LOG" "$SYSTEM_INFO_LOG" "$AUTOMATION_LOG"; do
        if [ -f "$file" ] && [ $(stat -c%s "$file") -gt 10485760 ]; then
            mv "$file" "$file.$(date +%Y%m%d%H%M%S).bak"
            > "$file"
        fi
    done
    log_message "Log files rotated."
}

# --- MAIN FUNCTION ---
function log_all() {
    log_message "Starting logging session."
    rotate_logs
    log_updates
    log_storage_changes
    log_errors
    log_alerts
    log_system_info
    log_user_activity
    log_message "Logging session completed."
}

# Execute logging function
log_all

log_message "Automation script executed successfully."
echo "Logs have been updated. Check $LOG_DIR for details."


```
-----
## Make the script executable:

```

chmod +x ~/automation/log_script.sh
```

