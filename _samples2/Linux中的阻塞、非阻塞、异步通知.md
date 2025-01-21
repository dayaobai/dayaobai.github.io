---
title: "Linux中的阻塞、非阻塞、异步通知"
collection: samples2
type: "Samples2"
permalink: /samples2/Linux中的阻塞、非阻塞、异步通知
venue: "UC San Francisco, Department of Testing"
date: 2025-01-21
location: "San Francisco, California"
number: 10
excerpt: "Linux中的阻塞、非阻塞、异步通知"
---


**阻塞**：当应用程序发起 I/O 操作时，进程会被阻塞（暂停执行）

**非阻塞**：如果数据不可用，不会阻塞线程，而是立即返回。应用程序需要通过轮询、事件通知或异步机制重新尝试操作

**异步通知**：驱动程序主动向应用程序发出通知，报告自己可以访问，然后应用程序在从驱动程序中读取或写入数据，类似于中断。