---
title: "将文件下载到SD中"
collection: samples2
type: "Samples2"
permalink: /samples2/将文件下载到SD中
venue: "UC San Francisco, Department of Testing"
date: 2025-01-21
location: "San Francisco, California"
number: 2
excerpt: "将文件下载到SD中"
---

将imxdownload拷贝到工程文件目录下

![images](/photos/Pasted image 20241114231748.png)

给予 imxdownload 可执行权限
```
chmod 777 imxdownload
```

确定要烧写的 SD 卡
```
ls /dev/sd*
```

向 SD 卡烧写 bin 文件
```
./imxdownload <.bin file> <SD Card>
```

例如：``./imxdownload led.bin /dev/sdd ``





烧写uboot进SD卡

```
./imxdownload uboot.bin /dev/sdb
```