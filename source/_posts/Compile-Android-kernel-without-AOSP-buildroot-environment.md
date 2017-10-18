---
title: Compile Android kernel without AOSP buildroot environment
date: 2017-10-18 23:38:06
tags:
    - linux-kernel
    - linux
    - android
    - android-development
    - english
    - english-note
    - quick-note
---

## Intro

Recently I've started a kernel porting project for Xiaomi Mi 6, porting optimisation patches from open source community (e.g. XDA-Developer’s OnePlus 5 forum). Here is a quick note for environment setup and compiling the kernel only without AOSP buildroot.

## Preparation

1. Install dependencies: `sudo apt install kernel-package git-core `

2. Download the source: `git clone https://github.com/huming2207/Popkern-sagit.git`
3. Toolchain setup: you can either try using Android perbuilt toolchains (may not work on my kernel project due to compiler argument in CFLAG is not supported), or build by your own with crosstool-ng

## Compilation

- Set environment variables:

```bash
export CROSS_COMPILE=aarch64-your-toolchain-name-
export ARCH=arm64
```

- Load configuration file

```
make defconfig sagit_user_defconfig
```

- Build the kernel

```
make -j8
```



## Creating flashable package

- Create a DTB-bundled kernel image. Since Xiaomi's kernel building script somehow messed up, the `Image.gz-dtb` is the same as `Image.gz`. So we have to do the merge by our own:

```bash
cat arch/arm64/boot/Image.gz arch/arm64/boot/dts/qcom/*.dtb > zImage
```
- Download my package from here, then unzip it: 
[https://github.com/huming2207/Popkern-sagit/releases](https://github.com/huming2207/Popkern-sagit/releases)
- Replace the `zImage` file which just generated, re-pack it.

- Flash to the device and it should works.




