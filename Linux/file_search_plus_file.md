---
title: File search (and more) with `find`
published: true
description: How to use the find command for Linux and Mac OSX Systems    
tags: Linux, terminal, find, commandline
---

Being able to use the command line is a productivity booster, all system operations that can be done with a mouse and keyboard on fancy GUI applications are doable ove CLI.



The find command is impressive by its versatility, for example, you can lookup for a file that you "lost" on your hard-drive.

`find / -name mylostfile`

by steps, the first argument to the file program is the initial path for search (recursevely, "/" for root):

the `-name` parameter specifies the file name that you are looking for.

**BONUS:** you can use wildcards in the `-name` parameters

`find / -name "*.jpg"`

This basic functionality, find already is worth a ton, but just looking for a file is just the tip of this Titanic killer iceberg.

**The exec parameter**

Here is where `find` shines, you can execute any command on the list of the files that you found, just replace the file name with {}

`find . -name "*.mp4" -exec ffmpeg -i {} -r 30 {.}.avi \;`


again step by step:

`-name "*.mp4"` search for any file with the mp4 extension

`-exec ffmpeg -i {} -r 30 {.}.avi \;` call ffpmeg to perform a operation, keeping a 30fps on a video file and converting it to avi.

`{}` current file.

`{.}` current file without extension.

*PS:*: the semi-colon in the end of the command is uterly important, you can find more details at: [`file` man file](https://linux.die.net/man/1/find)

ffmpeg details: [ffmpeg](https://ffmpeg.org/ffmpeg.html)

---

**Do you like using the terminal? Share your experiences with `find` in the comments and we can learn togheter!**


