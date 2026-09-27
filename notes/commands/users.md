# 👤 Linux Users & Groups

> Linux uses users and groups to control access to files, processes and system resources.

---

## 🧩 Users and Groups

Every Linux user has:

* 👤 A **username**
* 🔢 A **UID** (User ID)
* 👥 One or more **groups**
* 🔢 A **GID** (Group ID)
* 🏠 A **home directory**
* 🐚 A **default shell**

Linux also has system users that are used by services and applications rather than by people.

---

## 🔎 Identifying the current user

### `whoami`

Displays the username of the current user.

```bash id="n7l7v3"
whoami
```

Example:

```text id="v2e6st"
kali
```

---

### `id`

Displays the current user's UID, GID and group memberships.

```bash id="w7k8ob"
id
```

Example:

```text id="q5s8r4"
uid=1000(kali) gid=1000(kali) groups=1000(kali),27(sudo)
```

This tells us:

```text id="2y5u0j"
uid=1000(kali)  → User ID
gid=1000(kali)  → Primary group
groups=...      → Groups the user belongs to
```

Check another user:

```bash id="4i1o0r"
id <username>
```

---

## 👥 Groups

### `groups`

Shows the groups the current user belongs to.

```bash id="5w7y4v"
groups
```

Check another user:

```bash id="sq8w6c"
groups <username>
```

---

### `getent group`

Displays information about groups configured on the system.

```bash id="e6q3v1"
getent group
```

Check a specific group:

```bash id="q3h8ls"
getent group sudo
```

---

# 📂 Important user files

Linux stores local user and group information in several files.

### `/etc/passwd`

Contains information about local user accounts.

View it with:

```bash id="tqv1r9"
cat /etc/passwd
```

A typical entry looks like:

```text id="t7q2zy"
kali:x:1000:1000:Kali User:/home/kali:/bin/bash
```

The fields are separated by `:`:

```text id="q2z6jg"
username
password placeholder
UID
GID
description
home directory
login shell
```

For example:

```text id="m6gq0v"
kali
 ↓
x
 ↓
1000
 ↓
1000
 ↓
Kali User
 ↓
/home/kali
 ↓
/bin/bash
```

💡 The `x` normally means that the password hash is stored elsewhere, usually in `/etc/shadow`.

---

### `/etc/shadow`

Contains password hashes and password-related information.

```bash id="j9r1p7"
sudo cat /etc/shadow
```

Access to this file is normally restricted to privileged users.

A line may look like:

```text id="e3j1n8"
username:$6$...:...
```

🔐 Password hashes are stored here rather than directly in `/etc/passwd`.

---

### `/etc/group`

Contains information about groups.

```bash id="g7r4y2"
cat /etc/group
```

Example:

```text id="q0s4i6"
sudo:x:27:kali
```

This indicates that:

```text id="m8v2k3"
Group → sudo
GID   → 27
Member → kali
```

---

### `/etc/shells`

Lists shells that are considered valid login shells.

```bash id="2t5f8w"
cat /etc/shells
```

Example:

```text id="3k9c5p"
/bin/sh
/bin/bash
/bin/zsh
```

---

# 👤 Managing users

### `useradd`

Creates a new user.

```bash id="h6k1p0"
sudo useradd <username>
```

Create a user with a home directory:

```bash id="5h9v3a"
sudo useradd -m <username>
```

Specify a default shell:

```bash id="9d4m2x"
sudo useradd -m -s /bin/bash <username>
```

---

### `passwd`

Sets or changes a user's password.

Change your own password:

```bash id="q1x5w7"
passwd
```

Change another user's password:

```bash id="p8c2n6"
sudo passwd <username>
```

---

### `usermod`

Modifies an existing user account.

Add a user to a group:

```bash id="r6x0m2"
sudo usermod -aG <group> <username>
```

Example:

```bash id="z7p1k4"
sudo usermod -aG sudo alice
```

💡 `-aG` means **append the user to the supplementary group**.

The `-a` is important. Without it, you may replace the user's existing supplementary groups.

---

### `userdel`

Deletes a user.

```bash id="k5j8s1"
sudo userdel <username>
```

Delete the user and their home directory:

```bash id="c4r9y6"
sudo userdel -r <username>
```

> ⚠️ Be careful with `-r`, as it removes the user's home directory and its contents.

---

# 👥 Managing groups

### `groupadd`

Creates a new group.

```bash id="n3w8q5"
sudo groupadd <group>
```

Example:

```bash id="e8x1v4"
sudo groupadd developers
```

---

### `groupdel`

Deletes a group.

```bash id="u2m6k9"
sudo groupdel <group>
```

---

# 🔄 Switching users

### `su`

Switches to another user.

```bash id="r8k2w5"
su <username>
```

Switch to another user with their login environment:

```bash id="c5n1j7"
su - <username>
```

Switch to root:

```bash id="4x9m2p"
su -
```

This normally requires the target user's password.

---

### `sudo`

Run a command as another user, normally with elevated privileges.

```bash id="y6v3q8"
sudo <command>
```

Example:

```bash id="m4k1s9"
sudo whoami
```

Output:

```text id="5j2q7x"
root
```

Open a root shell:

```bash id="n8c4v6"
sudo -i
```

Check which commands the current user can run with `sudo`:

```bash id="z1r5t7"
sudo -l
```

💡 `sudo -l` is particularly useful when investigating privileges on a Linux machine.

---

# 🔍 Finding users

### List local users

```bash id="p7m3x9"
cat /etc/passwd
```

A simpler approach:

```bash id="w2k6n4"
cut -d: -f1 /etc/passwd
```

This extracts only the usernames.

---

### Find users with a specific UID

For example, users with UID 1000 or higher:

```bash id="h5q8v1"
awk -F: '$3 >= 1000 {print $1}' /etc/passwd
```

💡 On many Linux systems, regular human users commonly have UIDs starting at 1000, while system/service accounts use lower UIDs. This is a convention, not an absolute rule.

---

# 👀 Logged-in users

### `who`

Shows users currently logged in.

```bash id="c9r4m7"
who
```

---

### `w`

Shows logged-in users and what they are doing.

```bash id="k3v8x2"
w
```

---

### `last`

Shows previous login sessions.

```bash id="s6n1p5"
last
```

This can be useful when investigating system activity.

---

# 🧠 UID & GID

Linux identifies users and groups internally using numbers.

Example:

```text id="d8f2m6"
uid=1000(alice)
gid=1000(alice)
```

Here:

```text id="5c9w1x"
UID 1000 → Alice's user ID
GID 1000 → Alice's primary group ID
```

You can see your own IDs with:

```bash id
```

---

## 📌 Important files

| File          | Purpose                                     |
| ------------- | ------------------------------------------- |
| `/etc/passwd` | 👤 User account information                 |
| `/etc/shadow` | 🔐 Password hashes and password information |
| `/etc/group`  | 👥 Group information                        |
| `/etc/shells` | 🐚 Valid login shells                       |

---

## 🧠 Quick reference

| Command    | What it does                       |
| ---------- | ---------------------------------- |
| `whoami`   | 👤 Show current user               |
| `id`       | 🔢 Show UID, GID and groups        |
| `groups`   | 👥 Show group memberships          |
| `who`      | 👀 Show logged-in users            |
| `w`        | 👀 Show logged-in users + activity |
| `last`     | 🕐 Show previous logins            |
| `useradd`  | ➕ Create a user                    |
| `usermod`  | 🔧 Modify a user                   |
| `userdel`  | ❌ Delete a user                    |
| `passwd`   | 🔑 Change a password               |
| `groupadd` | ➕ Create a group                   |
| `groupdel` | ❌ Delete a group                   |
| `su`       | 🔄 Switch user                     |
| `sudo`     | 👑 Execute as another user         |
| `sudo -l`  | 🔎 Show sudo privileges            |

---

## 🧪 Example workflow

Check who you are:

```bash id="y3f7k1"
whoami
```

Check your UID, GID and groups:

```bash id="m8q2v5"
id
```

Check your sudo privileges:

```bash id="x4n9r6"
sudo -l
```

Look at local users:

```bash id="p1c7w3"
cat /etc/passwd
```

Check the groups of a specific user:

```bash id="v6k2s8"
groups <username>
```

---

### 🔗 Related topics

* `permissions.md` → File permissions and ownership
* `filesystem.md` → Files and directories
* `processes.md` → Running processes
* `services.md` → System services
