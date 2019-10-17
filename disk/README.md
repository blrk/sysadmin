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

