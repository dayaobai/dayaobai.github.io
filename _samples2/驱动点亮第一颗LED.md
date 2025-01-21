---
title: "驱动点亮第一颗LED"
collection: samples2
type: "Samples2"
permalink: /samples2/驱动点亮第一颗LED
venue: "UC San Francisco, Department of Testing"
date: 2025-01-21
location: "San Francisco, California"
number: 3
excerpt: "驱动点亮第一颗LED"
---


通过 NFS 将 Ubuntu 中的 rootfs(第三十八章制作好的根文件系统)目录挂载为根文件系统

写好led.c 和ledAPP，将二者拷贝到nfs/rootfs/lib/modules/4.1.15-g3dc0a4b 目录下：

```
sudo cp led.ko ledApp /home/alien/my/nfs/rootfs/lib/modules/4.1.15-g3dc0a4b/ -f
```

**你的开发板和编译led.ko的内核必须都是4.1.15-g3dc0a4b**


拷贝完成后重启开发板，就会在开发板的 /lib/modules/4.1.15-g3dc0a4b 目录下 存在led.ko 和ledAPP 这两个文件
![images](/photos/Pasted image 20241115233617.png)

*上述为4.1.15-g3dc0a4b,截图为之前错误的地方*


在4.1.15-g3dc0a4b目录下执行``depmod`` 命令自动生成modules.dep
![images](/photos/Pasted image 20241115233212.png)

然后输入``modprobe led.ko`` 就可以加载驱动了


驱动加载成功以后创建“/dev/led”设备节点，命令如下：
``mknod /dev/led c 200 0``


最后卸载驱动``rmmod led.ko``


**这里的坑：**
开发板移植的内核镜像zImage版本为**4.1.15-g3dc0a4b**,而编译led.ko的内核版本为**4.1.15**，版本不匹配会出现：
![images](/photos/Pasted image 20241115233232.png)


**解决办法：**
将开发板一致的内核版本改成了v2.4以后的版本，之前是v2.4之前的版本

疑问：
改成v2.4以后的版本后，在4.1.15和4.1.15-g3dc0a4b中都可以加载驱动了



1 iomuxc: iomuxc@020e0000 {
2 compatible = "fsl,imx6ul-iomuxc";
3 reg = <0x020e0000 0x4000>;
4 pinctrl-names = "default";

5 pinctrl-0 = <&pinctrl_hog_1>;
6 imx6ul-evk {
7 pinctrl_hog_1: hoggrp-1 {
8 fsl,pins = <
9 MX6UL_PAD_UART1_RTS_B__GPIO1_IO19 0x17059
10 MX6UL_PAD_GPIO1_IO05__USDHC1_VSELECT 0x17059
11 MX6UL_PAD_GPIO1_IO09__GPIO1_IO09 0x17059
12 MX6UL_PAD_GPIO1_IO00__ANATOP_OTG1_ID 0x13058
13 >;
......
16 };
17 };
18 };