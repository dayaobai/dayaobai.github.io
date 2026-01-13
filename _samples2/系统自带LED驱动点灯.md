---
title: "系统自带LED驱动点灯"
collection: samples2
type: "Samples2"
permalink: /samples2/系统自带LED驱动点灯
venue: "UC San Francisco, Department of Testing"
date: 2025-01-21
location: "San Francisco, California"
number: 5
excerpt: "系统自带LED驱动点灯"
---


简单的LED、BEEP驱动Linux以及为我们写好了，直接调用就行



这是系统封装好的驱动函数,位置在``/drivers/leds/leds-gpio.c``

```
static const struct of_device_id of_gpio_leds_match[] = {
	{.compatible = "gpio-leds", },
	{},
};
......
static struct platform_driver gpio_led_driver = {
	.probe = gpio_led_probe,
	.remove = gpio_led_remove,
	.driver = {
		.name = "leds-gpio",
		.of_match_table = of_gpio_leds_match,
	},
};

module_platform_driver(gpio_led_driver);
```

**注意：**.compatible = "gpio-leds"，所以在设备树中也要是 gpio-leds



系统以及封装好了LED驱动函数，所以我们只需要加入设备节点即可

```
dtsleds {
	compatible = "gpio-leds";
	
	led0 {
	label = "red";
	gpios = <&gpio1 3 GPIO_ACTIVE_LOW>;
	default-state = "off";
	};
};
```


重新编译设备树，启动开发板
会在``/sys/bus/platform/devices/``目录下存在dtsleds目录
![images](/photos/Pastedimage-2420241204.png)
进入dtsleds/leds可以看到
![images](/photos/Pastedimage-2420241204-1.png)
里面有定义的设备树下定义的label：red