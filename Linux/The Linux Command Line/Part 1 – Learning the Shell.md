Part 1 – Learning the Shell

## What Is the Shell?

- The shell is a program that takes keyboard commands and passes them to the operating system to carry out.
- Almost all Linux distributions supply a shell program from the GNU Project called bash.
- The name “`bash`” is an acronym for “**Bourne Again SHell**”, a reference to the fact bash is an enhanced replacement for `sh`, the original Unix shell program written by Steve Bourne.

### Terminal Emulators

- When using a graphical user interface (GUI), we need another program called a **terminal emulator** to interact with the shell.
- If we look through our desktop menus, we will probably find one. **KDE** uses **konsole** and **GNOME** uses **gnome-terminal**, though it's likely called simply “**terminal**” on our menu.
- A number of other terminal emulators are available for Linux, but they all basically do the same thing; give us access to the shell.

### Making Your First Keystrokes

➦ Launch the terminal emulator! Once it comes up, we should see some-
thing like this:
`[me@linuxbox ~]$`
➦ This is called a shell prompt and it will appear whenever the shell is ready to accept input.
It will typically include your `username@machinename`

**Note**: If the last character of the prompt is a **pound sign** (“#”) rather than a **dollar sign**, the terminal session has `superuser privileges`.

➦ This means either we are logged in as the `root user` or we selected a terminal emulator that provides superuser (**administrative**) privileges.

**Note**:
➦ If you **highlight some text by holding down the left mouse button** and dragging the mouse over it (or **double clicking on a word**), *it is copied* into a buffer maintained by X. **Pressing the middle mouse button** will cause the text to be *pasted* at the cursor location.

➦ **Don't** be tempted to use **Ctrl-c** and **Ctrl-v** to perform copy and paste inside a terminal window.

### Some Simple Commands

➦ **date**

```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ date
Monday 03 May 2021 08:11:11 PM IST
```

➦**Calendar**

```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ cal
May 2021
Su Mo Tu We Th Fr Sa
                   1
2  3  4  5  6 7    8
9 10 11 12  13  14 15
16 17 18 19 20 21 22
23 24  25  26 27 28 29
30  31
```

➦ **Free Space in Disk**

```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ df
```

➦ **Free Memory**

```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ free
```

### Ending a Terminal Session

We can end a terminal session by either **closing the terminal emulator window**, by entering the `exit` **command** at the shell prompt, or pressing `Ctrl-d`.

#### The Console Behind the Curtain

- Even if we have no terminal emulator running, several terminal sessions continue to run behind the graphical desktop.
- We can access these sessions, called ***virtual terminals*** or ***virtual consoles***, by pressing `Ctrl-Alt-F1` **through** `Ctrl-Alt-F6` on most Linux distributions.
- When a session is accessed, it presents a login prompt into which we can **enter** our **username** and **password**. To **switch from one virtual console** to **another**, press `Alt-F1` **through** `Alt-F6`. On most system we can **return to the graphical desktop** by pressing `Alt-F7`.

## Navigation

In this chapter we will introduce the following commands:
● pwd – Print name of current working directory
● cd – Change directory
● ls – List directory contents

### Understanding the File System Tree

- Like **Windows**, a **Unix-like** operating system such as **Linux** organizes its files in what is called a ***hierarchical directory*** structure.
- This means they are **organized** in a **tree-like** pattern of **directories** (sometimes called folders in other systems), which may contain files and other directories.
- The ***first directory*** in the file system is called the ***root directory***.
- **Note** that **unlike Windows**, which has a **separate file system tree** for each storage device, **Unix-like** systems such as **Linux** always have a **single file system tree**, *regardless of how many drives or storage devices are attached to the computer*.
- Storage devices are attached (or more correctly, **mounted**) at various points on the tree according to the whims of the system administrator, the person (or people) responsible for the maintenance of the system.

### The Current Working Directory

- At any given time, we are inside a single directory and we can see the files contained in the directory and the pathway to the directory above us (called the **parent directory**) and any **sub-directories** below us.
- The directory we are standing in is called the **current working directory**.

```
┌─┤🦆quackycoder@G580🦆~/.config/joplin-desktop├─╼
└╼ pwd
/home/quackycoder/.config/joplin-desktop
```

- Each user account is given its own home directory and it is the only place a regular user is allowed to write files.

### Listing the Contents of a Directory

To list the files and directories in the current working directory, we use the `ls` command.

```
┌─┤🦆quackycoder@G580🦆~/.config/joplin-desktop├─╼
└╼ ls
cache              log-autoupdater.txt  resources  userchrome.css
database.sqlite    log.txt              templates  userstyle.css
joplin-custom-css  plugins              tmp
```

### Changing the Current Working Directory

To change our working directory (where we are standing in our tree-shaped maze) we use the `cd` command.

```
┌─┤🦆quackycoder@G580🦆~/.config/joplin-desktop├─╼
└╼ cd /home/quackycode
┌─┤🦆quackycoder@G580🦆/home/quackycode├─╼
└╼ 
```

**`cd` Shortcuts**

|     |     |
| --- | --- |
| **Shortcut** | **Result** |
| cd  | Changes the working directory to your home directory. |
| cd - | Changes the working directory to the previous working directory. |
| cd ~user_name | Changes the working directory to the home directory of user_name. For example, cd ~bob will change the directory to the home directory of user “bob.” |

➦ **Important Facts About Filenames**
On Linux systems, files are named in a manner similar to other systems such as
Windows, but there are some important differences.

- Filenames that begin with a **period character** **are** **hidden**. This only means that `ls` **will not list them** unless you say `ls -a`.
- When your account was created, several hidden files were placed in your home directory to configure things for your account.
- Filenames and commands in Linux, like Unix, are case sensitive. The file names “**File1**” and “**file1**” refer to *different files*.
- Linux has **no concept** of a “**file extension**” like some other operating systems. *You may name files any way you like*.
- The contents and/or purpose of a file is determined by other means. Although **Unix-like operating systems don’t use file extensions** to determine the contents/purpose of files, many application programs do.
- Though **Linux supports long filenames** that may *contain embedded spaces* and *punctuation characters*, **limit the punctuation characters in the names** of files you create to **period**, **dash**, and **underscore**.
- **Most importantly**, **do not embed** `spaces` in **filenames**.
- If you want to represent spaces between words in a file name, **use underscore characters**.

## Exploring the System

Before we start however, we’re going to learn some more commands that will be useful along the way.

● `ls` – List directory contents
● `file` – Determine file type
● `less` – View file contents

### Having More Fun with `ls`

The `ls` command is probably the most used command, and for good reason.
With it, we can see **directory contents** and **determine a variety of important file and directory attributes**.

- We can even specify **multiple directories**. In the following example, we list both the user's home directory (symbolized by the “`~`” character) and the `/usr` directory.

```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls ~ /usr
/home/me:
Desktop Documents Music Pictures Public Templates Videos
/usr:
bin games include lib local sbin share src
```

- We can also **change the format of the output** to reveal **more detail**.

```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls -l
drwxr-xr-x 2 quackycoder quackycoder      4096 May  3 22:32  Desktop
drwxr-xr-x 3 quackycoder quackycoder      4096 May  3 22:31  Documents
drwxr-xr-x 8 quackycoder quackycoder      4096 May  4 01:28  Downloads
drwxrwxr-x 4 quackycoder quackycoder      4096 Apr 18 19:37  git
drwxrwxr-x 2 quackycoder quackycoder      4096 Apr 23 21:53  GitLab
drwxrwxr-x 3 quackycoder quackycoder      4096 Apr 24 16:48  Joplin
```

**Note**: By adding “`-l`” to the command, we changed the output to the **long format**.

#### Options and Arguments

- Commands are often followed by **one or more *options*** that modify their behavior, and further, by **one or more *arguments***, the items upon which the command acts.

So most commands look kinda like this:
`command -options arguments`

- Most commands use **options** which consist of **a single character preceded by a dash**, for example, “`-l`”.
- Many commands, however, including those from the GNU Project, also support **long options**, consisting of a word preceded by **two dashes**.
- Also, many commands allow **multiple short options** to be **strung together**.
- In the following example, the `ls` command is given **two options**, which are the `l` option **to produce long format** output, and the `t` option **to sort the result by the file's modification time**.

```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls -it
```

- We'll add the long option “`--reverse”` **to reverse the order** of the sort.

```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls -it --reverse
```

**Common `ls` Options**

| --- | --- | --- | --- | --- | --- |
| **Option** | **Long Option** | **Description** |
| **-a** | **--all** | List all files, even those with names that begin with a period, which are normally not listed(that is, hidden). |
| **-A** | **--almost-all** | Like the -a option above except it does not list . (current directory) and .. (parent directory). |
| **-d** | **--directory** | Ordinarily, if a directory is specified, ls will list the contents of the directory, not the directory itself. Use this option in conjunction with the -l option to see details about the directory rather than its contents. |
| **-F** | **--classify** | This option will append an indicator character to the end of each listed name. For example, a forward slash (/) if the name is a directory. |
| **-h** | **--human-readable** | In long format listings, display file sizes in human readable format rather than in bytes. |
| **-l** |  | Display results in long format|
| **-r** | --reverse | Display the results in reverse order. Normally, ls displays its results in ascending alphabetical order.|
| **-S** |  | Sort results by file size.|
| **-t** |  | Sort by modification time.|
#### A Longer Look at Long Format
`-l` option causes `ls` to display its results in long format. This format contains a great deal of useful information. Here is the Examples:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls -l
-rw-r--r-- 1 root root 3576296 May 3 11:05 Experience ubuntu.ogg
-rw-r--r-- 1 root root 1186219 May  3 11:05 kubuntu-leaflet.png
-rw-r--r-- 1 root root 47584   Apr 18 11:05 logo-Edubuntu.png
-rw-r--r-- 1 root root 44355   Apr 23 11:05 oo-derivatives.doc
```
**`ls` Long Listing Fields**
| --- | --- | --- | --- | --- | --- |
| **Field** | **Meaning** |
| **-rw-r--r--** | Access rights to the file. The first character indicates the type of file. Among the different types, a leading dash means a regular file, while a “d” indicates a directory. The next three characters are the access rights for the file's owner, the next three are for members of the file's group, and the final three are for everyone else.|
| 1 | File's number of hard links. See the sections "Symbolic Links" and "Hard Links" later in this chapter. |
| root | The username of the file's owner. |
| root | The name of the group that owns the file. |
| 32059 | Size of the file in bytes. |
| May 3 11:05 | Date and time of the file's last modification. |
| oo-cd-cover.odf | Name of the file. |
### Determining a File's Type with `file`
- As we explore the system it will be useful to know what files contain.
- To do this we will use the `file` command to determine a **file's type**.

We can invoke the file command this way:
`file filename`
```
┌─┤🦆quackycoder@G580🦆~/Pictures├─╼
└╼ file CRONjob.png 
CRONjob.png: PNG image data, 1249 x 699, 8-bit/color RGBA, non-interlaced
```
#### Viewing File Contents with less
- The `less` command is a program **to view text files**.
- Throughout our Linux system, there are many files that contain **human-readable text**. The `less` program provides a **convenient way to examine** them.

The less command is used like this:
`less filename`
- Once started, the less program **allows us to scroll forward and backward** through a text file.
```
┌─┤🦆quackycoder@G580🦆~/Pictures├─╼
└╼ less /etc/passwd
```
- **To exit** `less`, press the `q` key.

**`less` Commands**
| --- | --- | --- | --- | --- | --- |
| **Command** | **Action** |
| **Page Up or b**  | Scroll back one page |
| **Page Down or space** | Scroll forward one page |
| **Up arrow** | Scroll up one line |
| **Down arrow** | Scroll down one line |
| **G** | Move to the end of the text file |
| **1G or g** | Move to the beginning of the text file |
| **/characters** | Search forward to the next occurrence of characters |
| **n** | Search for the next occurrence of the previous search |
| **h** | Display help screen |
| **q** | Quit less |

**Interesting Facts:**
- The `less` program was designed as **an improved replacement** of an earlier Unix program called `more`.
- The name “`less`” is a play on the phrase “***less is more***” — a motto of modernist architects and designers.
- `less` falls into the class of programs called “`pagers`,” programs that **allow the easy viewing of long text documents** in a page by page manner.
- Whereas the `more` program could **only page forward**, the `less` program **allows paging both forward and backward** and has many other features as well.

- If we **accidentally attempt to view a non-text file** and it scrambles the terminal window, we can recover by entering the `reset` command.
### Linux Directories
**Directories Found on Linux Systems**
| --- | --- | --- | --- | --- | --- |
| **Directory** | **Comments** |
| **/** | The root directory. Where everything begins. |
| **/bin** | Contains binaries (programs) that must be present for the system to boot and run. |
| **/boot** | Contains the Linux kernel, initial RAM disk image (for drivers needed at boot time), and the boot loader. <br> Interesting files:<br> ● /boot/grub/grub.conf or menu.lst, which are used to configure the boot loader.<br>● /boot/vmlinuz (or something similar), the Linux kernel|
| **/dev** | This is a special directory that contains device nodes. “Everything is a file” also applies to devices. Here is where the kernel maintains a list of all the devices it understands. |
| **/etc** | The /etc directory contains all of the system-wide configuration files. It also contains a collection of shell scripts that start each of the system services at boot time. Everything in this directory should be readable text.<br><br> Interesting files: While everything in /etc is interesting, here are some all-time favorites:<br>● /etc/crontab, a file that defines when automated jobs will run.<br>● /etc/fstab, a table of storage devices and their associated mount points.<br>● /etc/passwd, a list of the user accounts. |
| **/home** | In normal configurations, each user is given a directory in /home. Ordinary users can only write files in their home directories. This limitation protects the system from errant user activity. |
| **/lib** | Contains shared library files used by the core system programs. These are similar to dynamic link libraries (DLLs) in Windows. |
| **/lost+found** | Each formatted partition or device using a Linux file system, such as ext4, will have this directory. It is used in the case of a partial recovery from a file system corruption event. Unless something really bad has happened to our system, this directory will remain empty. |
| **/media** | On modern Linux systems the /media directory will contain the mount points for removable media such as USB drives, CD-ROMs, etc. that are mounted automatically at insertion. |
| **/mnt** | On older Linux systems, the /mnt directory contains mount points for removable devices that have been mounted manually. |
| **/opt** | The /opt directory is used to install “optional” software. This is mainly used to hold commercial software products that might be installed on the system. |
| **/proc** | The /proc directory is special. It's not a real file system in the sense of files stored on the hard drive. Rather, it is a virtual file system maintained by the Linux kernel. The “files” it contains are peepholes into the kernel itself. The files are readable and will give us a picture of how the kernel sees the computer. |
| **/root** | This is the home directory for the root account. |
| **/sbin** | This directory contains “system” binaries. These are programs that perform vital system tasks that are generally reserved for the superuser. |
| **/tmp** | The /tmp directory is intended for the storage of temporary, transient files created by various programs. Some configurations cause this directory to be emptied each time the system is rebooted. |
| **/usr** | The /usr directory tree is likely the largest one on a Linux system. It contains all the programs and support files used by regular users. |
| **/usr/bin** | /usr/bin contains the executable programs installed by the Linux distribution. It is not uncommon for this directory to hold thousands of programs. |
| **/usr/lib** | The shared libraries for the programs in /usr/bin. |
| **/usr/bin** | /usr/bin contains the executable programs installed by the Linux distribution. It is not uncommon for this directory to hold thousands of programs. |
| **/usr/local** | The /usr/local tree is where programs that are not included with the distribution but are intended for system-wide use are installed. Programs compiled from source code are normally installed in /usr/local/bin. On a newly installed Linux system, this tree exists, but it will be empty until the system administrator puts something in it. |
| **/usr/sbin** | Contains more system administration programs. |
| **/usr/share** | /usr/share contains all the shared data used by programs in /usr/bin. This includes things such as default configuration files, icons, screen backgrounds, sound files, etc. |
| **/usr/share/doc** | Most packages installed on the system will include some kind of documentation. In /usr/share/doc, we will find documentation files organized by package. |
| **/var** | With the exception of /tmp and /home, the directories we have looked at so far remain relatively static, that is, their contents don't change. The /var directory tree is where data that is likely to change is stored. Various databases, spool files, user mail, etc. are located here. |
| **/var/log** | /var/log contains log files, records of various system activity. These are important and should be monitored from time to time. The most useful ones are /var/log/messages and /var/log/syslog. Note that for security reasons on some systems only the superuser may view log files. |

### Symbolic Links
As we look around, we are likely to see a directory listing (for example, /lib) with an entry like this:
```
lrwxrwxrwx 1 root root 11 2007-08-11 07:34 libc.so.6 -> libc-2.6.so
```
- Notice how the first letter of the listing is “`l`” and the entry seems to have **two filenames**?
- This is a **special kind of a file** called a ***symbolic link*** (also known as a ***soft link*** or ***sym-link***).
- In most Unix-like systems it is possible to have a file referenced by **multiple names**.
## Manipulating Files and Directories
We will know about these commands:
● `cp` – Copy files and directories
● `mv` – Move/rename files and directories
● `mkdir` – Create directories
● `rm` – Remove files and directories
● `ln` – Create hard and symbolic links

- These **five commands** are among the **most frequently used Linux commands**. 
- They are used for **manipulating both** **files** and **directories**.

If you are thinking some of these task can be much easier using a graphical file manager, then you are not completely right. Though you are not completely wrong, the **CLI** is more **powerful** and **flexible**. 

**For ex**:
Imagine this scenario: 
**How could we copy all the HTML files from one directory to another but only copy files that do not exist in the destination directory or are newer than the versions in the destination directory?**

- It's **pretty hard with a file manager** but **pretty easy with the command line**.
With this simple command, you can achieve it:
`cp -u *.html destination`

### Wildcards
- Since the shell uses filenames so much, it provides special characters to help us rapidly specify groups of filenames. 
- These special characters are called ***wildcards(which is also known as globbing)***

**Wildcards notations**:
| --- | --- | --- | --- | --- | --- |
| **Wildcard** | **Meaning** |
| **\*** | Matches any characters |
| **?** | Matches any single character |
| **[characters]** | Matches any character that is a member of the set characters |
| **[!characters]** | Matches any character that is not a member of the set characters |
| **[[:class:]]** | Matches any character that is a member of the specified class |


**Commonly Used Character Classes**
| --- | --- | --- | --- | --- | --- |
| **Character Class** | **Meaning** |
| **[:alnum:]** | Matches any alphanumeric character |
| **[:alpha:]** | Matches any alphabetic character |
| **[:digit:]** | Matches any numeral |
| **[:lower:]** | Matches any lowercase letter |
| **[:upper:]** | Matches any uppercase letter |

- Using wildcards **makes it possible to construct sophisticated selection** criteria for file- names.
- Wildcards can be used with **any command that accepts filenames** as **arguments**.

**Wildcard Examples**
| --- | --- | --- | --- | --- | --- |
| **Pattern** | **Matches** |
| **\*** | All files |
| **g\*** | Any file beginning with “g” |
| **b\*.txt** | Any file beginning with “b” followed by any characters and ending with “.txt” |
| **Data???** | Any file beginning with “Data” followed by exactly three characters |
| **[abc]\*** | Any file beginning with either an “a”, a “b”, or a “c” |
| **BACKUP.[0-9][0-9][0-9]** | Any file beginning with “BACKUP.” followed by exactly three numerals |
| **[[:upper:]]\*** | Any file beginning with an uppercase letter |
| **[![:digit:]]\*** | Any file not beginning with a numeral |
| **[:upper:]** | Matches any uppercase letter |
| **\*[[:lower:]123]** | Any file ending with a lowercase letter or the numerals “1”, “2”, or “3” |

<br><br><br><br>


**Important**:

**Be Careful** with `rm`!
- Be particularly careful with **wildcards**. Consider this classic example: 
- Let's say you want to **delete just the HTML files** in a directory. 
- To do this, you type the following:
`rm *.html`
- This is **correct**, **but** if you **accidentally place a space between the * and the .html** like so:
`rm * .html`
- The `rm` command will **delete all the files** in the directory and then complain that there is no file called .html.

**Useful tip:**
- whenever you use wildcards with `rm` (besides **carefully checking your typing**!), **test the wildcard** first with **ls**.
- This will let **you see the files that will be deleted**. 
- Then **press the up arrow key** to recall the command and **replace** `ls` with `rm`.
## Working with Commands
The commands we will know:

● `type` – Indicate how a command name is interpreted

syntax: `type command`

**Ex**:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ type ls
ls is aliased to `ls --color=auto'
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ type cp
cp is /usr/bin/cp
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ type cd
cd is a shell builtin
```

● `which` – Display which executable program will be executed

syntax: `type command`

**Ex**:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ which ls
/usr/bin/ls
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ which cp
/usr/bin/cp
```
● `help` – Get help for shell builtins

Ex:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ help ls
bash: help: no help topics match `ls'.  Try `help help' or `man -k ls' or `info ls'.
```
● `man` or `tldr`or `cs`(cheatsheet.sh) – Display a command's manual page
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ man ls
NAME
       ls - list directory contents

SYNOPSIS
       ls [OPTION]... [FILE]...
..............
.............
```
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ tldr ls
- List files one per line:
   ls -1

 - List all files, including hidden files:
   ls -a

 - List all files, with trailing / added to directory names:
   ls -F
.....................
....................
```
- The “manual” that man displays is broken into sections and covers not only user commands but also system administration commands, programming interfaces, file formats and more.
| --- | --- | --- | --- | --- | --- |
| **Section** | **Contents** |
| **1** | User commands |
| **2** | Programming interfaces for kernel system calls |
| **3** | Programming interfaces to the C library |
| **4** | Special files such as device nodes and drivers |
| **5** | File formats |
| **6** | Games and amusements such as screen savers |
| **7** | Miscellaneous |
| **8** | System administration commands |

**Ex**:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ man 5 passwd
```
● `apropos` – Display a list of appropriate commands

**Ex**:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ apropos partition
addpart (8)          - tell the kernel about the existence of a partition
cfdisk (8)           - display or manipulate a disk partition table
cgdisk (8)           - Curses-based GUID partition table (GPT) manipulator
delpart (8)          - tell the kernel to forget about a partition
fdisk (8)            - manipulate disk partition table
```
- **Note** that the `man` command with the “`-k`” option performs the same function as apropos.
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ man -k partition
addpart (8)          - tell the kernel about the existence of a partition
cfdisk (8)           - display or manipulate a disk partition table
cgdisk (8)           - Curses-based GUID partition table (GPT) manipulator
delpart (8)          - tell the kernel to forget about a partition
fdisk (8)            - manipulate disk partition table
```
● `info` – Display a command's info entry
- The GNU Project provides an **alternative** to man pages for their programs, called “`info`.”
- Info manuals are displayed with a **reader program named**, **appropriately enough**, **info**.
- Info pages are ***hyperlinked*** much like web pages.
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ info ls
```
● `whatis` – Display one-line manual page descriptions

**Ex**:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ whatis ls
ls (1)               - list directory contents
```
● `alias` – Create an alias for a command
- It's possible to put more than one command on a line by separating each command with a semicolon. 

It works like this:
`command1; command2; command3...`

**Ex**:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ cd /usr; ls; cd -
bin    include  lib32  libexec  local  share
games  lib      lib64  libx32   sbin   src
/home/quackycoder
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ 
```
- First we change directory to `/usr` then **list the directory** and finally **return to the original directory** (by using '`cd -`') so we end up where we started.
- Now let's turn this sequence into a **new command** using **alias**.

**Syntax**:
`alias name='string'`

**Ex**:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ alias foo='cd /usr; ls; cd -'
```
- To **remove** an **alias**, the **unalias** command is used, like so:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ unalias foo
```
- **To see all the aliases defined** in the environment, **use** the `alias` command **without arguments**.
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ alias 
alias cd..='cd ..'
alias grep='grep --color'
alias ls='ls --color=auto'
```
- There is **one tiny problem** with defining aliases on the command line. They **vanish when our shell session ends**.
## Redirection
One of the coolest features of command line is **I/O redirection**.

- The “`I/O`” stands for **input/output** and with this facility we can *redirect the input and output of commands to and from files*.
-  It can also **connect multiple commands together into powerful command pipelines**.

To show off this facility, we will introduce the following commands:

● `cat` – Concatenate files
● `sort` – Sort lines of text
● `uniq` – Report or omit repeated lines
● `grep` – Print lines matching a pattern
● `wc` – Print newline, word, and byte counts for each file
● `head` – Output the first part of a file
● `tail` – Output the last part of a file
● `tee` – Read from standard input and write to standard output and files

### Standard Input, Output, and Error
- Many of the programs produce output of some kind which consists of two types:
 • The **program's results**, that is, the data the    program is designed to produce
 • **Status and error messages** that tell us how      the program is getting along
 
 - Keeping with the Unix theme of “**everything is a file**,” programs such as `ls` actually send their results to a special file called **standard output** (often expressed as **stdout**) and their **status messages** to another file called **standard error** (**stderr**). 
 - By default, both **standard output** and **standard error** are **linked to the screen** and **not saved into a disk file**.
 - In addition, many programs take input from a facility called **standard input** (**stdin**), which is, by default, **attached to the keyboard**.
 - **I/O redirection** allows us to change **where output goes and where input comes from**. 
 - Normally, **output goes to the screen** and **input comes from the keyboard**, but **with I/O redirection**, **we can change that**.

- To redirect **standard output** to another file instead of the screen, we use the `>` **redirection operator** followed by the **name of the file**.

Ex:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls -l /usr/bin > ls-output.txt

```
- if we ever need to actually **truncate a file** (or **create a new, empty file**), we can use a trick like this:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ > ls-output.txt
```
- **Simply using the redirection operator** with **no command preceding it** will **truncate an existing file** or **create a new, empty file**.
- To **append** redirected output to a file **instead of overwriting** the file, we use `>>` redirection operator. 

Ex:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls -l /usr/bin >> ls-output.txt
```
- **If the file does not already exist**, **it is created** just as though the `>` operator had been used.
### Redirecting Standard Error
- **Redirecting standard error** lacks the ease of a dedicated redirection operator. 
- **To redirect standard error** we must **refer to its file descriptor**.
- A program can produce output on any of several numbered file streams.
- While we have referred to the first three of these file streams as **standard input**, **output** and **error**, the **shell references them** internally as file descriptors **0**, **1**, and **2**, respectively.
- Since **standard error** is the same as **file descriptor number 2**, we can redirect **standard error** with this notation:

Ex:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls -l /bin/usr 2> ls-error.txt
```
### Redirecting Standard Output and Standard Error to One File
There are **two ways** to do this.

1. **Traditional way**
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls -l /bin/usr > ls-output.txt 2>&1
```
- Using this method, **we perform two redirections**. 
- **First** we redirect standard output to the file `ls-output.txt` 
- And then we redirect **file descriptor 2** (**standard error**) to **file descriptor 1** (**standard output**) using the notation `2>&1`.
- **Notice that the order of the redirections is significant**. The redirection of **standard error must always occur after redirecting standard output** or it doesn't work.
- The following example **redirects standard error to the file** *ls-output.txt*:
`>ls-output.txt 2>&1`

- However, if the order is changed to the following, **standard error is directed to the screen**.
`2>&1 >ls-output.txt`

2. **More streamlined method**
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls -l /bin/usr &> ls-output.txt
```
- we use the single notation `&>` to redirect **both** **standard output** and **standard error** to the file ls-output.txt.
- We can also **append** the **standard output and standard error** streams to a single file like so:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls -l /bin/usr &>> ls-output.txt
```
### Disposing of Unwanted Output
- If we **don't want output from a command**, we just want to throw it away, particularly the **error and status messages**, we redirect the output to a **special file** called “`/dev/null`”. 
- **This file** is a **system device** often referred to as a **bit bucket**, which **accepts input and does nothing** with it.

Ex:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls -l /bin/usr 2> /dev/null
```
### Redirecting Standard Input
`cat` – Concatenate Files
- The cat command **reads one or more files** and **copies them to standard output** like so:
`cat [file...]`
- `cat` is often used to display short text files.
- Since cat can accept more than one file as an argument, it can also be **used to join files together**.

**Ex**:
If the files were named:
movie.mpeg.001, movie.mpeg.002, ... movie.mpeg.099
`cat movie.mpeg.0* > movie.mpeg`

- What happens if we enter `cat` **with no arguments**?

**Ans**:
- It reads from **standard input** and since standard input is, by default, attached to the keyboard, it's **waiting for us to type something**!
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ **cat** The quick brown fox jumped over the lazy dog.`
```
- Next, type a `Ctrl-d` to tell cat that it has
reached **end of file** (**EOF**) on **standard input**:

```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ cat
The quick brown fox jumped over the lazy dog.
The quick brown fox jumped over the lazy dog.
```

- In the **absence of filename arguments**, `cat` **copies standard input** to **standard output**, so we see our **line of text repeated**.
- We can use this behavior to **create short text files**.

**Ex**:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ cat > lazy_dog.txt
The quick brown fox jumped over the lazy dog.
```
- Type the command followed by the text we want to place in the file. 
- Remember to type `Ctrl-d` at the **end**.
- To see our results, we can use `cat` to **copy the file** to **stdout** again.

**Ex**:

```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ cat lazy_dog.txt
The quick brown fox jumped over the lazy dog.
```
- That's how `cat` accepts standard input, in addition to filename arguments.

Let's try redirecting standard input:

```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ cat < lazy_dog.txt
The quick brown fox jumped over the lazy dog.
```
- Using the `<` redirection operator, we **change the source** of **standard input** from the keyboard **to the file** *lazy_dog.txt*.
- The result is the **same as passing a single filename argument**.
- This is **not particularly useful** compared to passing a filename argument, but it **serves to demonstrate using a file as a source of standard input**.
### Pipelines
- The capability of **commands to read data from standard input** and **send to standard output** is utilized by a shell feature called **pipelines**.

**Ex**:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls -l /usr/bin | less
```
- Using this technique, we can conveniently **examine the output of any command** that **produces standard output**.

**NOTE**:
**The Difference Between `>` and `|`**

- The **redirection operator**,`>`, **connects a command with a file**.
- The **pipeline operator**,`|`, **connects the output of one command with the input of a second command**.

**Ex**:
`command1 > file1`

`command1 | command2`

**NOTE**:
A lot of people will try the following when they are learning about pipelines, “just to see what happens”:

They can turn less into a mess!:D

This is how:

As the **superuser**, if you do this:
 ```
cd /usr/bin
 ls > less
```
- The **first command** put him in the directory where most programs are stored. 
- The **second command** told the shell to **overwrite the file** `less` with the **output of the** `ls` command.
- Since the `/usr/bin` directory **already contained** a file named `less` (the `less` program), the **second command** **overwrote** the `less` program file with the text from `ls`, thus **destroying the** `less` program on the system.
- The lesson here is that the **redirection operator** silently **creates or overwrites files**, so you need to treat it with a lot of respect.

#### Filters
- Filters take input, change it somehow, and then output it.
- The first one we will try is `sort`.
- Imagine we wanted to make a combined list of all the executable
programs in `/bin` and `/usr/bin`, put them in sorted order and view the resulting list:
**Example**:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls /bin /usr/bin | sort | less
```
- Since we specified two directories (`/bin` and `/usr/bin`), the output of ls would have consisted of two sorted lists, one for each directory.
- By including `sort` in our pipeline, we changed the data to produce a single, sorted list.
#### uniq - Report or Omit Repeated Lines
- The `uniq` command is often used in conjunction with `sort`.
- `uniq` accepts a sorted list of data from either standard input or a single filename argument and, by default, removes any duplicates from the list.
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls /bin /usr/bin | sort | uniq | less
```
- In this example, we use `uniq` to **remove** any duplicates from the output of the `sort` command. If we want **to see the list of duplicates instead**, we add the “`-d`” option to `uniq` like so:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls /bin /usr/bin | sort | uniq -d | less
```
#### wc – Print Line, Word, and Byte Counts
- The `wc` (**word count**) command is used to display the **number of lines**, **words**, and **bytes contained** in files. Here's an example:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ wc file.txt
```
- If executed without command line arguments, `wc` accepts **standard input**.
- The “`-l`” option limits its output to only report lines.
- To see the **number of items** we have in our sorted list, we can do this:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls /bin /usr/bin | sort | uniq | wc -l
```
#### grep – Print Lines Matching a Pattern
- `grep` is a powerful program used to **find text patterns** within files. It's used like this:
```
grep pattern [file...]
```
- When `grep` encounters a “**pattern**” in the file, it **prints out the lines** containing it.
- Let's say *we wanted to find all the files in our list of programs that had the word* **zip** embedded in the name.
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls /bin /usr/bin | sort | uniq | grep zip
```
- There are a couple of handy options for grep:
• `-i`, which causes grep to **ignore case** when performing the search (normally searches are case sensitive)
• `-v`, which tells `grep` to **print only those lines that *do not match the pattern***.
#### head / tail – Print First / Last Part of Files
- The `head` command prints the **first ten lines of a file**, and the `tail` command prints the **last ten lines**.
- **By default**, both commands print **ten lines** of text, but this **can be adjusted** with the `-n` option.
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ head -n 5 file.txt
```
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ tail -n 5 file.txt
```
- These can be used in **pipelines** (`|`)as well:
 ```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls /usr/bin | tail -n 5
```
- `tail` has an option(`-f`) which **allows us to view files in real time**. This is **useful for watching the progress of log files** as they are being written.
- We will look at the **messages** file in `/var/log` (or the `/var/log/syslog` file if **messages** is missing).
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ sudo tail -f /var/log/messages
```
- Using the “`-f`” option, `tail` **continues to monitor the file**, and when new lines are appended, they immediately appear on the display. This continues until we press `Ctrl-c`.
#### tee – Read from Stdin and Output to Stdout and Files
- Linux provides a command called `tee` which creates a “`tee`” fitting on our pipe.
- The `tee` program **reads standard input** and **copies it to both standard output** (allowing the data to continue down the pipeline) and to one or more files.
- This is **useful for capturing a pipeline's contents** at an **intermediate stage of processing**.
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls /usr/bin | tee ls.txt | grep zip
```
**Summing Up**

- There are **many commands** that make use of **standard input** and **output**, and **almost all command line programs** use **standard error** to display their informative messages.
## Seeing the World as the Shell Sees It
<br>

### Expansion
- Each time we type a command and press the Enter key, bash performs several substitutions upon the text before it carries out our command.
- The process that makes this happen is called **expansion**.
- With expansion, **we enter something** and it is **expanded into something else** before the shell acts upon it.

**Ex**:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo *
```
- Why didn't `echo` print **\***?
- The __*__ is a wildcard character means **match any characters** in a filename
- The shell expands the __*__ into something else (in this instance, the **names of the files in the current working directory**) before the `echo` command is executed.
- So the echo command never saw the __*__, **only its expanded result**.
#### Pathname Expansion
- The mechanism by which **wildcards** work is called ***pathname expansion***.
- we could carry out the following expansions:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo D*
Desktop Devops Documents Downloads
```
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo *s
Books Devops Documents Downloads Pictures Templates Videos
```
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo [[:upper:]]*
Books Desktop Devops Documents Downloads
```
**NOTE**:
**Pathname Expansion of Hidden Files**

- An expansion such as the following does not reveal hidden files.
```echo *```
- To better perform **pathname expansion** in this situation, we have to employ a more specific pattern: `echo .[!.]*`
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo .[!.]*
.aspell.en.prepl .aspell.en.pws .bash_history
```
- This pattern expands into **every filename** that begins with **only one period** followed by any other characters.
- It still won't include filenames with **multiple leading periods**.
- The `ls` command with the `-A` option (“almost all”) will provide a correct **listing of hidden files**. `ls -A`
#### Tilde (~) Expansion
- The **tilde** character (`~`) has a **special meaning**. 
- When **used at the beginning of a word**, it **expands into the name of the home directory** of the **named user** or, **if no user is named**, the home **directory of the current user**.
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo ~
/home/quackycoder
```
#### Arithmetic Expansion
- This allows us to use the **shell prompt** as a **calculator**.
- Arithmetic expansion uses the following form:
`$((expression))`
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo $((2 + 2))
4
```
**Arithmetic Operators**
| --- | --- |
| **Operator** | **Description** |
| __+__ | Addition |
| __-__ | Substraction |
| __*__ | Multiplication |
| __/__ | Division (but remember, since expansion supports only integer arithmetic, results are integers). |
| __%__ | Modulo, which simply means “remainder.” |
| __**__ | Exponentiation |
- **Spaces** are **not significant** in arithmetic expressions and **expressions may be nested**.
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo $(($((5**2)) * 3))
75
```
- **Single parentheses** may be used **to group multiple sub-expressions**.
- the previous example and get the same result using a single expansion instead of two:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo $(((5**2) * 3))
75
```
#### Brace Expansion
- Perhaps the **strangest** expansion is called **brace expansion**.
- we can **create multiple text strings** from a pattern containing braces. 
- Here's an example:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo Front-{A,B,C}-Back
Front-A-Back Front-B-Back Front-C-Back
```
- Patterns to be brace expanded may contain a **leading portion** called a ***preamble*** and a **trailing portion** called a ***postscript***.
- The **brace expression** itself may **contain either** a **comma-separated list of strings** or a **range of integers** or **single characters**.
- The pattern may not contain **unquoted whitespace**.

**EX**:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo Number_{1..5}
Number_1 Number_2 Number_3 Number_4 Number_5
```
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo {01..15}
01 02 03 04 05 06 07 08 09 10 11 12 13 14 15
```
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo {A..Z}
A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
```
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo a{A{1,2},B{3,4}}b
aA1b aA2b aB3b aB4b
```
- The **most common application** is to **make lists of files** or **directories** to be created.
- For example, if we were photographers and had a large collection of images that we wanted to **organize** into **years** and **months**
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ mkdir Photos
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ cd Photos
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ mkdir {2007..2009}-{01..12}
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls
2007-01 2007-07 2008-01 2008-07 2009-01 2009-07
2007-02 2007-08 2008-02 2008-08 2009-02 2009-08
2007-03 2007-09 2008-03 2008-09 2009-03 2009-09
2007-04 2007-10 2008-04 2008-10 2009-04 2009-10
2007-05 2007-11 2008-05 2008-11 2009-05 2009-11
2007-06 2007-12 2008-06 2008-12 2009-06 2009-12
```
#### Parameter Expansion
- It's a feature that is more useful in shell scripts than directly on the command line.
- Many of its **capabilities** have to do with the **system's ability to store small chunks (called *variables*) of data** and to **give each chunk a name**.
- For example, the *variable* named **USER** contains our **username**.
- To **invoke parameter expansion** and **reveal the contents** of **USER** we would do this:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo $USER
quackycoder
```
- To see a **list of available variables**:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ printenv | less
```
#### Command Substitution
- **Command substitution** allows us to **use the output of a command as an expansion**.
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo $(ls)
Books Desktop Devops
```
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls -l $(which cp)
-rwxr-xr-x 1 root root 153976 Sep  5  2019 /usr/bin/cp
```
- Here we **passed the results** of `which cp` as an **argument** to the `ls` command
- And getting the listing of the `cp` program **without having to know its full pathname**.
- We are not limited to just simple commands. Entire pipelines can be used: 
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ file $(ls -d /usr/bin/* | grep zip)
/usr/bin/bunzip2:      ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=00c09d800d549d58e3b7c4f6170446cc69bf14a5, for GNU/Linux 3.2.0, stripped
```
### Quoting
- The **shell** provides a mechanism called ***quoting*** to **selectively suppress unwanted expansions**.
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo This is     my  Shell
This is my Shell
```
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo The total is $100.00
The total is 00.00
```
- In the **first example**, ***word-splitting*** by the **shell removed extra whitespace** from the `echo` command's list of arguments.
- In the **second example**, **parameter expansion** **substituted an empty string** for **the value of $1 because it was an undefined variable**.
#### Double Quotes
- If we **place text** inside ***double quotes***, all the special characters used by the shell lose their special meaning and are **treated as ordinary characters**.
- The exceptions are `$`, `\` (**backslash**), and ` (**back quote**).
- **word-splitting**, **pathname expansion**, **tilde expansion**, and **brace expansion** are **suppressed**, but **parameter expansion**, **arithmetic expansion**, and **command substitution** are still **carried out**.
- Using **double quotes**, we can **cope with filenames containing embedded spaces**.
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ ls -l "two words.txt"
-rw-rw-r-- 1 quackycoder quackycoder 0 Jun 12 15:59 'two words.txt'
```
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo "$USER $((2+2)) $(cal)"
quackycoder 4      June 2021        
Su Mo Tu We Th Fr Sa  
       1  2  3  4  5  
 6  7  8  9 10 11 12  
13 14 15 16 17 18 19  
20 21 22 23 24 25 26  
27 28 29 30 
```
#### Single Quotes
- If we need **to suppress all expansions**, we **use single quotes**.
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo 'text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER'
text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER
```
#### Escaping Characters
- Sometimes we want **to quote only a single character**. To do this, we can **precede a character with a backslash** (`\`), which in this context is called the **escape character**.
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ echo "The balance for user $USER is: \$5.00"
The balance for user quackycoder is: $5.00
```
- Note that within **single quotes**, the **backslash** loses its special meaning and is **treated as an ordinary character**.
- The **backslash** is also used as part of a **notation to represent certain special characters** called ***control codes***.

| --- | --- |
| **Escape Sequence** | **Meaning** |
| __\a__ | Bell (an alert that causes the computer to beep) |
| __\b__ | Backspace |
| __\n__ | Newline. On Unix-like systems, this produces a linefeed. |
| __\r__ | Carriage return |
| __\t__ | Tab |

- Adding the `-e` option to `echo` will **enable interpretation of escape sequences**.
- You may also place them inside `$' '`.
- We can create a primitive **countdown timer**:
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ sleep 10; echo -e "Time's up\a"
Time's up
```
Or
```
┌─┤🦆quackycoder@G580🦆~├─╼
└╼ sleep 10; echo "Time's up" $'\a'
Time's up
```
## Advanced Keyboard Tricks
