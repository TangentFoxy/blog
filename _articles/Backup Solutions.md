---
title: Backup Solutions
date: 2019-05-11 13:26:00 -0800
modified: 
permalink: /backup-solutions/
category: Administration
blags: [backups, data storage, encryption, software analysis]
tags: writing/blog/published
---

The following is current as of May 2019:

I've spent a few days researching software and services for backing up data. My requirements: encrypted backups, deduplication, low cost, compatible with Windows 10 & Linux, and preferably using off-site storage.

## Software

I have only considered two competitors: [tarsnap](https://tarsnap.com/) and [restic](https://restic.net/). Tarsnap can create keys with different permissions – a server can run backups with no danger of a compromise leading to the destruction of backups, but it is only compatible with tarsnap.com for data storage.

Restic allows you to plug it into any system for storage. I prefer tarsnap's extra layer of paranoia, but the service costs are where the battle ends for me.

**Update**: These tools both deduplicate at a block size rather than by file, and both utilize a cache for speeding up backups. Both chunk at a dynamic level, with data blobs/chunks/blocks usually being around 1MB. Tarsnap's cache is local, but can be restored by scanning the backup server (at a network usage cost of approximately 0.1% the size of the data stored), while restic uses both a local cache and a cache on the destination. Restic also creates checkpoints while uploading backups to reduce duplication caused by interrupted uploads.

## Services

- [Tarsnap](https://www.tarsnap.com/): $0.25/GB/month (transfer: $0.25/GB)
- [Rsync.net](https://www.rsync.net/): $0.04/GB/month (min: 200 GB)
- [Amazon S3](https://aws.amazon.com/s3/): f\*\*\*ing complicated pricing
- [Wasabi](https://wasabi.com/): $0.0059/GB/month (no other charges)
- [Backblaze B2](https://www.backblaze.com/b2/): $0.005/GB/month (download: $0.01/GB)
- Local: Hardware costs + electricity.

Obviously, price is not everything. Rsync.net offers daily snapshots, cheaper per-GB pricing with mass amounts of data storage needed, and additional features. Amazon S3 and Wasabi are designed for application services rather than storage. Backblaze's B2 is probably the only cloud service (of those I examined) designed for this usage.

Ultimately, cost is my limiting factor. My backups are using restic and local hardware for now, but I plan to move to using Backblaze B2 as I can afford to.

## Updates

Since publication, a few have reached out to me recommending alternative services or sharing their choices. I have not compared these as thoroughly as I did my shortlist, but I feel they deserve their own note for anyone pursuing this decision themselves:

- [SpiderOak One Backup](https://spideroak.com/one/): Starts at $0.04/GB for their 150GB plan, goes down to $0.0058/GB with a 5TB plan. I'd probably choose it if I had a bit more money to spend.
- [CrashPlan for Small Business](https://www.crashplan.com/): $10/computer, "unlimited" storage. Haven't looked at the caveats included.
