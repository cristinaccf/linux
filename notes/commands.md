# 🐧 Linux Commands Cheatsheet

Quick reference for the most commonly used Linux commands.

---

## 📁 Navigation

| Command | Description                         | Memory aid                          |
| ------- | ----------------------------------- | ----------------------------------- |
| `pwd`   | Shows the current working directory | **P**rint **W**orking **D**irectory |
| `ls`    | Lists files and directories         | **L**i**s**t                        |
| `cd`    | Changes directory                   | **C**hange **D**irectory            |
| `tree`  | Shows directories as a tree         |                                     |
| `clear` | Clears the terminal                 |                                     |
| `..`    | Parent directory                    | Go one level up                     |
| `~`     | User's home directory               | Your "home"                         |

### Common options for `ls`

| Command  | Description                                |
| -------- | ------------------------------------------ |
| `ls -l`  | Detailed listing                           |
| `ls -a`  | Includes hidden files                      |
| `ls -la` | Detailed listing + hidden files            |
| `ls -lh` | Detailed listing with human-readable sizes |

---

## 📄 Files and Directories

| Command | Description                               | Memory aid                   |
| ------- | ----------------------------------------- | ---------------------------- |
| `touch` | Creates an empty file / updates timestamp | "Touch" the file             |
| `mkdir` | Creates a directory                       | **M**a**k**e **Dir**ectory   |
| `cp`    | Copies files/directories                  | **C**o**p**y                 |
| `mv`    | Moves or renames files/directories        | **M**o**v**e                 |
| `rm`    | Removes files                             | **R**e**m**ove               |
| `rmdir` | Removes empty directories                 | **R**e**m**ove **Dir**ectory |
| `file`  | Identifies the type of a file             | Literal                      |

### ⚠️ Be careful

```bash
rm -rf
```

* `-r` → recursive
* `-f` → force

Can delete directories and their contents without asking.

---

##  Reading Files

| Command | Description                 | Memory aid            |
| ------- | --------------------------- | --------------------- |
| `cat`   | Displays/concatenates files | **Cat** = concatenate |
| `less`  | Reads a file page by page   | "Less is more"        |
| `more`  | Reads a file page by page   | Literal               |
| `head`  | Shows the first lines       | Head                  |
| `tail`  | Shows the last lines        | Tail                  |
| `nl`    | Displays numbered lines     | **N**umber **L**ines  |

### Useful options

```bash
head -n 20 file
```

Shows the first 20 lines.

```bash
tail -n 20 file
```

Shows the last 20 lines.

```bash
tail -f logfile
```

Follows a file and displays new lines as they appear.

`-f` → **follow**

---

## 🔎 Searching

| Command   | Description                         | Memory aid   |
| --------- | ----------------------------------- | ------------ |
| `find`    | Searches for files/directories      | Literal      |
| `locate`  | Searches for files using a database | "Locate"     |
| `grep`    | Searches for text/patterns          | Text search  |
| `which`   | Shows the path of an executable     | "Which one?" |
| `whereis` | Locates binary, source and manual   | "Where is?"  |

### 🧠 Remember

```text
find → searches for FILES
grep → searches for TEXT
```

### `find` options

| Option    | Meaning                      |
| --------- | ---------------------------- |
| `-name`   | Search by name               |
| `-type f` | Regular files                |
| `-type d` | Directories                  |
| `-size`   | Search by size               |
| `-user`   | Search by owner              |
| `-perm`   | Search by permissions        |
| `-mtime`  | Search by modification time  |
| `-exec`   | Execute a command on results |

---

## 👤 Users

| Command  | Description                                 | Memory aid          |
| -------- | ------------------------------------------- | ------------------- |
| `whoami` | Shows the current user                      | **Who am I?**       |
| `id`     | Shows UID, GID and groups                   | Identity            |
| `who`    | Shows logged-in users                       | Who                 |
| `w`      | Shows logged-in users and activity          | Who + activity      |
| `groups` | Shows user's groups                         | Literal             |
| `sudo`   | Executes a command with elevated privileges | **Superuser Do**    |
| `su`     | Switches user                               | **S**witch **U**ser |
| `passwd` | Changes a password                          | Password            |

---

## 🔐 Permissions

| Command | Description                  | Memory aid               |
| ------- | ---------------------------- | ------------------------ |
| `chmod` | Changes file permissions     | **Ch**ange **mod**e      |
| `chown` | Changes file owner           | **Ch**ange **own**er     |
| `chgrp` | Changes file group           | **Ch**ange **gr**ou**p** |
| `umask` | Sets default permission mask | User file-creation mask  |

### Permission symbols

```text
r = read
w = write
x = execute
```

### Numeric permissions

```text
r = 4
w = 2
x = 1
```

Therefore:

```text
7 = rwx
6 = rw-
5 = r-x
4 = r--
3 = -wx
2 = -w-
1 = --x
0 = ---
```

---

## ⚙️ Processes

| Command | Description                        | Memory aid             |
| ------- | ---------------------------------- | ---------------------- |
| `ps`    | Displays processes                 | **P**rocess **S**tatus |
| `top`   | Real-time process/resource monitor | Literal                |
| `htop`  | Improved version of `top`          | `h`top                 |
| `kill`  | Sends a signal to a process        | Literal                |
| `pkill` | Sends signals to processes by name | **P**rocess **kill**   |
| `jobs`  | Shows shell jobs                   | Literal                |
| `bg`    | Sends a job to the background      | **B**ack**g**round     |
| `fg`    | Brings a job to the foreground     | **F**ore**g**round     |
| `nohup` | Runs a command immune to hangups   | **No Hang Up**         |

### Common `ps`

```bash
ps aux
```

Shows processes from all users with detailed information.

---

## 🌐 Networking

| Command         | Description                       | Memory aid                                 |
| --------------- | --------------------------------- | ------------------------------------------ |
| `ip`            | Network configuration/information | Literal                                    |
| `ping`          | Tests network connectivity        | Sonar 📡                                   |
| `ss`            | Shows sockets/connections/ports   | **S**ocket **S**tatistics                  |
| `netstat`       | Network connections/statistics    | **Net**work **stat**istics                 |
| `curl`          | Makes requests to URLs            | **Client URL**                             |
| `wget`          | Downloads files                   | Web + get                                  |
| `ssh`           | Secure remote connection          | **S**ecure **Sh**ell                       |
| `scp`           | Secure file copy over SSH         | **S**ecure **C**o**p**y                    |
| `sftp`          | Secure file transfer over SSH     | **S**SH **F**ile **T**ransfer **P**rotocol |
| `nc` / `netcat` | Creates TCP/UDP connections       | Network cat                                |
| `dig`           | Performs DNS queries              | **D**omain **I**nformation **G**roper      |
| `nslookup`      | Performs DNS queries              | **Name Server Lookup**                     |
| `traceroute`    | Shows the route to a destination  | Trace route                                |

### Useful `ip` commands

```bash
ip addr
```

Shows network interfaces and IP addresses.

```bash
ip route
```

Shows the routing table.

```bash
ip link
```

Shows network interfaces.

### Useful `ss`

```bash
ss -tuln
```

* `t` → TCP
* `u` → UDP
* `l` → listening
* `n` → numeric

Very useful for discovering listening ports.

---

## 🌍 HTTP / Web

| Command         | Description                       |
| --------------- | --------------------------------- |
| `curl`          | Make HTTP/HTTPS requests          |
| `wget`          | Download resources                |
| `nc` / `netcat` | Establish raw network connections |
| `telnet`        | Connect to a remote service       |

### Useful `curl` options

| Option | Meaning                  |
| ------ | ------------------------ |
| `-I`   | Headers only             |
| `-i`   | Include response headers |
| `-v`   | Verbose output           |
| `-X`   | Specify HTTP method      |
| `-d`   | Send data                |
| `-o`   | Save output to a file    |
| `-L`   | Follow redirects         |

---

## 🔑 SSH

```bash
ssh user@host
```

Secure remote shell.

Common options:

| Option | Description            |
| ------ | ---------------------- |
| `-p`   | Specify port           |
| `-i`   | Specify private key    |
| `-v`   | Verbose output         |
| `-L`   | Local port forwarding  |
| `-R`   | Remote port forwarding |

---

## 📦 Compression & Archives

| Command  | Description               | Memory aid       |
| -------- | ------------------------- | ---------------- |
| `tar`    | Creates/extracts archives | **Tape Archive** |
| `gzip`   | Compresses files          | **GNU zip**      |
| `gunzip` | Decompresses gzip files   | GNU unzip        |
| `zip`    | Creates ZIP archives      | Literal          |
| `unzip`  | Extracts ZIP archives     | Literal          |
| `7z`     | Works with 7-Zip archives | 7-Zip            |

### Common `tar` options

```text
c = create
x = extract
f = file
z = gzip
v = verbose
```

---

## 💾 Disks & Storage

| Command  | Description                    | Memory aid                         |
| -------- | ------------------------------ | ---------------------------------- |
| `df`     | Shows available disk space     | **D**isk **F**ree                  |
| `du`     | Shows disk usage               | **D**isk **U**sage                 |
| `lsblk`  | Lists block devices/disks      | **L**i**s**t **B**loc**k** devices |
| `mount`  | Mounts a filesystem            | Literal                            |
| `umount` | Unmounts a filesystem          | Unmount                            |
| `fdisk`  | Manages disk partitions        | **F**ixed **Disk**                 |
| `blkid`  | Shows block device identifiers | **Block ID**                       |

### 🧠 Remember

```text
df → disk FREE
du → disk USAGE
```

---

## 🖥️ System Information

| Command    | Description                                | Memory aid           |
| ---------- | ------------------------------------------ | -------------------- |
| `uname`    | Kernel/system information                  | **Unix name**        |
| `hostname` | Shows system hostname                      | Literal              |
| `uptime`   | Shows how long the system has been running | Up time              |
| `free`     | Shows RAM usage                            | Literal              |
| `lscpu`    | Shows CPU information                      | **L**i**s**t **CPU** |
| `lsblk`    | Shows block devices                        | List block devices   |
| `lsusb`    | Shows USB devices                          | List USB             |
| `lspci`    | Shows PCI devices                          | List PCI             |
| `dmesg`    | Shows kernel messages                      | Kernel messages      |
| `date`     | Shows date/time                            | Literal              |

---

## 📦 Package Management

### Debian / Ubuntu / Kali

| Command       | Description                            |
| ------------- | -------------------------------------- |
| `apt update`  | Updates package repository information |
| `apt upgrade` | Upgrades installed packages            |
| `apt install` | Installs a package                     |
| `apt remove`  | Removes a package                      |
| `apt search`  | Searches for packages                  |
| `apt show`    | Shows package information              |
| `dpkg`        | Manages `.deb` packages                |

`apt` → **Advanced Package Tool**

---

## 📝 Text Editors

| Command | Description                   | Memory aid        |
| ------- | ----------------------------- | ----------------- |
| `nano`  | Simple terminal text editor   | Easy editor       |
| `vim`   | Advanced terminal text editor | **Vi IMproved**   |
| `vi`    | Classic Unix text editor      | **Visual editor** |

---

## 🔀 Pipes & Redirection

These are not commands, but they are essential for using the Linux shell effectively.

| Symbol | Description                                             |
| ------ | ------------------------------------------------------- |
| `\|`   | Sends output to another command                         |
| `>`    | Redirects output and overwrites the file                |
| `>>`   | Redirects output and appends to the file                |
| `<`    | Uses a file as input                                    |
| `2>`   | Redirects stderr                                        |
| `2>&1` | Redirects stderr to stdout                              |
| `&>`   | Redirects stdout + stderr                               |
| `;`    | Executes multiple commands independently                |
| `&&`   | Executes the next command only if the previous succeeds |
| `\|\|` | Executes the next command if the previous fails         |
| `&`    | Runs a command in the background                        |

### 🧠 The important idea

```text
command A | command B
```

The output of **A** becomes the input of **B**.

This is one of the most powerful concepts in the Linux shell.

---

## 🧰 Other Useful Commands

| Command   | Description                           | Memory aid      |
| --------- | ------------------------------------- | --------------- |
| `echo`    | Prints text/variables                 | Echo            |
| `env`     | Shows environment variables           | **Env**ironment |
| `export`  | Creates/exports environment variables | Literal         |
| `alias`   | Creates command shortcuts             | Literal         |
| `history` | Shows command history                 | Literal         |
| `man`     | Opens the manual for a command        | **Man**ual      |
| `help`    | Help for shell built-ins              | Literal         |
| `source`  | Executes a file in the current shell  | Literal         |
| `strings` | Extracts readable strings from a file | Literal         |
| `xxd`     | Displays binary data in hexadecimal   | Hex dump        |
| `base64`  | Encodes/decodes Base64                | Literal         |
| `sleep`   | Pauses execution                      | Literal         |
| `exit`    | Exits the shell                       | Literal         |

---

# ⭐ Essential Commands for HTB

The commands below are particularly useful when working on Hack The Box machines and Linux-based cybersecurity labs.

```text
pwd
ls
cd
mkdir
touch
cp
mv
rm

cat
less
head
tail

find
grep
which
file

whoami
id
sudo
su
chmod
chown

ps
top
kill

ip
ping
ss
curl
wget
ssh
scp
nc

tar
df
du

uname
hostname
env
history

apt
nano
vim
man
```

## 🔥 Essential shell operators

```text
|
>
>>
2>
2>&1
&&
||
;
&
```

---

# 🧠 Quick Mental Map

```text
NAVIGATION
pwd · ls · cd

FILES
touch · mkdir · cp · mv · rm

READ
cat · less · head · tail

SEARCH
find · grep · which · file

USERS
whoami · id · sudo · su

PERMISSIONS
chmod · chown · chgrp

PROCESSES
ps · top · kill

NETWORK
ip · ping · ss · curl · wget · ssh · nc

DISK
df · du · lsblk · mount

SYSTEM
uname · hostname · uptime · free

PACKAGES
apt · dpkg

HELP
man · help · history

SHELL
| · > · >> · && · || · &
```

> **Linux is not about memorising every command.**
>
> Learn what each command does, then learn how to combine them.
>
> `find` + `grep` + pipes + redirection will take you much further than memorising a huge list of commands.
