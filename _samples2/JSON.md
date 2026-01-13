---
title: "JSON"
collection: samples2
type: "Samples2"
permalink: /samples2/JSON
venue: "UC San Francisco, Department of Testing"
date: 2025-01-21
location: "San Francisco, California"
number: 8
excerpt: "JSON"
---

https://blog.51cto.com/u_15294398/3091968
./config --prefix=/home/alien/ztk/linux/openssl --cross-compile-prefix=arm-linux-gnueabihf- no-shared

./config --cross-compile-prefix=arm-linux-gnueabihf- --prefix=/home/alien/ztk/linux/openssl/opensslarm

./config --prefix=/home/alien/ztk/linux/openssl2

export PATH=$PATH:/usr/local/arm/gcc-linaro-4.9.4-2017.01-x86_64_arm-linux-gnueabihf/bin/

./config no-asm shared --prefix=/home/alien/ztk/linux/openssl --cross-compile-prefix=arm-linux-gnueabihf-


ln -s /home/alien/ztk/linux/openssl2/lib/libssl.so.1.1 /lib/x86_64-linux-gnu/libssl.so.1.1

sudo ln -sf /home/alien/ztk/linux/openssl2/lib/libcrypto.so.1.1 /lib/x86_64-linux-gnu/libcrypto.so.1.1

export OPENSSL=/home/alien/ztk/linux/openssl2/bin
export PATH=$OPENSSL:$PATH:$HOME/bin