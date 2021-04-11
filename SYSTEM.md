## Linux General Information

#### Display Linux system information and kernel release information
`uname -a`

#### Display kernel release information
`uname -r`

#### Show which version of Linux installed
`cat /etc/*-release`

#### Show how long the system has been running + load
`uptime`

#### Show system host name
`hostname`

#### Display all local IP addresses of the host.
`hostname -I`

#### Show system reboot history
`last reboot`

#### Show the current date and time
`date`

## Users information

#### Display who is online
`w`

#### Who you are logged in as
`whoami`

## Hardware Information
#### Display messages in kernel ring buffer
`dmesg`

#### Display CPU information
`cat /proc/cpuinfo`

#### Display memory information
`cat /proc/meminfo`

#### Display free and used memory ( -h for human readable, -m for MB, -g for GB.)
`free -h`

#### Display PCI devices
`lspci -tv`

#### Display USB devices
`lsusb -tv`

#### Display DMI/SMBIOS (hardware info) from the BIOS
`dmidecode`

#### Show info about disk sda
`hdparm -i /dev/sda`

#### Perform a read speed test on disk sda
`hdparm -tT /dev/sda`

#### Test for unreadable blocks on disk sda
`badblocks -s /dev/sda`
