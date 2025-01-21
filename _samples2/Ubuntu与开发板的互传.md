---
title: "Ubuntu与开发板的互传"
collection: samples2
type: "Samples2"
permalink: /samples2/Ubuntu与开发板的互传
venue: "UC San Francisco, Department of Testing"
date: 2025-01-21
location: "San Francisco, California"
number: 13
excerpt: "Ubuntu与开发板的互传"
---


## 通过NFS实现:

首先设置好开发板和Ubuntu的网络，并通过网线连接

在Ubuntu中建立共享目录   ``/home/alien/my/nfs``

将需要发送到开发板的文件放入上述目录

在开发板中创建一个 get 目录，将虚拟机（192.168.10.100）NFS **共享目录挂载到到开发板**的 get 目录中
``mount -t nfs -o nolock,nfsvers=3 192.168.10.100:/home/alientek/linux/nfs get/``

此时，共享目录下的文件已经挂载到get目录下了

最后，记得卸载NFS目录   ```umount get```

## 通过tftp实现

基础配置弄好后


将所需要传的文件放入ubuntu目录 ``/home/alien/my/tftp``  中


然后再开发板执行命令
```
ifconfig eth0 192.168.10.50   //开发板IP
tftp -g -r test.c 192.168.10.100   //Ubuntu虚拟机IP

//test.c为所需要传输的文件
```



/usr/local/arm/gcc-linaro-4.9.4-2017.01-x86_64_arm-linux-gnueabihf/arm-linux-gnueabihf/libc/lib


/usr/local/arm/gcc-linaro-4.9.4-2017.01-x86_64_arm-linux-gnueabihf/arm-linux-gnueabihf/libc/usr/lib



root=/dev/nfs nfsroot=192.168.10.100:/home/alien/my/nfs/rootfs,proto=tcp rw ip=169.254.211.213:192.168.10.100:192.168.10.1:255.255.255.0::eth0:off


sudo cp led.ko ledApp /home/alien/my/nfs/1/ -f

mount -t nfs -o nolock,nfsvers=3 192.168.10.100:/home/alien/my/nfs 4.1.15-g3dc0a4b/

mount -t nfs -o nolock,nfsvers=3 192.168.10.100:/home/alien/my/nfs get/