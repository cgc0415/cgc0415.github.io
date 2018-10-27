---
title: /proc/$PID/maps文件解读
date: 2018-10-27 22:11:00
tags: proc maps
categories: Linux相关
---

Each row in /proc/$PID/maps describes a region of contiguous virtual memory in a process or thread. Each row has the following fields:

```shell
address           perms offset  dev   inode   pathname
08048000-08056000 r-xp 00000000 03:0c 64593   /usr/sbin/gpm
```

> * **address** - This is the starting and ending address of the region in the process's address space
> * **permissions** - This describes how pages in the region can be accessed. There are four different permissions: read, write, execute, and shared. If read/write/execute are disabled, a '-' will appear instead of the 'r'/'w'/'x'. If a region is not shared, it is private, so a 'p' will appear instead of an 's'. If the process attempts to access memory in a way that is not permitted, a segmentation fault is generated. Permissions can be changed using the mprotect system call.
> * **offset** - If the region was mapped from a file (using mmap), this is the offset in the file where the mapping begins. If the memory was not mapped from a file, it's just 0.
> * **device** - If the region was mapped from a file, this is the major and minor device number (in hex) where the file lives.
> * **inode** - If the region was mapped from a file, this is the file number.
> * **pathname** - If the region was mapped from a file, this is the name of the file. This field is blank for anonymous mapped regions. There are also special regions with names like [heap], [stack], or [vdso]. [vdso] stands for virtual dynamic shared object. It's used by system calls to switch to kernel mode.

You might notice a lot of anonymous regions. These are usually created by `mmap` but are not attached to any file. They are used for a lot of miscellaneous things like shared memory or buffers not allocated on the heap. For instance, I think the pthread library uses anonymous mapped regions as stacks for new threads.