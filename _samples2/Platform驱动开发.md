---
title: "Platform驱动开发"
collection: samples2
type: "Samples2"
permalink: /samples2/Platform驱动开发
venue: "UC San Francisco, Department of Testing"
date: 2025-01-21
location: "San Francisco, California"
number: 11
excerpt: "Platform驱动开发"
---


platform 只是为了驱动的分离与分层而提出来的一种框架，其驱动的具体实现还是需要字符设备驱动、块设备驱动或网络设备驱动。


Platform 驱动主要围绕两个核心结构展开：

- **Platform Device**：表示平台上的一个硬件设备。
- **Platform Driver**：用于驱动与某个 Platform Device 对应的硬件。

Platform 驱动通过匹配 `platform_device` 和 `platform_driver` 来完成驱动加载。这种匹配通常依赖设备的名字或者设备树节点的 compatible 属性。



## 1. Platform Device 定义

可以通过静态定义（旧）及设备树定义

**设备树**定义：
```
my_device: my_device@10000000 {
    compatible = "atkalpha-gpioled";
    reg = <0x10000000 0x100>;
    interrupts = <30>;
};
```
重点是要设置好 compatible属性的值，因为 platform 总线需要通过设备节点的 compatible 属性值来匹配驱动

在Platform Driver中 of_match_table 属性表中也要有“atkalpha-gpioled，二者要匹配


## 2. **Platform Driver 定义**

Platform Driver 是具体的驱动程序，实现硬件设备的初始化、操作和卸载。


platform框架：
```c
/* 设备结构体 */
struct xxx_dev{
	struct cdev cdev;
	/* 设备结构体其他具体内容 */
};

struct xxx_dev xxxdev; /* 定义个设备结构体变量 */

static int xxx_open(struct inode *inode, struct file *filp)
{
	/* 函数具体内容 */
	return 0;
}

static ssize_t xxx_write(struct file *filp, const char __user *buf, size_t cnt, loff_t *offt)
{
	/* 函数具体内容 */
	return 0;
}

/* 字符设备驱动操作集 */
static struct file_operations xxx_fops = {
	.owner = THIS_MODULE,
	.open = xxx_open,
	.write = xxx_write,
};




//当驱动和设备匹配成功以后此函数就会执行
static int XXX_probe(struct platform_device *dev)
{
	//以前在驱动入口 init 函数里面编写的字符设备驱动程序就全部放到此 probe 函数里面。比如注册字符设备驱动、添加 cdev、创建类等等
};



static int led_remove(struct platform_device *dev)
{
	//以前在驱动卸载 exit 函数里面要做的事情就放到此函数中来
};


/* 匹配列表 */
//如果使用设备树的话将通过此匹配表进行驱动和设备的匹配
//此匹配项的 compatible 值为“xxx-gpio”，因此当设备树中设备节点的compatible 属性值为“xxx-gpio”的时候此设备就会与此驱动匹配。
static const struct of_device_id xxx_of_match[] = {
	{ .compatible = "xxx-gpio" },
	{ /* Sentinel */ } 
	//注意最后一行是一个空元素，编写该函数时最后一个元素一定要为空！
};

MODULE_DEVICE_TABLE(of, xxx_of_match);



/* platform驱动结构体 */
static struct platform_driver led_driver = {
    .driver     = {
        .name   = "imx6ul-led",   /* 驱动名字，用于和设备匹配 */
    },
    .probe      = led_probe,
    .remove     = led_remove,
};


/* 驱动模块加载 */
static int __init xxxdriver_init(void)
{
	//驱动入口函数里面调用该函数向 Linux 内核注册一个 platform 驱动
    return platform_driver_register(&led_driver);
}



/* 驱动模块卸载 */
static void __exit xxxdriver_exit(void)
{
	platform_driver_unregister(&xxx_driver);
}


module_init(xxxdriver_init);
module_exit(xxxdriver_exit);
MODULE_LICENSE("GPL");
MODULE_AUTHOR("zhaodaer");


```