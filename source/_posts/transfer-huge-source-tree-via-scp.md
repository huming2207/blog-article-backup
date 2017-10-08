---
title: Transfer huge amount of source files via network (SCP + GZip)
date: 2017-10-08 17:45:10
tags: 
 - linux
 - scp
 - ssh
 - english-note
 - quick-note
---

# Scenario

I've got a modified AOSP (Mokee, ~50GB with repo cache) need to be transferred from my Mac to my Thinkpad. But macOS does not support linux file systems while Linux does not support apple file systems too.

# Solution

After a quick Google, I've found a way to solve this issue by using WiFi to transfer. 

Simply transfer the file with SCP/FTP is not fast enough. Here we use Tar to compress the data, then put it to SCP's pipe, and decompress the data on the target machine.

The command is:

```
tar zcvf - mokee | ssh hu@the-damn-thinkpad "cd /home/hu/target/mokee/directory; tar zx"
```

# Efficiency

Looks good, 25~35MB/s with 802.11ac (867Mbps, 2x2 MIMO) connection.

![](/media/15074458869506.jpg)


