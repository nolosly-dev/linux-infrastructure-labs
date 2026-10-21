understanding and learning `df -h`, `df -i`, `du -sh`.


# First: desk space triage.

### Simulation:
**Tested the current space empty on the desk 'the virtual qemu desk'**
[root@localhost ~]# df -h  
Filesystem               Size  Used Avail Use% Mounted on  
==/dev/mapper/fedora-root   15G  2.6G   13G  17% /==
devtmpfs                 952M     0  952M   0% /dev  
tmpfs                    977M     0  977M   0% /dev/shm  
tmpfs                    391M  968K  390M   1% /run  
none                     1.0M     0  1.0M   0% /run/credentials/systemd-journald.service  
none                     1.0M     0  1.0M   0% /run/credentials/systemd-resolved.service  
tmpfs                    977M     0  977M   0% /tmp  
/dev/sda2                2.0G  478M  1.5G  25% /boot  
none                     1.0M     0  1.0M   0% /run/credentials/serial-getty@ttyS0.service  
none                     1.0M     0  1.0M   0% /run/credentials/getty@tty1.service 
tmpfs                    196M  4.0K  196M   1% /run/user/1000  

**Adding the extra desk usage simulation (ex: 200 of 1M, a 200M file):**
[root@localhost ~]# dd if=/dev/zero of=test_load.img bs=1M count=200 status=progress  
200+0 records in  
200+0 records out  
209715200 bytes (210 MB, 200 MiB) copied, 0.0811055 s, 2.6 GB/s

**Notice the increase in desk usage:**
[root@localhost ~]# df -h  
Filesystem               Size  Used Avail Use% Mounted on  
==/dev/mapper/fedora-root   15G  2.8G   13G  19% /==
devtmpfs                 952M     0  952M   0% /dev  
tmpfs                    977M     0  977M   0% /dev/shm  
tmpfs                    391M  968K  390M   1% /run  
none                     1.0M     0  1.0M   0% /run/credentials/systemd-journald.service  
none                     1.0M     0  1.0M   0% /run/credentials/systemd-resolved.service  
tmpfs                    977M     0  977M   0% /tmp  
/dev/sda2                2.0G  478M  1.5G  25% /boot  
none                     1.0M     0  1.0M   0% /run/credentials/serial-getty@ttyS0.service  
none                     1.0M     0  1.0M   0% /run/credentials/getty@tty1.service 
tmpfs                    196M  4.0K  196M   1% /run/user/1000


**Now, using du with the output pipelined to sort with -s for the biggest in size and -h for human readable.** 
[root@localhost ~]# du -sh * | sort -hr  
==200M    test_load.img==
4.0K    anaconda-ks.cfg

**Removing the file hogging the space**
[root@localhost ~]# rm -f test_load.img 

**Confirming**
[root@localhost ~]# du -sh * | sort -hr  
4.0K    anaconda-ks.cfg  
[root@localhost ~]# df -h  
Filesystem               Size  Used Avail Use% Mounted on  
==/dev/mapper/fedora-root   15G  2.6G   13G  17% /==
devtmpfs                 952M     0  952M   0% /dev  
tmpfs                    977M     0  977M   0% /dev/shm  
tmpfs                    391M  968K  390M   1% /run  
none                     1.0M     0  1.0M   0% /run/credentials/systemd-journald.service  
none                     1.0M     0  1.0M   0% /run/credentials/systemd-resolved.service  
tmpfs                    977M     0  977M   0% /tmp  
/dev/sda2                2.0G  478M  1.5G  25% /boot  
none                     1.0M     0  1.0M   0% /run/credentials/serial-getty@ttyS0.service  
none                     1.0M     0  1.0M   0% /run/credentials/getty@tty1.service 
tmpfs                    196M  4.0K  196M   1% /run/user/1000


---
# Second: inodes consumption.

**testing df -i, for inodes incidents. created a test directory and cd-ed into it:**
[root@localhost ~]# mkdir /tmp/inode_test && cd /tmp/inode_test  
[root@localhost inode_test]#

**Double checked the inode usage of /tmp before simulating inodes usage:**
[root@localhost inode_test]# df -i  
Filesystem               Inodes IUsed   IFree IUse% Mounted on  
/dev/mapper/fedora-root 7864320 65298 7799022    1% /  
devtmpfs                 243596   544  243052    1% /dev  
tmpfs                    249994     1  249993    1% /dev/shm  
tmpfs                    819200   885  818315    1% /run  
none                       1024     2    1022    1% /run/credentials/systemd-journald.service  
none                       1024     2    1022    1% /run/credentials/systemd-resolved.service  
==tmpfs                   1048576    26 1048550    1% /tmp==
/dev/sda2               1048576   364 1048212    1% /boot  
none                       1024     2    1022    1% /run/credentials/serial-getty@ttyS0.service  
none                       1024     2    1022    1% /run/credentials/getty@tty1.service  
tmpfs                     49998    21   49977    1% /run/user/1000


**AI advised with this for loop `for i in {1..10000}; do touch file_$i; done` to create a simulation of chunks or inodes consumption, checking:**
[root@localhost inode_test]# df -i  
Filesystem               Inodes IUsed   IFree IUse% Mounted on  
/dev/mapper/fedora-root 7864320 65298 7799022    1% /  
devtmpfs                 243596   544  243052    1% /dev  
tmpfs                    249994     1  249993    1% /dev/shm  
tmpfs                    819200   885  818315    1% /run  
none                       1024     2    1022    1% /run/credentials/systemd-journald.service  
none                       1024     2    1022    1% /run/credentials/systemd-resolved.service  
==tmpfs                   1048576 10925 1037651    2% /tmp==
/dev/sda2               1048576   364 1048212    1% /boot  
none                       1024     2    1022    1% /run/credentials/serial-getty@ttyS0.service  
none                       1024     2    1022    1% /run/credentials/getty@tty1.service  
tmpfs                     49998    21   49977    1% /run/user/1000


**noticeably, the space from before is still the same:**
*Before:*
[root@localhost ~]# df -h  
Filesystem               Size  Used Avail Use% Mounted on  
/dev/mapper/fedora-root   15G  2.6G   13G  17% / 
devtmpfs                 952M     0  952M   0% /dev  
tmpfs                    977M     0  977M   0% /dev/shm  
tmpfs                    391M  968K  390M   1% /run  
none                     1.0M     0  1.0M   0% /run/credentials/systemd-journald.service  
none                     1.0M     0  1.0M   0% /run/credentials/systemd-resolved.service  
==tmpfs                    977M     0  977M   0% /tmp==
/dev/sda2                2.0G  478M  1.5G  25% /boot  
none                     1.0M     0  1.0M   0% /run/credentials/serial-getty@ttyS0.service  
none                     1.0M     0  1.0M   0% /run/credentials/getty@tty1.service
tmpfs                    196M  4.0K  196M   1% /run/user/1000

*After:*
[root@localhost inode_test]# df -h  
Filesystem               Size  Used Avail Use% Mounted on  
/dev/mapper/fedora-root   15G  2.6G   13G  17% /  
devtmpfs                 952M     0  952M   0% /dev  
tmpfs                    977M     0  977M   0% /dev/shm  
tmpfs                    391M  968K  390M   1% /run  
none                     1.0M     0  1.0M   0% /run/credentials/systemd-journald.service  
none                     1.0M     0  1.0M   0% /run/credentials/systemd-resolved.service  
==tmpfs                    977M     0  977M   0% /tmp==
/dev/sda2                2.0G  478M  1.5G  25% /boot  
none                     1.0M     0  1.0M   0% /run/credentials/serial-getty@ttyS0.service  
none                     1.0M     0  1.0M   0% /run/credentials/getty@tty1.service 
tmpfs                    196M  4.0K  196M   1% /run/user/1000 


**a command that can be used where it sorts the biggest ever inode consumption to triage such an incident:**
`find / -type f | cut -d/ -f1-3 | sort | uniq -c | sort -hr | head -n 10`


[root@localhost ~]# find / -type f | cut -d/ -f1-3 | sort | uniq -c | sort -hr | head -n 10  
 55566 /sys/kernel  
 22910 /usr/share  
 22816 /usr/lib  
 ==10000 /tmp/inode_test==
  5995 /sys/devices  
  5875 /sys/fs  
  4170 /usr/lib64  
  2317 /sys/module  
  1349 /var/lib  
  1258 /usr/bin  


**Removing the inodes consuming directory:**
[root@localhost ~]# rm -fr /tmp/inode_test/

**Confirmation:**
[root@localhost ~]# df -i /tmp/  
Filesystem      Inodes IUsed   IFree IUse% Mounted on  
tmpfs          1048576    25 1048551    1% /tmp
[root@localhost ~]# find / -type f | cut -d/ -f1-3 | sort | uniq -c | sort -hr | head -n 10
  55566 /sys/kernel
  22910 /usr/share
  22816 /usr/lib
   5995 /sys/devices
   5875 /sys/fs
   4170 /usr/lib64
   2317 /sys/module
   1349 /var/lib
   1258 /usr/bin
   1135 /proc/sys
