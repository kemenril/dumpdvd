# dumpdvd
Does a single-pass image dump of a video DVD through libdvdcss, with no filesystem manipulation or video transcoding.

This is a simple script in Python 3 that will use **pydvdcss** to pull an image from a video DVD.  It's a one pass process, and nothing in the video or filesystem on the disk is changed.  If it works, the output file will be a (probably decrypted) disk image of the original disk, identical in most every possible way.  A disc containing this image should be playable on any player that can read it.  If you have a software player that will (like VLC) treat a filesystem image as a container type, you will also be able to play it there directly.

I wrote this quickly, because I noticed that I couldn't find a piece of software that allowed you to make a full copy of a disc, menues and all, without extracting the videos and rebuilding the UDF image separately.  Many of them seem to insist on transcoding the video somehow too.  This one doesn't.  It's rather as close as you want to get to a **dd** for DVDs.

## Required modules
Not very many non-standard modules are needed.  You should be able to _pip install_ them.  They are:
   * **pydvdcss**
   * **progress**

## Installation

Just put the script somewhere in your path.  I recommend _/use/local/bin_.  You may want to edit the default DVD device in the top of the script.


## Use

The simple case is:

```
# dumpdvd -o /tmp/dvd.iso
Waiting for medium on /dev/sr0....
Writing to /tmp/dvd.iso
Ripping /dev/sr0 -> /tmp/dvd.iso:
 ◉◉◉◉◉◉◉◉◉◉◉◉◉◉◉◯◯◯◯◯◯◯◯◯◯◯◯◯◯◯◯◯ 533s | 429s remaining
Finished in 8m53s
```

There are a few other things it can do:

If your DVD drive won't allow access without bus authentication, the **-x** flag will attempt to do that, and then exit without ripping any data.  This will allow you to run something like _ddrescue_ on the disk.  

If your rip fails because the disk is dirty, you can clean it and restart it with the **-r** flag.  That will resume near the end, without having to rip the whole data-set again.  

If you specify **-d** instead of **-o** and give an output directory, the program will try to name the file based on the volume label of the DVD.  If you're lucky, this will allow you to rip disks in a bit more bulk, with less intervention.

See the help for a complete list of options.

Note that 100% on the progress bar is roughly at the end of a dual-layer disc, and your disk may not have that much data on it.  We never check to see if it does.
