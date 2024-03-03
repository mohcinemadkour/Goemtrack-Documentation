
title: Linux 
created at: Sun Feb 07 2021 03:30:00 GMT+0000 (Coordinated Universal Time)
updated at: Mon Aug 14 2023 13:23:45 GMT+0000 (Coordinated Universal Time)
---

# Linux

The accepted answer lists only the filenames, but to get the top 5 files one can also use:

`ls -lht | head -6`

where:

`-l` outputs in a list format

`-h` makes output human readable (i.e. file sizes appear in kb, mb, etc.)

`-t` sorts output by placing most recently modified file first

`head -6` will show 5 files because `ls` prints the block size in the first line of output.

I think this is a slightly more elegant and possibly more useful approach.

          