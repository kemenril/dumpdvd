# dumpdvd
Does a single-pass image dump of a video DVD through libdvdcss, with no filesystem manipulation or video transcoding.

This is a simple script in Python 3 that will use **pydvdcss** to pull an image from a video DVD.  It's a one pass prices, and nothing in the video or filesystem in the disk is changed in the process.  If it works, the output for will be a (probably decrypted) disk image of the original disk, identical in most every possible way.

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
# dumpdvd /tmp/dvd.iso
Ripping /dev/sr0 -> /tmp/dvd.iso:
 ◉◉◉◉◉◉◉◉◉◉◉◉◉◉◉◯◯◯◯◯◯◯◯◯◯◯◯◯◯◯◯◯ 533s | 429s remaining


Finished in 8m53s

```

Note that 100% on the progress bar is roughly at the end of a dual-layer disc, and your disk may not have that much data on it.  We never check to see if it does.
