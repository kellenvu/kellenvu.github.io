---
title: How to create a 3-2-1 backup plan using Backblaze B2 and restic in 5 simple steps
tags: [Guide]
description: If a natural disaster strikes, is your data safe?
comments: true
---

(Skip to the guide [here](#guide))

{% include elements/figure.html image="https://www.reuters.com/resizer/v2/O43O4YA5AZOCDH6EQJ3PCQ5PUQ.jpg?auth=ed08b900605800050563d9f5df707e69e4515aa000b9a519034ec77bfd269e92&width=1920&quality=80" caption="Source: Reuters" %}

Imagine this: your house burns down. As you stand outside, watching flames consume everything, what’s running through your mind? What do you wish you could have saved?

I asked myself this while watching videos of the January 2025 Southern California fires. It was heartbreaking to see people mourn the loss of everything they owned. But the things they missed most weren’t usually the expensive ones. It was the personal, irreplaceable things: heirlooms, collections, mementos of loved ones.

For me, the biggest loss would be my data. Years of family photos, travel videos, all my writing—gone in an instant. That’s when I decided it was time for a better backup plan.

## The 3-2-1 Rule

Invented by photographer Peter Krogh in his 2005 book *Digital Asset Management for Photographers*, the 3-2-1 backup strategy has become the gold standard for protecting data. It’s simple and practical:

- [ ] **Do I have at least 3 copies of my data?**
- [ ] **Are those copies stored on 2 different devices?**
- [ ] **Is 1 of those copies stored off-site?**

Each box you check reduces the risk of losing your data.

For years, I've been checking off the first two boxes by keeping my data on both my computer and some external drives at home. I always knew I needed an off-site cloud backup, but every time I searched for a guide, I was met with lengthy, technical instructions. The complexity and the apparent cost made me give up before I even started.

That’s why I’m writing this guide—to make creating an affordable 3-2-1 backup plan as approachable as possible.

## Why Backblaze?

The first step in setting up an off-site backup is deciding which cloud storage service to use. There are plenty of options, each varying in features and affordability.

I chose [Backblaze B2](https://www.backblaze.com/cloud-storage), and my decision came down to three simple reasons:

- It was recommended by enough people on Reddit to seem reliable.
- It looked [cheap](https://www.backblaze.com/cloud-storage/pricing). At the time of writing, it costs $6 per month for 1 TB of data. Since the pricing is per GB, you only pay for what you use—if you’re storing 500 GB, you’ll pay half that.
- You get 10 GB free with your account, so it was easy to set up and test without committing.

You’re welcome to explore other options, but for simplicity (and to avoid decision paralysis), this guide will focus on using Backblaze B2.

One clarification, since I was confused at first: Backblaze offers two products. There’s **Backblaze Computer Backup**, a one-click backup solution that automatically backs up everything on your computer. Then there’s **Backblaze B2 Cloud Storage**, which gives you more control over what and when you back up. I wanted the flexibility to back up my external drive whenever I chose, so this guide will focus on Backblaze B2.

## Why Restic?

Once you’ve chosen your cloud storage service, the next step is selecting the backup software to handle the backup process and upload your data to the cloud. There are plenty of options, but I went with [restic](https://restic.net/).

Restic is a command-line program that creates incremental backups. It works by taking self-contained "snapshots" of your data, storing only the changes since the previous snapshot to save time and space. This process, called deduplication, ensures that identical data isn’t stored more than once, which keeps your backups efficient (this is why restic is a better backup solution than programs like rclone).

One thing to recognize: restic stores your backups as snapshots, not as a browsable file system. When you look at your Backblaze B2 filetree, you’ll see encrypted data, not individual files. To access your data, you’ll need to restore a snapshot, either fully or partially.

## Guide

Setting up your cloud backup is as simple as following these 5 steps!

The examples in this guide are written for a Windows computer, but the equivalent commands for other systems should be easy to find (ask ChatGPT).

1. Create a [Backblaze](https://www.backblaze.com/) account, and set up a bucket to store your data. Then create an application key to access the bucket.

    <iframe src="https://www.iorad.com/player/2496063/Set-up-Backblaze?src=iframe&oembed=1" class="my-3" width="100%" height="500px" style="width: 100%; height: 500px; border-bottom: 1px solid #ccc;" referrerpolicy="strict-origin-when-cross-origin" frameborder="0" webkitallowfullscreen="webkitallowfullscreen" mozallowfullscreen="mozallowfullscreen" allowfullscreen="allowfullscreen" allow="camera; microphone; clipboard-write;" sandbox="allow-scripts allow-forms allow-same-origin allow-presentation allow-downloads allow-modals allow-popups allow-popups-to-escape-sandbox allow-top-navigation allow-top-navigation-by-user-activation"></iframe>

1. Install [restic](https://restic.readthedocs.io/en/stable/020_installation.html) on your computer.

1. Open the Windows cmd. Assign your application key ID and your application ID to these environmental variables.

    ```
    set B2_ACCOUNT_ID=<YOUR_APPLICATION_KEY_ID>
    set B2_ACCOUNT_KEY=<YOUR_APPLICATION_KEY>
    ```

1. Initiate your restic repository using the command below.

    ```
    restic -r b2:<BucketName>:<RepositoryName> init
    ```

    The repository name is the name of the directory that will be created at the top level of the bucket. For example...

    ```
    restic -r b2:MyBucket:MyRepository init
    ```

    would create a directory called MyRepository at the top level of MyBucket. You can choose any repository name. This repository will store all the snapshots that you upload.

    It will ask you to create a password for accessing this repository. Remember your password!

1. Whenever you want to create a backup, run the following command.

    ```
    restic -r b2:<BucketName>:<RepositoryName> --verbose backup C:/path/to/local/directory/you/want/to/back/up
    ```

    This will create a snapshot of the target directory (and everything inside), which will be stored inside the given repository.

And that's it! The first backup will take a long time (depending on how much data you're uploading). For example, when I uploaded 563 GB, it took about 48 hours. After that, thanks to deduplication, the following backups should be much faster.

If you exceed your free 10 GB, then Backblaze will send you an email, giving you the option to add a credit card to increase your cap.

In order to restore a backup...

1. Run the following command to see a list of your uploaded snapshots and their IDs.

    ```
    restic -r b2:<BucketName>:<RepositoryName> snapshots
    ```

1. Run the following command to restore a specific snapshot to your computer.

    ```
    restic -r b2:<BucketName>:<RepositoryName> restore <SnapshotID> --target C:/path/to/destination
    ```

Happy backing up!