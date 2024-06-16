# Everything is a File

## Story

After getting a nervous breakdown due to the stress being a system administrator you went into exile to a monastery on top of a mountain in Silicon Valley.

A few things happened.

First, since Silicon Valley is rather flat, the mountain top wasn't an actual *mountain top* per se, but a classroom seminar about system administrator at the 22th floor of a skycraper ... well that was a bummer.

Second, the chief zed buddhist monk turned out to be a DevOps guru who said only one thing and one thing only, repeating that everyday ... *remember novice, in Unix everything is a file*.

You asked *even disks, printers and all that master?*, to which he replied *yes, even nothingness* and went silence for the rest of your stay (mostly due to sleep deprivation due to a failed production rollout as you have later found out).

Let's find out what he meant!

## What are you going to learn?

- About the philosophy of Unix: everything is a file, devices, text files, network sockets, etc.
- What a filename is and which part of it is the file extension
- Different file types: regular file, directory, hard and symbolic link
- Creating a symbolic or soft link
- Creating a hard link
- The difference between soft and hard links, and their limitations
- Handle files with filenames containing spaces
- Edit file contents
- Understand the hidden file/directory concept
- Understand what command "flags" are and what's their purpose
- The difference between file type and structure
- What "file structure" means
- How to check the actual path of an executable/command with `which`
- Use `wget` to download files via URLs

## Tasks

1. Create or use an existing, an `ext4` formatted virtual disk (`.vdi`), attach it to your VM and mount it.
    - A 4 MB large, fixed-size virtual disk is created in `.vdi` format
    - The disk is named in `<Lastname><Firstname>.vdi` format, e.g. if your name is John Smith then your disk should be named as `SmithJohn.vdi`
    - The disk is `ext4` formatted and has a single volume
    - The disk is attached to your VMs SATA storage controller
    - The volume is mounted at `/home/ubuntu/disk` and owned by `ubuntu:ubuntu`

2. Mimic the required directory structure exactly on your own virtual disk.
    - The following directory structure/hierarchy is created inside your disk's mount-point.
Directory names must be specified as listed here, containing spaces, letter casing must match, etc.

```
/home
└── ubuntu
    └── disk
        └── Directories
            ├── Hard Links
            ├── Other Files
            ├── Regular Files
            └── Symbolic Links
```

3. Create various types of files on the mounted volume.
    - `/home/ubuntu/disk/Directories/Regular Files/my path.txt` exists and its contents are two lines
(1) The first is the path of the file itself relative to `$HOME/disk`
(2) The second its absolute path in the filesystem
    - A directory named `.Hidden` is created under `/home/ubuntu/disk/Directories` that isn't listed by a simple `ls` command
    - A hidden text file named `.secret.txt` is created under `/home/ubuntu/disk/Directories/Regular Files` that isn't listed by a simple `ls` command, its content should be `Password1`
    - Symlinks are created under `Symbolic Links` for every other (regular) directory present on the attached disk; each symlink's name is suffixed with `.dir.lnk`
    - All files (not directories) in the `Regular Files` directory (hidden or not) are hard-linked into the `Hard Links` directory; each hard-link is suffixed with `.bak` (for backup)
    - Copies of the following executables/commands are saved to the `Regular Files` directory: `echo`, `cat`, `wget`
    - Create a file called `nothing` in `Regular Files` whose content is the absolute path of the `null` device

4. Create a CSV file to serve a simple database for your favorite quotations.
Find famous English language quotations off of the Internet from different authors.
    - A CSV file is created at `/home/ubuntu/disk/Directories/Regular Files/quotations.csv`
    - The file is structured into 2 columns (Author, Quotation) and 5 rows (6 in total including the header row), values are separated with semicolons (`;`) as follows:

```
Author;Quotation
John C. Maxwell;The greatest mistake we make is living in constant fear that we will make one.
Isaac Asimov;Violence is the last refuge of the incompetent.
...
```

5. Archives are created of the `Directories` directory including all files and directories it may contain, but not the directory itself.
    - A `.zip` archive called `archive.zip` of `Directories` is saved under `/home/ubuntu/disk`
    - A `.tar` archive called `archive.tar` of `Directories` is saved under `/home/ubuntu/disk`

6. Use `df` to create a report of filesystem usage and save it as a report on your disk.
    - `report.txt` is created under the `Regular Files` directory
    - It contains the disk usage of `ext4` filesystems available in your system in human-readable format (KBs, MBs, GBs, etc. instead of bytes)
    - The first line of `report.txt` should be the command and flag(s) used to create the report file itself

7. An empty disk is a sad disk :(
To mitigate this, after you've finished every other task before this download data from the Internet and fill up the remaining space on the disk.
    - `wget` is used to [download 1MB large files](http://speedtest4.tele2.net/#http) until the 4MB disk is completely full

## General requirements

None

## Hints

- To learn a file's absolute path you can use the `readlink -f` or the `realpath` commands
- When dealing with hard links notice that it's not possible to create them _across_ file-systems
  1. Try hard linking `/etc/paperfile` to `/home/ubuntu/disk/Hard Links/` on the mounted disk
  1. If this fails, copy the file to the `Regular Files` directory and hard link `/home/ubuntu/disk/Regular Files/paperfile` to `/home/ubuntu/disk/Hard Links/`
  1. What did you notice?
- You might also wonder, _why didn't they ask me to create a hard link for a directory?_
  Well, in short, it's (usually) not possible to do so, don't bother.
  Most modern operating systems prevent you from doing such a thing
- **When you are reading background materials:**
  - [Linux File Types](https://www.youtube.com/watch?v=7KTk8NVB1N8) (focus on **regular files**, **directories**, and **symbolic links**, other file types like block and character devices, named pipes and sockets are for another day)

## Background materials

- <i class="far fa-exclamation"></i> [Everything is a file](https://en.wikipedia.org/wiki/Everything_is_a_file)
- <i class="far fa-exclamation"></i> [What Does "Everything Is a File" Mean in Linux?](https://www.howtogeek.com/117939/htg-explains-what-everything-is-a-file-means-on-linux/) (the main point is that since everything is a file everything has permissions attached to it as well)
- <i class="far fa-exclamation"></i> [Linux File Types](https://www.youtube.com/watch?v=7KTk8NVB1N8)
- <i class="far fa-exclamation"></i> [Hard Links vs. Soft Links](https://www.youtube.com/watch?v=lW_V8oFxQgA)
- <i class="far fa-exclamation"></i> [Flags, Switches, and Manual Pages](https://www.youtube.com/watch?v=01aPfjHMNUU)
- <i class="far fa-exclamation"></i> [Finding the path to executables](https://www.youtube.com/watch?v=JcsCKv_pVNw)
- [Other basic Linux commands](https://factorpad.com/tech/linux-essentials/outline.html)
