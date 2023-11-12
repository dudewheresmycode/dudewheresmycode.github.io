---
layout: post
title:  "Migrating my Plex library with ssh, screen, and rsync"
date:   2023-01-14 12:00:00 -0600
categories: Plex media guide

---



I've been running my Plex server on a Mac mini with some external USB hard drives for years now. It's become a tangled mess of precariously plugged in USB cords and AC adapters. I also had zero redundancy or backup :sweat_smile:. I decided it was finally time for a major upgrade and overhaul. So I purchased 4 new [10TB WD drives](https://www.amazon.com/dp/B08TZPS4QQ), and embarked upon building a NAS running [Unraid](https://unraid.net/) with an old PowerEdge R520 with 8 hot-saw bays, which I got from my buddy Dean last year. If you're interested in the full story of ordering and installing the drives, add [New Years and a Bonus Christmas]({% post_url 2023-01-12-newyears-bonus-christmas %}) to your reading list.

Now the problem of moving my existing 13TB of media to the new 30TB array. My Plex server will remain on the Mac mini, but the files need to get moved from the external USB drives to the new NAS share on the network. The standard file transfer Mac OS could work, but offers no real features or guarantee. I just don't trust it to do the job. Enter [`rsync`](https://ss64.com/osx/rsync.html), a copy util meant for syncing folders. It has a slew of useful features, and should easily be able to handle recursive copy from folder to folder. 

The basic syntax is:

```bash
rsync [options] [source] [destination]
```

This command will copy all the contents of one folder over to the destination.

```bash
rsync -av --progress --exclude=".*" '/Volumes/Media/TV Shows/' '/Volumes/unraid/Transfers'
```

Let's break down the options above:

- `-av` 
  - The `a` is for Archive Mode. From the rsync docs, this is the recommended way to copy folders.
  - The `v` is for verbose, which means we'll get all the messages for any warnings or errors.
- `--progress` - Will output progress information about each transfer. Including percent complete and copy speed (MB/s).
- `--exclude=".*"` - Excludes hidden files. Since we only care about copying the media files, we don't want to move any of the  hidden files some systems create like `.DS_Store` on Mac.

The trailing slash. Notice in the above example, the source directory has a trailling `/`. This is an important bit, as it tells rsync to only copy the contents of the folder "TV Shows". Sort of like saying `/Volumes/Media/TV Shows/*`. If we were to omit that trailing slash, it would copy the folder TV Shows itself, to the destination.

Currently my Plex server is headless, so I generally SSH in, or use the Remote Desktop for some things. The problem with running rsync copy jobs over SSH, is dropped connections and broken pipes. The solution to that 
