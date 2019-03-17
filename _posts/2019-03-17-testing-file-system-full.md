---
layout: post
title:  "Testing out of space errors"
date:   2019-03-17
categories: testing mmap linux unix sparsefile
---

Many times, you want to see how your program reacts when writes to a
file start failing due to out of space error. There is a handy way to
test this error condition. All the commands shown in this article were
run on a *CentOS* box but they should work in a similar fashion on any
Linux machine.

- First create a sparse file that acts as backing storage for the test
  file system.

```
$ truncate -s 128M /tmp/testfile
```

- Create a loop back device.

```
$ losetup /dev/loop0 /tmp/testfile
```

- Create a file system and mount it.

```
$ mkfs.ext4 /dev/loop0
$ mount /dev/loop0 /mnt

$ df -hl /mnt
Filesystem      Size  Used Avail Use% Mounted on
/dev/loop0      120M  1.6M  110M   2% /mnt
```

Now you have a file system that has less than 128 MiB space and it
should be easy to fill it up so that writes would start failing. For
example, I recently wanted to test the behavior of memory mapped files
when writes to the backing file fail. It is especially important to
test this case as behavior of *mmap* in several corner cases is
not well documented.

Just as a quick primer,
[*mmap*](http://man7.org/linux/man-pages/man2/mmap.2.html)
 system call allows a region of file
to be mapped to memory so that file data can be accessed as if
it is in memory. Kernel takes care of reading in required data
from file and of flushing the changes back to the file. This type of
access is supposed to be more efficient as it avoids copying data to
user space and also avoids the overhead of system calls. But the
results of improper usage of *mmap* can be severe. 

For example, if you create a 0-length file and then map the first 1
MiB of the file, *mmap* will succeed but the moment any data is
accessed (read or write), the program will get *SIGBUS*, effectively
terminating it. On the other hand, if we create a sparse file of some
size (say, by seeking to an offset and writing a byte) and map entire
file into memory, we should be able to write to any portion of the
file. But what happens if the underlying file system runs out of space
so that kernel can't flush data to the sparse file? 

I wanted to verify this particular behavior so I created a small file
system using the steps outlined above. I then created a sparse file
whose size is larger than the size of the available file system. Note
that it doesn't actually occupy any disk space so we will be able to
create such large sparse file though the underlying file system
doesn't have enough free space. 

Here, I am creating a sparse file of size 1 GiB in the mounted file
system.

```
$ truncate -s 1G /mnt/mmaptestfile
```

Once the file is in place, the following Python script (`mmaptest.py`)
will map entire file into memory and then start writing 1 MiB
data chunks. Since the file system only has about 120 MiB free space but the
memory mapped file is 1 GiB in size, writing data to the memory should
fail at some point.

```
#!/usr/bin/env python3

import mmap

with open("/mnt/mmaptestfile", "r+b") as f:
    mm = mmap.mmap(f.fileno(), 0)
    offset = 0
    mb = 1024*1024
    for i in range(200):
        print(i)
        mm[offset:offset+mb] = b"0" * mb
        offset += mb

    mm.close()
```

Here is a sample run:

```
$ ./mmaptest.py
0
1
2
3
...
...
114
115
Bus error
```

It can be clearly seen that write after the first 115 MiB resulted in
program receiving SIGBUS.

## Conclusion

So with few commands and a small Python script, I could verify how a
system call (*mmap* in this case) behaves in a particular situation,
one that is not very often encountered. This also shows how commands on 
*Linux* (on any *Unix* really) can be combined dynamically to perform a
complicated test.

Incidentally, one of the easiest and best ways to prevent out of space
errors in by preallocating the space (using 
[*fallocate*](http://man7.org/linux/man-pages/man2/fallocate.2.html)
system call). Preallocation may not be feasible in all cases and 
[*fallocate*](http://man7.org/linux/man-pages/man2/fallocate.2.html) may
not work on some file systems (*ZFS* for example), but it offers a
simple solution in many cases.




