# Inodes-in-Linux

Whenever you run the `ls` command, we get lot of information such as files listed, permissions, ownership etc… In linux all these data about the files are stored separately from the files. Inodes or index nodes are the one’s that is storing the metadata about a file in linux.

## What all metadata are stored in inodes ?

Let’s refer inode man page to have a look at what all metadata are stored in inode.

https://man7.org/linux/man-pages/man7/inode.7.html

They are the following -

```
- Device where inode resides,
- Inode number, 
- File type, 
- Permissions, 
- File size, 
- UID, 
- GID, 
- Last Access time, 
- modify time, 
- change time, 
- Number of links, 
- Number of blocks, 
- Pointers to the data blocks.
```

## Where is filename?

Inodes don’t store file name. Dentry is the one that has filename stored. It holds inodes and files together by relating inode numbers to file names.

## How to get Inode Information in Linux?

1. Get inode number
```
$ ls -i
393292 test.txt
```

2. Get Inode Usage

```
$ df -i
Filesystem     Inodes IUsed  IFree IUse% Mounted on
udev           502781   300 502481    1% /dev
tmpfs          505101   397 504704    1% /run
/dev/sda1      647168 67568 579600   11% /
tmpfs          505101     1 505100    1% /dev/shm
tmpfs          505101     3 505098    1% /run/lock
tmpfs          505101    17 505084    1% /sys/fs/cgroup
/dev/sda15          0     0      0     - /boot/efi
tmpfs          505101    10 505091    1% /run/user/1001
```

Each filesystem mounted to your computer has its own inodes. An inode number may be used more than once but never by the same filesystem.

If we create lot of empty files, inode used will get filled up. So even if there is enough space in the disk, we won’t be able to create a file as inode has been completely consumed.

3. Get information of a file

```
$ stat test.txt
  File: test.txt
  Size: 0          Blocks: 0          IO Block: 4096   regular empty file
Device: 801h/2049d Inode: 393292      Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1001/   sajan)   Gid: ( 1002/   sajan)
Access: 2022-07-12 06:49:08.204997427 +0000
Modify: 2022-07-12 06:49:08.204997427 +0000
Change: 2022-07-12 06:49:08.204997427 +0000
 Birth: -
 ```
 
This includes — size, block, number of links, device, access time, modify time and change time of a file.

## Conclusion

Inode is an important part in linux file system which has all data to read a file in linux. So it is very important to understand its concept.

Hope this article helped you in understanding inode concept in linux ! Happy reading!
