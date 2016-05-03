---
layout: lesson
root: .
title: Importing and downloading data 
minutes: 15
---

## Learning Objectives

- Be able to import data onto a server:
    - from one server (or your computer) to another server using `scp`  
    - from one server (or your computer) to another server using `rsync`  
    - from an ftp/URL
        - using `wget`
        - using `curl`
    - from SRA
    - from a grid resource (iRODS)
    - from a volume
- Be able to verify file integrity using checksums
- Be able to preview and decompress compressed files
- Understand the 'life cycle of data'

## Lesson

Just like laboratory bench work, a good analysis depends on having the right reagents. Besides the data that you have produced in your experiment, you will also need to have access to reference genomes, annotations, and software. While most reagents may be labeled with expiration dates or lot numbers, your data also need to pass 'smell tests' - some checks you can use to examine and verify data integrity. 

Before you can even get to examine the data you will often have to move it either from your computer or an online database to your cloud instance or HPC server. This is getting easier, but is not guaranteed to be foolproof or fun. The exercises below will explain a few useful methods and show you how to use them. 

![XKCD 'File Transfer' Comic](http://imgs.xkcd.com/comics/file_transfer.png)

> **Tip:** For the purpose of these lessons, we have pretty much staged all the large data files you will need during the workshop. If a link is broken, or or a download does not proceed we should have all the files needed already in place. 


## Exercises 

### Choices, Choices, Choices

According to the learning objectives, we want you to know about 7 methods to transfer data onto your remote server. If you are learning these at the workshop, we will probably only have time to cover 2-3 methods. Please come back and consider/try the rest if these are useful. Please also note, that many of these methods can be used in many more situations that we will cover in these examples. Many of these programs will also have options we will not cover in the workshop so read the man pages, especially when you want to ask the question can program `xxx` do `yyy`? It probably can, check the man page!

#### Important Caveats 
- We will only discuss getting data onto your cloud/HPC server; see the [DATAROUNDTRIPPING LESSON - PLACEHOLDER]()
- Many of the programs covered don't have a simple alternative for PC. Since `scp` is the simplest, we will cover that here. For PC users who must try some of the other programs, [Cygwin](https://www.cygwin.com/) is comprehensive (but not necessarily light-weight) way to use PC friendly alternatives. 


**A. Moving files from your local machine to a remote machine using `scp`**

**Program:** `scp` - [scp man page](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man1/scp.1?query=scp&sec=1)

**When to use:** When you have one or a few smaller (<100mb) files to transfer from your computer to a remote machine. 

**Example Usage:** 
```bash
$ scp /dir_on_your_computer/file_on_your_computer.file your_username@remotehost.edu:/remote/directory 
```
>**MAC/Linux vs PC difference:** Since PC has no scp, you can use [PSCP](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) following the directions below:

#### PC

Using PC, we recommend you use the *PSCP* program. This program is from the same suite of tools as the putty program we have been using to connect. 

1. If you haven't done so, download pscp from [http://the.earth.li/~sgtatham/putty/latest/x86/pscp.exe](http://the.earth.li/~sgtatham/putty/latest/x86/pscp.exe)
2. Make sure the *PSCP* program is somewhere you know on your computer. In this case, your Downloads folder is appropriate. 
3. Open the windows [PowerShell](https://en.wikipedia.org/wiki/Windows_PowerShell); go to your start menu/search enter the term **'cmd'**; you will be able to start the shell (the shell should start from C:\Users\your-pc-username>). 
4.Change to the download directory
```
> cd Downloads
```
5. locate a file on your computer that you wish to upload (be sure you know the path). Then upload it to your remote machine (**you will need to know your ip address, and login credentials**). You will be prompted to enter a password, and then your upload will begin. **(make sure you use substitute 'your-pc-username' for your actual pc username)**

   ```
C:\User\your-pc-username\Downloads> pscp.exe local_file.txt dcuser@ip.address:/home/dcuser/
```

#### MAC/Linux

1. Open the terminal and use the *scp* command to upload a file (e.g. local_file.txt) to the dcuser home directory:

   ```bash
$  scp local_file.txt dcuser@ip.address:/home/dcuser/
```

---
### `scp` challenge
1. Copy a small text file from your your laptop to your remote machine's home directory. 

---
 
**B. Moving files from your local machine to a remote machine using `rsync`**

**Program:** `rsync` - [rsync man page](http://linuxcommand.org/man_pages/rsync1.html)

**When to use:** When you have large (>100mb)/lots of files to transfer from your computer to a remote machine. `rsync` will compare files and directories and copy only missing or incomplete files.  

**Example Usage:** 
```bash
$ rsync /dir_on_your_computer/file_on_your_computer.file your_username@remotehost.edu:/remote/directory     
```

### `rsync` options

`rsync` has some important options that are too good to skip over:

**`rsync -a`**: The archive option allows you to copy directories (recursively) and preserve special unix filesystem features associated with files (such as modification date, permissions, etc.)

**`rsync -anv`**: In addition to the archive option, adding `n` (dry-run) and `v` (verbose) allows you to preview a list of the files that *would* be transferred   without the `n` option. 

---
### `rsync` challenge
On your local computer choose (or create) a directory with at least one file. Try the following and observe the results assuming your directory and file have the path `/dir/file.file`

1. What is the difference between copying your directory `-anv` options if you use or omit a trailing slash (e.g. copying `rsync -anv /dir` vs. `rsync -anv /dir/`?
2. What does `rsync` do when you use the `-P` option?
3. what does `rsync -c` do?

---

**C. Importing/downloading files from a URL (e.g. ftp) to a remote machine using `curl` or `wget`**

**Program:** 
- `wget` - [wget man page](https://www.gnu.org/software/wget/manual/wget.html)
- `curl` - [curl man page](http://manpages.debian.org/cgi-bin/man.cgi?query=curl&apropos=0&sektion=0&manpath=Debian%20unstable%20sid&format=html&locale=en)

**When to use:**  

**Example Usage:** 
```bash
$     
```
