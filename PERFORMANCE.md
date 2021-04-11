### Reversing recent changes

The odd thing about making changes on Linux (or any other system) is that the change itself might work perfectly when 
you make it, but in a day or two, your system performance suffers. Before you do anything else, check your change 
documentation to see if any recent changes were made to the system. Changes include software patches, updates of any 
kind, hardware replacements or upgrades, driver updates, firmware updates, code pushes, new software installs, and 
configuration changes.

###### Display the last 100 syslog messages  (Use /var/log/syslog for Debian based systems.)
`tail -100 /var/log/messages`

### Update, update, update

You can avoid performance problems associated with software and hardware bugs by keeping everything updated, 
especially when it comes to server-side software (rather than client-side, like a web browser). Client-side should be 
updated too, of course, but that's a different discussion.

> If your systems are up-to-date and there are no newer updates available, you can generally rule out updates and 
patches as a performance problem root cause.

### CPU

Check top to see if any processes are overloading your CPU(s). To sort top for CPU, run top and then type P (Shift+P). 
Look at the processes burning up your CPU cycles. Are the ones at the top of the list system-related or applications? 
If they're system processes, check your uptime. The uptime shouldn't be extremely high because of regular rebooting.

###### Display and manage the top processes
`top`

###### Interactive process viewer (top alternative)
`htop`

###### Display processor related statistics
`mpstat 1`

###### Display I/O statistics
`iostat 1`

If you find a particular application using an abnormal amount of CPU cycles, restart the application to see if the 
problem persists. If the process is system-related, try restarting the process if possible. If not, reboot the system. 

> to rule out a lot of issues, a good reboot solves a lot of problems and helps you diagnose hardware problems with 
>minimal effort. 

### Memory

#### Unnecessary Logging
The next most obvious place to look when troubleshooting performance is memory use. Memory problems can manifest 
themselves in different ways that obscure the fact that memory is indeed the problem. If you find that during the 
course of a day your system's memory is drained off, the first thing to check is **your logging**.

#### Swap
You should also look at swap space if you suspect a memory problem. In this output, my system is idle so the result 
isn't dramatic. Use the `free -m` command to check physical and virtual (swap) memory usage. 
If you're using a lot of swap, your system might be doing what *nix administrators call "thrashing." 
You don't want your system to thrash. Thrashing can also appear as a disk problem if it's severe enough. If your system 
is so busy paging in and out that it affects disk performance, you need to act immediately by restarting the offending 
process.

> A lot of modern systems have so much memory that disk-based swap isn't used at all. Some administrators feel that 
>it's a waste of disk space.

#### Programs 

Finally, errant programs can cause memory issues. Java-based programs have historically caused me the most grief. 
Some Java programmers don't program correctly for garbage cleanup or memory release, and problems ensue when loads are 
high or when certain calls are made. I always start by restarting the process. My next option is to check top for the 
amount of memory consumed by the program.

###### List all open files on the system
`lsof`

###### List files opened by user
`lsof -u user`

###### Display free and used memory ( -h for human readable, -m for MB, -g for GB.)
`free -h`

###### Display virtual memory statistics
`vmstat 1`


### Disk Usage

If you suspect a disk is your performance killer, the first thing to look at is available space with a quick df command:

###### Show free and used space on mounted filesystems
`df -h`

###### Execute "df -h", showing periodic updates
`watch df -h`

###### Show free and used inodes on mounted filesystems
`df -i`

###### Display disks partitions sizes and types
`fdisk -l`

###### Display disk usage for all files and directories in human readable format
`du -ah`

###### Display total disk usage off the current directory
`du -sh`

> The next item to check is if your filesystems are full or almost full. If none are, then you have a failed disk. 
> We can't simulate a disk failure, but some server systems let you know when they have failed disks. 

### Network

Network problems due to hardware are somewhat rare, but they do happen. 

###### Capture and display all packets on interface eth0
`tcpdump -i eth0`

###### Monitor all traffic on port 80 ( HTTP )
`tcpdump -i eth0 'port 80'`
