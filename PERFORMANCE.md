### Display and manage the top processes
`top`

#### Interactive process viewer (top alternative)
`htop`

#### Display processor related statistics
`mpstat 1`

#### Display virtual memory statistics
`vmstat 1`

#### Display I/O statistics
`iostat 1`

#### Display the last 100 syslog messages  (Use /var/log/syslog for Debian based systems.)
`tail -100 /var/log/messages`

#### Capture and display all packets on interface eth0
`tcpdump -i eth0`

#### Monitor all traffic on port 80 ( HTTP )
`tcpdump -i eth0 'port 80'`

#### List all open files on the system
`lsof`

#### List files opened by user
`lsof -u user`

#### Display free and used memory ( -h for human readable, -m for MB, -g for GB.)
`free -h`

#### Execute "df -h", showing periodic updates
`watch df -h`

# Disk Usage

# Show free and used space on mounted filesystems
df -h

# Show free and used inodes on mounted filesystems
df -i

# Display disks partitions sizes and types
fdisk -l

# Display disk usage for all files and directories in human readable format
du -ah

# Display total disk usage off the current directory
du -sh
