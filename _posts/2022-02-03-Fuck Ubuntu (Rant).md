---
title: Fuck Windows ..and Ubuntu (Rant)
date: 2022-02-03 16:13:00 -0700
modified: 
permalink: /fuck-windows-and-ubuntu/
category: Uncategorized
tags: [operating systems, rant]
---

## My OS History
I started with Windows 95, and it was *okay*. Upgrading to Windows 98 helped a lot and I still love that OS. My next experience was with Windows XP, and it was good. When Windows Vista first came out, I tried it and had several problems with it. (No, I don't remember what they were.)

Somewhere around this time I was introduced to Linux and tried a few distributions. (My favorites were [Ubuntu](https://en.wikipedia.org/wiki/Ubuntu), [slax](https://en.wikipedia.org/wiki/Slax), & [Antergos](https://en.wikipedia.org/wiki/Antergos). Later, my absolute favorite would be [CrunchBang](https://en.wikipedia.org/wiki/CrunchBang_Linux). I still miss all of these, *including old versions of Ubuntu*.)

After Windows 7 came out, my experience with Windows started to go downhill. Nonsensical errors (why does an administrator not have full disk access?), rebooting my computer without consent (no matter how many times I disabled this "feature"), running slowly despite good hardware.. the list is long. This is when I first thought about using Linux for things besides programming.

I again skipped Windows versions until Windows 10, mainly due to free upgrades being offered and hating the UI changes in Windows 8 that were partially walked back. At this point, my hatred started. Default applications I can't uninstall or even hide, advertisements built-in, a virtual assistant I could not disable or remove always running in the background.. and they even removed the pretense of controlling updates.

Oh, and the default malware included to spy on your usage, again, without consent.

But the problem is that I was running a mildly successful gaming YouTube channel at the time, I *needed* Windows because no video editor on Linux was good enough, and games only work on Windows.

Then Steam announced <span title="Which, to be clear, is just a modified and improved version of WINE - a free open source tool to run Windows software on Linux.">Proton</span>, and reviews were good. Over time, Linux seemingly became viable. There was even a hot new video editor called daVinci Resolve, and it runs on Windows, macOS, and Linux!

## What Happened to Ubuntu?
I ran various versions of Ubuntu as a secondary OS or on a USB drive from 8 to 18 without problems. Common problems like networking, video card support, and audio issues were never difficult - and often did not even occur. Ubuntu was a good choice because its popularity made it more often supported, and it was usually stable.

Not this time. I spent *weeks* trying to get it working, and while I was eventually successful, it was only through stubbornness and a lot of reading.

I started with a new SSD, as my old one only had 128 GB of space, and I was going to need a lot more for video editing and running games that require better disk streaming. First, the install failed because a disk I *wasn't even using* is corrupted. Then, it failed to install the bootloader. Then it failed because of a partially completed Ubuntu install. I moved on to trying elementary OS (a derivative of Ubuntu) because it has several improvements and is still widely supported, but this also failed.

Turns out, since version *14.04*, there's a bug where Ubuntu won't install a bootloader if you select any disk besides the first. There is *no warning of this anywhere*, and I had to find a bug report from half a decade ago to even learn this. So, I removed all disks except my new SSD, and moved it to first SATA port on the motherboard, and Ubuntu .. still didn't install.

Time to try again, except I accidentally booted into Ubuntu from the SSD.. you know, the OS that ***failed to install***? So, it turns out that not only does it fail to install a bootloader under most possible conditions, *but a success crashes the installer*. Oh well, at least I now have a working system, time to update!

### Ubuntu Prominently Publishes Broken Versions
I run updates, and find out there's a new OS version. I'd started with version 20.10 because it was what was out when I started this, and version 21.04 had released since then. I run the upgrade.. and now I can't boot anymore. *This has never happened to me before*, and this is a brand new system.

Turns out, version 21.04 shipped with a bug that breaks the bootloader on *any* system, whether it be a fresh install or through an upgrade. Here's the fucking problem: They only disabled update notifications, instead of pulling the faulty update or OFFERING ANY WARNING WHATSOEVER.

There is no reason I couldn't have been notified not to update. There is no reason to keep a broken release public. There is no reason for *any* of this to have happened the way it did.

This is unacceptable, and even since fixing the problem on my system, Ubuntu has just been a completely different system than what it was. They added ads/spyware to the base OS and pushed updates that break configuration & uninstall apps. It's just not good anymore, and it makes me sad.