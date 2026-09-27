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
