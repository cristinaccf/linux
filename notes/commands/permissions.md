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

Allow
