# Linux-Real-Time-Hardware-Usage-Monitor
Certainly! Below is a simple Bash script that monitors real-time hardware usage, including CPU, memory, and disk usage. This script uses common Linux utilities like top, free, and df.

#!/bin/bash

# Function to display CPU usage
cpu_usage() {
    echo "CPU Usage:"
    top -bn1 | grep "Cpu(s)" | \
    sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | \
    awk '{print 100 - $1"%"}'
}

# Function to display Memory usage
memory_usage() {
    echo "Memory Usage:"
    free -m | awk 'NR==2{printf "Memory Usage: %s/%sMB (%.2f%%)\n", $3, $2, $3*100/$2 }'
}

# Function to display Disk usage
disk_usage() {
    echo "Disk Usage:"
    df -h | awk '$NF=="/"{printf "Disk Usage: %d/%dGB (%s)\n", $3, $2, $5}'
}

# Infinite loop to update the usage every 5 seconds
while true; do
    clear
    echo "Real-Time Hardware Usage Monitor"
    echo "==============================="
    cpu_usage
    memory_usage
    disk_usage
    echo "==============================="
    sleep 5
done





How to Use the Script
Save the script: Save the script to a file, for example, monitor.sh.
Make it executable: Run chmod +x monitor.sh to make the script executable.
Run the script: Execute the script by running ./monitor.sh.
This script will continuously update the CPU, memory, and disk usage every 5 seconds. You can adjust the sleep interval as needed. Enjoy monitoring your system!
