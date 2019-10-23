Disk partitioning using fdisk
------------------------------------
<li>Partitions listed from a host machine(Desktop / laptop) </li>
<pre>
(base) blrk@rk-lpc:~> lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0 931.5G  0 disk 
├─sda1   8:1    0   300M  0 part /boot/efi
├─sda2   8:2    0    32G  0 part [SWAP]
├─sda3   8:3    0   100G  0 part /boot/grub2/x86_64-efi
├─sda4   8:4    0   200G  0 part /home
└─sda5   8:5    0 599.2G  0 part /rkdrive
sr0     11:0    1  1024M  0 rom
</pre>

<li> List the Partitions of a VM(Virtual Machine) </li>
<pre>
blrk@linux-jbz9:~> lsblk
NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
sr0     11:0    1   4G  0 rom  
vda    253:0    0  16G  0 disk 
├─vda1 253:1    0   2G  0 part [SWAP]
└─vda2 253:2    0  14G  0 part /usr/local
</pre>

<li>New Disk added </li>
<li>List the partitions</li>
<li>Note : vdb has no partitions in it</li>
<pre>
blrk@linux-jbz9:~> lsblk
NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
sr0     11:0    1   4G  0 rom  
vda    253:0    0  16G  0 disk 
├─vda1 253:1    0   2G  0 part [SWAP]
└─vda2 253:2    0  14G  0 part /usr/local
vdb    253:16   0  10G  0 disk 
</pre>

<li>List the device files of disk partition</li>
<pre>
linux-jbz9:~ # ls -l /dev/ | grep vda
brw-rw----  1 root disk    253,   0 Oct 17 10:16 vda
brw-rw----  1 root disk    253,   1 Oct 17 10:16 vda1
brw-rw----  1 root disk    253,   2 Oct 17 10:16 vda2
</pre>

Create a partition using fdisk
--------------------------------
<li>Run the fdisk command</li>
<pre>
linux-jbz9:~ # fdisk /dev/vdb 

Welcome to fdisk (util-linux 2.29.2).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Device does not contain a recognized partition table.
Created a new DOS disklabel with disk identifier 0xa09907cd.

Command (m for help): 
</pre>

<li>Choose the option p for print</li>
<li>Note: Press m for help menu</li>
<pre>
Command (m for help): p
Disk /dev/vdb: 10 GiB, 10737418240 bytes, 20971520 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xab18e436
</pre>

<li>Choose the option n for create new partition</li>
<pre>
Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p): p
Partition number (1-4, default 1): 
First sector (2048-20971519, default 2048): 
Last sector, +sectors or +size{K,M,G,T,P} (2048-20971519, default 20971519): +2G
</pre>

<li>Choose the option p to print the created partition</li>
<pre>
Command (m for help): p
Disk /dev/vdb: 10 GiB, 10737418240 bytes, 20971520 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xab18e436

Device     Boot Start     End Sectors Size Id Type
/dev/vdb1        2048 4196351 4194304   2G 83 Linux
</pre>

<li>Create the second partition</li>
<pre>
Command (m for help): n
Partition type
   p   primary (1 primary, 0 extended, 3 free)
   e   extended (container for logical partitions)
Select (default p): p
Partition number (2-4, default 2): 
First sector (4196352-20971519, default 4196352): 
Last sector, +sectors or +size{K,M,G,T,P} (4196352-20971519, default 20971519): +3G

Created a new partition 2 of type 'Linux' and of size 3 GiB.
</pre>

<li>Choose the option p to print the created partitions</li>
<pre>
Command (m for help): p
Disk /dev/vdb: 10 GiB, 10737418240 bytes, 20971520 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xab18e436

Device     Boot   Start      End Sectors Size Id Type
/dev/vdb1          2048  4196351 4194304   2G 83 Linux
/dev/vdb2       4196352 10487807 6291456   3G 83 Linux
</pre>

<li>Deleting a partition</li>
<pre>
Command (m for help): d
Partition number (1,2, default 2): 2

Partition 2 has been deleted.

Command (m for help): 

Command (m for help): p
Disk /dev/vdb: 10 GiB, 10737418240 bytes, 20971520 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xab18e436

Device     Boot Start     End Sectors Size Id Type
/dev/vdb1        2048 4196351 4194304   2G 83 Linux
</pre>

<li>Create partitions > primary</li>
<pre>
Command (m for help): n
Partition type
   p   primary (2 primary, 0 extended, 2 free)
   e   extended (container for logical partitions)
Select (default p): p
Partition number (3,4, default 3): 
First sector (8390656-20971519, default 8390656): 
Last sector, +sectors or +size{K,M,G,T,P} (8390656-20971519, default 20971519): +1G

Created a new partition 3 of type 'Linux' and of size 1 GiB.

Command (m for help): p
Disk /dev/vdb: 10 GiB, 10737418240 bytes, 20971520 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xab18e436

Device     Boot   Start      End Sectors Size Id Type
/dev/vdb1          2048  4196351 4194304   2G 83 Linux
/dev/vdb2       4196352  8390655 4194304   2G 83 Linux
/dev/vdb3       8390656 10487807 2097152   1G 83 Linux
</pre>

<li>Creating partition > extended</li>
<pre>
Command (m for help): n
Partition type
   p   primary (3 primary, 0 extended, 1 free)
   e   extended (container for logical partitions)
Select (default e): e

Selected partition 4
First sector (10487808-20971519, default 10487808): 
Last sector, +sectors or +size{K,M,G,T,P} (10487808-20971519, default 20971519): 

Created a new partition 4 of type 'Extended' and of size 5 GiB.

Command (m for help): p
Disk /dev/vdb: 10 GiB, 10737418240 bytes, 20971520 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xab18e436

Device     Boot    Start      End  Sectors Size Id Type
/dev/vdb1           2048  4196351  4194304   2G 83 Linux
/dev/vdb2        4196352  8390655  4194304   2G 83 Linux
/dev/vdb3        8390656 10487807  2097152   1G 83 Linux
/dev/vdb4       10487808 20971519 10483712   5G  5 Extended

Command (m for help): 
</pre>

<li>create partition > logical</li>
</pre>
Command (m for help): n
All primary partitions are in use.
Adding logical partition 5
First sector (10489856-20971519, default 10489856): 
Last sector, +sectors or +size{K,M,G,T,P} (10489856-20971519, default 20971519): +2G

Created a new partition 5 of type 'Linux' and of size 2 GiB.

Command (m for help): p
Disk /dev/vdb: 10 GiB, 10737418240 bytes, 20971520 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xab18e436

Device     Boot    Start      End  Sectors Size Id Type
/dev/vdb1           2048  4196351  4194304   2G 83 Linux
/dev/vdb2        4196352  8390655  4194304   2G 83 Linux
/dev/vdb3        8390656 10487807  2097152   1G 83 Linux
/dev/vdb4       10487808 20971519 10483712   5G  5 Extended
/dev/vdb5       10489856 14684159  4194304   2G 83 Linux
</pre>

<li>Save all the new partition </li>
<pre>
Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
</pre>

<li>View the partitons created </li>
<pre>
linux-jbz9:~ # lsblk
NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
sr0     11:0    1   4G  0 rom  
vda    253:0    0  16G  0 disk 
├─vda1 253:1    0   2G  0 part [SWAP]
└─vda2 253:2    0  14G  0 part /
vdb    253:16   0  10G  0 disk 
├─vdb1 253:17   0   2G  0 part 
├─vdb2 253:18   0   2G  0 part 
├─vdb3 253:19   0   1G  0 part 
├─vdb4 253:20   0   1K  0 part 
└─vdb5 253:21   0   2G  0 part 
</pre>

<li>Creating file system > ext4</li>
<pre>
linux-jbz9:~ # mkfs.ext4 /dev/vdb1 
mke2fs 1.43.8 (1-Jan-2018)
/dev/vdb1 contains a ext3 file system
	last mounted on Wed Oct 23 06:36:39 2019
Proceed anyway? (y,N) y
Creating filesystem with 524288 4k blocks and 131072 inodes
Filesystem UUID: 495a699d-51e6-46dd-a59c-e5f8af2d5107
Superblock backups stored on blocks: 
	32768, 98304, 163840, 229376, 294912

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information: done 
</pre>

<li>Creating file system > btrfs </li>
<li>Note : use option -f if any file system already exists in the partition</li>
<pre>
linux-jbz9:~ # mkfs.btrfs -f /dev/vdb2 
btrfs-progs v4.5.3+20160729
See http://btrfs.wiki.kernel.org for more information.

Label:              (null)
UUID:               327ed6df-14f1-40ec-b16a-4a26ab4e8b56
Node size:          16384
Sector size:        4096
Filesystem size:    2.00GiB
Block group profiles:
  Data:             single            8.00MiB
  Metadata:         DUP             110.38MiB
  System:           DUP              12.00MiB
SSD detected:       no
Incompat features:  extref, skinny-metadata
Number of devices:  1
Devices:
   ID        SIZE  PATH
    1     2.00GiB  /dev/vdb2
</pre>

<li>Create mount directory</li>
<pre>
mkdir /database /backup
</pre>

<li>Temporary mount, create a file in the partition then umount </li>
<pre>
linux-jbz9:~ # mount -t ext4 /dev/vdb1  /database/
linux-jbz9:~ # mount -t btrfs /dev/vdb2 /backup/
linux-jbz9:~ # lsblk
NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
sr0     11:0    1   4G  0 rom  
vda    253:0    0  16G  0 disk 
├─vda1 253:1    0   2G  0 part [SWAP]
└─vda2 253:2    0  14G  0 part /
vdb    253:16   0  10G  0 disk 
├─vdb1 253:17   0   2G  0 part /database
├─vdb2 253:18   0   2G  0 part /backup
├─vdb3 253:19   0   1G  0 part 
├─vdb4 253:20   0   1K  0 part 
└─vdb5 253:21   0   2G  0 part 
linux-jbz9:~ # cd /database/
linux-jbz9:/database # ls
lost+found
linux-jbz9:/database # touch file1
linux-jbz9:/database # ls
file1  lost+found
linux-jbz9:/database # cd ../backup/
linux-jbz9:/backup # ls
linux-jbz9:/backup # touch file2
linux-jbz9:/backup # ls
file2
linux-jbz9:/backup # cd ..
linux-jbz9:/ # umount /dev/vdb1
linux-jbz9:/ # umount /backup 
linux-jbz9:/ # lsblk
NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
sr0     11:0    1   4G  0 rom  
vda    253:0    0  16G  0 disk 
├─vda1 253:1    0   2G  0 part [SWAP]
└─vda2 253:2    0  14G  0 part /
vdb    253:16   0  10G  0 disk 
├─vdb1 253:17   0   2G  0 part 
├─vdb2 253:18   0   2G  0 part 
├─vdb3 253:19   0   1G  0 part 
├─vdb4 253:20   0   1K  0 part 
└─vdb5 253:21   0   2G  0 part 
</pre>

<li>Create an entry in the fstab (mount using device name)</li>
<pre>
linux-jbz9:/ # vi /etc/fstab 
#add the following line at the bottom of the fstab file and save it</li>
/dev/vdb1       /backup ext3    defaults        1 2
linux-jbz9:/ # mount -a
linux-jbz9:/ # lsblk
NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
sr0     11:0    1   4G  0 rom  
vda    253:0    0  16G  0 disk 
├─vda1 253:1    0   2G  0 part [SWAP]
└─vda2 253:2    0  14G  0 part /
vdb    253:16   0  10G  0 disk 
├─vdb1 253:17   0   2G  0 part /backup
├─vdb2 253:18   0   2G  0 part 
├─vdb3 253:19   0   1G  0 part 
├─vdb4 253:20   0   1K  0 part 
└─vdb5 253:21   0   2G  0 part 
</pre>

<li>Create an entry in the fstab (mount using UUID)</li>
<li>get the UUID</li>
<pre>
linux-jbz9:/ # blkid /dev/vdb2 
/dev/vdb2: UUID="327ed6df-14f1-40ec-b16a-4a26ab4e8b56" UUID_SUB="b4848399-3d70-4171-930c-cf39e07a6ad8" TYPE="btrfs" PARTUUID="ab18e436-02"
#copy the UUID and use instead of device name
</pre>

<pre>
linux-jbz9:/ # vi /etc/fstab 
#add the following line at the bottom of the fstab file and save it</li>
UUID=327ed6df-14f1-40ec-b16a-4a26ab4e8b56	/database	btrfs	defaults	1 2
linux-jbz9:/ # mount -a
linux-jbz9:/ # lsblk
NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
sr0     11:0    1   4G  0 rom  
vda    253:0    0  16G  0 disk 
├─vda1 253:1    0   2G  0 part [SWAP]
└─vda2 253:2    0  14G  0 part /
vdb    253:16   0  10G  0 disk 
├─vdb1 253:17   0   2G  0 part /backup
├─vdb2 253:18   0   2G  0 part /database
├─vdb3 253:19   0   1G  0 part 
├─vdb4 253:20   0   1K  0 part 
└─vdb5 253:21   0   2G  0 part 

linux-jbz9:/ # ls /database/
file2
linux-jbz9:/ # ls /backup/
file1  lost+found
</pre>
