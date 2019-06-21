---
lang: en
title: How to connect your TASCAM US-600 with MacOS Mojave
description: This also works with any TASCAM US-XXX.
date: '2019-03-06T03:31:17.766Z'
categories:
  - music
keywords:
  - tascam
  - us-600
  - macos
  - mojave
  - high-sierra
---

![](img/0__8wBqYg8hqrwXw5q5.jpg)

This also works with any TASCAM US-XXX.

First of all, download the old drivers [from the official Tascam website](https://tascam.com/us/product/us-600/download).

Now, follow the instructions below, which have been copied and adapted from [the original thread where explains how to make this work](http://www.tascamforums.com/threads/us-200-not-working-with-macos-sierra.4265/).

Since Sierra, MacOS does not seem to load drivers (kexts for Mac OS) that contain both a 32bit and 64bit binary and, at least for the US-600 El Capitan kext, both binaries are present.

See [https://forums.developer.apple.com/thread/50380](https://forums.developer.apple.com/thread/50380).

Luckily, code signing seems to be done on each binary when it is compiled and removing the 32bit version allows the kext to be loaded.

The following steps worked for me but obviously your mileage may vary.

> _**Disclaimer:** I accept no responsibility for what may happen to you, your computer, peripherals or anything else that may occur from following these steps. Use strictly at your own risk! Messing up with kernel extensions could prevent your machine from booting or cause crashes so make sure you have all work saved, a backup and are ready to restore/fix your machine from the recovery partition. If you are not comfortable performing the steps outlined, reverting to El Capitan is a safer option._

In the instructions below you will need to replace all instances of “TASCAM\_US600" with whatever applies to your device.

First, open a terminal. Then, ensure that you can proceed further by checking that you see information about x86\_64 and i386 from the following command:

```sh
file /Library/Extensions/TASCAM_US1641.kext/Contents/MacOS/TASCAM_US200
```

If so, remove the i386 binary with the following:

```sh
# First make a copy to the desktop  
sudo lipo -thin x86\_64 -output ~/Desktop/TASCAM\_US200 /Library/Extensions/TASCAM\_US200.kext/Contents/MacOS/TASCAM\_US200
```

This will have output a file named TASCAM\_US200 to the desktop which should only have the x86\_64 binary.

Remove the orignal:

```sh
sudo rm /Library/Extensions/TASCAM\_US1641.kext/Contents/MacOS/TASCAM\_US200
```

Copy the new binary:

```sh
sudo cp ~/Desktop/TASCAM\_US200 /Library/Extensions/TASCAM\_US200.kext/Contents/MacOS/
```

Try loading the new kext:

```sh
sudo kextload /Library/Extensions/TASCAM\_US200.kext
```

There should be no errors at this point. You can use `kextstat` as an additional check here. Now rebuild the kext cache:

```sh
sudo rm -rf /System/Library/Caches/com.apple.kext.caches  
sudo kextcache -prelinked-kernel /System/Library/Caches/com.apple.kext.caches/Startup/kernelcache -K /System/Library/Kernels/kernel /System/Library/Extensions
```

> As [Renato Borges](https://medium.com/u/85584a6d7eb5) mentioned in the comments, if `sudo rm -rf /System/Library/Caches/com.apple.kext.caches` doesn’t work for you, try with the command`sudo kextcache -e`

Reboot your Mac, check the US-600 audio input is now there. If so, delete that file from your desktop.

Enjoy using your Tascam.
