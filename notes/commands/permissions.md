# 🔐 Linux Permissions

> Linux permissions control who can read, modify and execute files and directories.

---

## 🧩 Understanding permissions

Linux permissions are divided into three categories:

```text
        Owner    Group    Others
          ↓        ↓        ↓
        rwx      rwx      rwx
```

Each permission has a meaning:

| Permission | Symbol | Meaning             |
| ---------- | ------ | ------------------- |
| Read       | `r`    | 📖 Read the file    |
| Write      | `w`    | ✏️ Modify the file  |
| Execute    | `x`    | ▶️ Execute the file |

For example:

```text
-rwxr-xr--
```

Can be broken down as:

```text
-   rwx   r-x   r--
    │     │     │
   Owner Group Others
```

So:

* 👤 Owner → `rwx`
* 👥 Group → `r-x`
* 🌍 Others → `r--`

---

## 🔎 Viewing permissions

### `ls -l`

Displays detailed information about files and directories.

```bash
ls -l
```

Example:

```text
-rwxr-xr-- 1 alice users 1200 Sep 27 script.sh
```

The first part contains the permissions:

```text
-rwxr-xr--
```

The next fields show the owner and group:

```text
alice users
```

---

## 📖 Read, write and execute

### Read `r`

Allows the contents of a file to be read.

```text
r--
```

### Write `w`

Allows the file to be modified.

```text
-w-
```

### Execute `x`

Allows a file to be executed as a program or script.

```text
--x
```

For directories, these permissions have a slightly different meaning:

| Permission | On a file       | On a directory         |
| ---------- | --------------- | ---------------------- |
| `r`        | Read contents   | List contents          |
| `w`        | Modify contents | Create/delete entries  |
| `x`        | Execute         | Enter/access directory |

💡 The `x` permission on a directory is particularly important. Without it, you may not be able to access files inside the directory even if you can read the directory listing.

---

# 🔢 Numeric permissions

Permissions can also be represented using numbers.

```text
r = 4
w = 2
x = 1
```

Add the values together:

```text
rwx = 4 + 2 + 1 = 7
r-x = 4 + 0 + 1 = 5
r-- = 4 + 0 + 0 = 4
```

Therefore:

```text
rwxr-xr--
 ↓   ↓   ↓
 7   5   4
```

The permission is:

```text
754
```

---

## ⭐ Common permission values

| Number | Permissions | Meaning                |
| -----: | ----------- | ---------------------- |
|    `7` | `rwx`       | Read + write + execute |
|    `6` | `rw-`       | Read + write           |
|    `5` | `r-x`       | Read + execute         |
|    `4` | `r--`       | Read only              |
|    `3` | `-wx`       | Write + execute        |
|    `2` | `-w-`       | Write only             |
|    `1` | `--x`       | Execute only           |
|    `0` | `---`       | No permissions         |

---

## 🛠️ `chmod`

`chmod` changes file and directory permissions.

### Numeric mode

```bash
chmod <permissions> <file>
```

Example:

```bash
chmod 755 script.sh
```

This gives:

```text
Owner  → rwx
Group  → r-x
Others → r-x
```

Another common example:

```bash
chmod 644 file.txt
```

Which gives:

```text
Owner  → rw-
Group  → r--
Others → r--
```

---

### Symbolic mode

Permissions can also be changed using symbols.

Add execute permission for the owner:

```bash
chmod u+x script.sh
```

Remove write permission from others:

```bash
chmod o-w file.txt
```

Add read permission for the group:

```bash
chmod g+r file.txt
```

The main symbols are:

```text
u → user/owner
g → group
o → others
a → all
```

Examples:

```bash
chmod u+x script.sh
chmod g+w file.txt
chmod o-r file.txt
chmod a+x script.sh
```

---

## 👑 `chown`

`chown` changes the **owner** of a file or directory.

```bash
sudo chown <user> <file>
```

Example:

```bash
sudo chown alice file.txt
```

Change both owner and group:

```bash
sudo chown alice:users file.txt
```

Change ownership recursively:

```bash
sudo chown -R alice:users project/
```

> ⚠️ `-R` applies the change recursively to everything inside the directory.

---

## 👥 `chgrp`

Changes the group that owns a file or directory.

```bash
sudo chgrp <group> <file>
```

Example:

```bash
sudo chgrp developers project.txt
```

---

# 🧑‍💻 `sudo`

`sudo` allows an authorized user to execute a command with elevated privileges.

Example:

```bash
sudo systemctl restart ssh
```

Or:

```bash
sudo cat /etc/shadow
```

The second command requires elevated privileges because `/etc/shadow` contains sensitive account information.

💡 `sudo` does **not** mean "become root permanently". It normally grants elevated privileges for the specific command being executed.

---

## 🧪 Example

Create a script:

```bash
touch script.sh
```

Check its permissions:

```bash
ls -l script.sh
```

Make it executable:

```bash
chmod +x script.sh
```

Check again:

```bash
ls -l script.sh
```

You should now see an `x` in the permissions.

Run the script:

```bash
./script.sh
```

---

# 🔍 Permissions in HTB

When investigating a Linux machine, permissions can reveal interesting things.

Check a file:

```bash
ls -l <file>
```

Check a directory:

```bash
ls -ld <directory>
```

Find files owned by a specific user:

```bash
find / -user <user> 2>/dev/null
```

Find files with specific permissions:

```bash
find / -perm -4000 2>/dev/null
```

💡 The last command searches for **SUID files**, which can be particularly interesting during Linux privilege escalation.

---

## 🧠 Quick reference

| Command      | What it does                        |
| ------------ | ----------------------------------- |
| `ls -l`      | 🔎 View permissions and ownership   |
| `chmod`      | 🔐 Change permissions               |
| `chown`      | 👤 Change owner                     |
| `chgrp`      | 👥 Change group                     |
| `sudo`       | 👑 Execute with elevated privileges |
| `find -perm` | 🔍 Search by permissions            |
| `find -user` | 🔍 Search by owner                  |

---

## 📌 Permission cheat sheet

```text
r = 4
w = 2
x = 1

7 = rwx
6 = rw-
5 = r-x
4 = r--
3 = -wx
2 = -w-
1 = --x
0 = ---

Common:

755 → rwxr-xr-x
644 → rw-r--r--
700 → rwx------
600 → rw-------
```

---

### 🔗 Related topics

* `filesystem.md` → Files and directories
* `users.md` → Users and groups
* `processes.md` → Running processes
* `services.md` → System services
