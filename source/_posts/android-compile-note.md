---
title: Android kernel compilation on macOS
date: 2017-10-13 09:47:36
tags: 
    - note
    - english-note
    - linux
    - linux-kernel
    - quick-note
---

# Intro

I'm trying to port some linux kernel optimisation patches from OnePlus 5 to my Xiaomi Mi 6. Here are some quick notes for some issues and errors I've encountered.

Btw here is the kernel repo: [https://github.com/huming2207/sagit-daily-kernel](https://github.com/huming2207/sagit-daily-kernel)

For someone who cares about this kernel, please use with precaution, I'm not sure if it works or not.

# Issue 1

## Issue

```bash
build/core/config.mk:608: *** Error: could not find jdk tools.jar 
at /System/Library/Frameworks/JavaVM.framework/Versions/Current/Commands/../lib/tools.jar, 
please check if your JDK was installed correctly.  Stop.
```
Android buildroot script (makefiles) need two Java home path variables to make it works. The variables are `JAVA_HOME` and `ANDROID_JAVA_HOME`.

## Solution:

Add two lines to `~/.zshrc` or `~/.bashrc`:

```bash
export JAVA_HOME=$(/usr/libexec/java_home -v 1.8)
export ANDROID_JAVA_HOME=$(/usr/libexec/java_home -v 1.8)
```

# Issue 2

## Issue

I terminated the iTerm session by mistake, so I didn't get the full error log. But it should be something like this:

```
...
Could not find a supported mac sdk
...
```

## Solution

Download macOS SDK package from here: [https://github.com/phracker/MacOSX-SDKs/releases](https://github.com/phracker/MacOSX-SDKs/releases)

Then unzip to `/Developer/SDKs`

