# 📁 Linux Filesystem

> Commands for navigating, creating, modifying and searching files and directories.

---

## 📍 Navigation

### `pwd`

Shows the **current working directory**.

```bash
pwd
```

Example:

```text
/home/user
```

---

### `ls`

Lists files and directories in the current location.

```bash
ls
```

Useful options:

```bash
ls -l       # Detailed information
ls -a       # Include hidden files
ls -la      # Detailed information + hidden files
ls -lh      # Human-readable file sizes
```

💡 `ls -la` is one of the most useful combinations to remember.

---

### `cd`

Changes the current directory.

```bash
cd <directory>
```

Examples:

```bash
cd /etc
cd Documents
```

Go to the parent directory:

```bash
cd ..
```

Go to the home directory:

```bash
cd ~
```

Go to the previous directory:

```bash
cd -
```

---

## 📂 Creating files & directories

### `mkdir`

Creates a directory.

```bash
mkdir <directory>
```

Example:

```bash
mkdir projects
```

Create nested directories:

```bash
mkdir -p projects/linux/notes
```

---

### `touch`

Creates an empty file if it doesn't exist.

```bash
touch <file>
```

Example:

```bash
touch notes.txt
```

It can also update the file's timestamps if the file already exists.

---

## 📄 Copying & moving

### `cp`

Copies files or directories.

Copy a file:

```bash
cp <source> <destination>
```

Example:

```bash
cp notes.txt backup.txt
```

Copy a directory:

```bash
cp -r <directory> <destination>
```

Example:

```bash
cp -r notes/ backup/
```

💡 `-r` means **recursive**, allowing directories and their contents to be copied.

---

### `mv`

Moves or renames files and directories.

Move a file:

```bash
mv notes.txt Documents/
```

Rename a file:

```bash
mv old.txt new.txt
```

Rename a directory:

```bash
mv old_folder new_folder
```

---

## 🗑️ Removing files & directories

### `rm`

Removes files.

```bash
rm <file>
```

Example:

```bash
rm notes.txt
```

Remove a directory and its contents:

```bash
rm -r <directory>
```

Force removal:

```bash
rm -f <file>
```

Force removal of a directory and its contents:

```bash
rm -rf <directory>
```

> ⚠️ `rm` permanently removes files. There is no normal recycle bin to rescue you afterwards. 🫠

Be especially careful with:

```bash
rm -rf
```

---

## 📖 Viewing files

### `cat`

Displays the contents of a file.

```bash
cat <file>
```

Example:

```bash
cat /etc/hosts
```

---

### `less`

Displays a file one page at a time.

```bash
less <file>
```

Useful for large files.

Navigation:

```text
Space   → Next page
b       → Previous page
q       → Quit
```

---

### `head`

Shows the beginning of a file.

```bash
head <file>
```

Show the first 20 lines:

```bash
head -n 20 <file>
```

---

### `tail`

Shows the end of a file.

```bash
tail <file>
```

Show the last 20 lines:

```bash
tail -n 20 <file>
```

Follow a file as it changes:

```bash
tail -f <file>
```

💡 `tail -f` is especially useful for watching log files in real time.

---

## 🔍 Finding files

### `find`

Searches for files and directories.

Basic syntax:

```bash
find <path> <criteria>
```

Find a file by name:

```bash
find / -name "config.txt"
```

Case-insensitive search:

```bash
find / -iname "config.txt"
```

Find directories:

```bash
find / -type d -name "backup"
```

Find files:

```bash
find / -type f -name "*.txt"
```

💡 On a real system, searching from `/` may produce permission errors. You can redirect them:

```bash
find / -name "config.txt" 2>/dev/null
```

---

## 🔗 Useful filesystem commands

### `file`

Identifies the type of a file.

```bash
file <file>
```

Example:

```bash
file image.jpg
```

This is useful when a file extension doesn't tell you what the file actually contains.

---

### `du`

Shows how much disk space files and directories use.

```bash
du <directory>
```

Human-readable format:

```bash
du -h <directory>
```

Show the total:

```bash
du -sh <directory>
```

---

### `df`

Shows available and used disk space on mounted filesystems.

```bash
df -h
```

💡 `df` looks at **filesystem/disk usage**, while `du` looks at **space used by files and directories**.

---

## 🧠 Quick reference

| Command | What it does                      |
| ------- | --------------------------------- |
| `pwd`   | 📍 Show current directory         |
| `ls`    | 📋 List files                     |
| `cd`    | 🚶 Change directory               |
| `mkdir` | 📁 Create directory               |
| `touch` | 📄 Create empty file              |
| `cp`    | 📑 Copy files/directories         |
| `mv`    | 🔀 Move or rename                 |
| `rm`    | 🗑️ Remove files/directories      |
| `cat`   | 📖 Display file contents          |
| `less`  | 📖 Read file page by page         |
| `head`  | ⬆️ Show beginning of file         |
| `tail`  | ⬇️ Show end of file               |
| `find`  | 🔎 Search for files               |
| `file`  | 🏷️ Identify file type            |
| `du`    | 💾 Show directory/file disk usage |
| `df`    | 💽 Show filesystem disk usage     |

---

## 🧪 Example workflow

Create a directory and a file:

```bash
mkdir project
cd project
touch notes.txt
```

Write something to the file:

```bash
echo "Linux notes" > notes.txt
```

Read it:

```bash
cat notes.txt
```

Create a backup:

```bash
cp notes.txt backup.txt
```

Check the files:

```bash
ls -la
```

Rename the backup:

```bash
mv backup.txt notes_backup.txt
```

Remove it:

```bash
rm notes_backup.txt
```

---

### 🔗 Related topics

* `permissions.md` → File permissions and ownership
* `processes.md` → Running processes
* `services.md` → System services
* `networking.md` → Network-related commands
