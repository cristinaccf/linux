# 📦 Linux Package Management

> Package managers are used to install, update, remove and manage software on Linux.

Kali Linux is based on **Debian**, so it primarily uses `apt` and `dpkg` for package management.

---

## 🧩 `apt` vs `dpkg`

There are two commands you will commonly encounter:

* `apt` → High-level package manager. Handles dependencies and repositories.
* `dpkg` → Low-level package management tool for `.deb` packages.

In everyday use, `apt` is usually the first choice.

---

# 📋 Updating package information

### `apt update`

Downloads the latest information about available packages from configured repositories.

```bash
sudo apt update
```

💡 This **does not update the installed software**. It only refreshes the package lists.

Think:

```text
apt update
    ↓
"What's available?"
```

---

# ⬆️ Updating installed packages

### `apt upgrade`

Updates installed packages to newer versions when possible.

```bash
sudo apt upgrade
```

You can combine both steps:

```bash
sudo apt update && sudo apt upgrade
```

This means:

```text
1. Refresh package information
2. If successful → upgrade packages
```

---

## 🚀 Installing packages

### `apt install`

Installs a package and its required dependencies.

```bash
sudo apt install <package>
```

Example:

```bash
sudo apt install nmap
```

Install several packages at once:

```bash
sudo apt install nmap wireshark gobuster
```

---

## 🔍 Searching for packages

### `apt search`

Searches for packages available through the configured repositories.

```bash
apt search <term>
```

Example:

```bash
apt search nmap
```

You can also search for a general concept:

```bash
apt search network scanner
```

---

## ℹ️ Package information

### `apt show`

Displays information about a package.

```bash
apt show <package>
```

Example:

```bash
apt show nmap
```

It can show information such as:

* Package version
* Description
* Dependencies
* Package size
* Repository

---

# 🗑️ Removing packages

### `apt remove`

Removes the package but normally keeps its configuration files.

```bash
sudo apt remove <package>
```

Example:

```bash
sudo apt remove nmap
```

---

### `apt purge`

Removes the package **and its configuration files**.

```bash
sudo apt purge <package>
```

Example:

```bash
sudo apt purge nmap
```

💡 Difference:

```text
remove → Package removed, configuration may remain
purge  → Package + configuration removed
```

---

## 🧹 Cleaning unused packages

### `apt autoremove`

Removes packages that were installed as dependencies but are no longer required.

```bash
sudo apt autoremove
```

This can help keep the system clean.

---

# 📦 `dpkg`

`dpkg` is the lower-level package management system used by Debian-based distributions.

---

## 📋 List installed packages

```bash
dpkg -l
```

Search installed packages:

```bash
dpkg -l | grep <package>
```

Example:

```bash
dpkg -l | grep nmap
```

---

## 🔎 Check whether a package is installed

```bash
dpkg -s <package>
```

Example:

```bash
dpkg -s nmap
```

---

## 📄 List files installed by a package

```bash
dpkg -L <package>
```

Example:

```bash
dpkg -L nmap
```

This can be useful when you want to know where a package installed its files.

---

# 📥 Installing `.deb` packages

If you have a local `.deb` package:

```bash
sudo dpkg -i <package>.deb
```

Example:

```bash
sudo dpkg -i package.deb
```

If there are missing dependencies, you can usually fix them with:

```bash
sudo apt --fix-broken install
```

💡 When possible, installing packages through `apt` is generally easier because it can handle dependencies automatically.

---

# 🧹 Cleaning package files

### `apt clean`

Removes downloaded package files from the local package cache.

```bash
sudo apt clean
```

### `apt autoclean`

Removes package files that can no longer be downloaded or are no longer useful.

```bash
sudo apt autoclean
```

---

# 🔄 Common workflow

Before installing software:

```bash
sudo apt update
```

Install a package:

```bash
sudo apt install <package>
```

Check its information:

```bash
apt show <package>
```

Check whether it is installed:

```bash
dpkg -s <package>
```

Remove it when no longer needed:

```bash
sudo apt remove <package>
```

---

## 🧠 Quick reference

| Command          | What it does                         |
| ---------------- | ------------------------------------ |
| `apt update`     | 🔄 Update package lists              |
| `apt upgrade`    | ⬆️ Upgrade installed packages        |
| `apt install`    | 📥 Install a package                 |
| `apt remove`     | 🗑️ Remove a package                 |
| `apt purge`      | 🧹 Remove package + configuration    |
| `apt autoremove` | 🧹 Remove unused dependencies        |
| `apt search`     | 🔎 Search for packages               |
| `apt show`       | ℹ️ Show package information          |
| `apt clean`      | 🧹 Clear package cache               |
| `dpkg -l`        | 📋 List installed packages           |
| `dpkg -s`        | 🔎 Show package status               |
| `dpkg -L`        | 📂 List files installed by a package |
| `dpkg -i`        | 📦 Install a `.deb` package          |

---

## ⚡ Useful combinations

Update package information and upgrade the system:

```bash
sudo apt update && sudo apt upgrade
```

Search installed packages:

```bash
dpkg -l | grep <package>
```

Install several packages:

```bash
sudo apt install <package1> <package2> <package3>
```

Remove a package and unused dependencies:

```bash
sudo apt remove <package>
sudo apt autoremove
```

---

### 🔗 Related topics

* `filesystem.md` → Files and directories
* `permissions.md` → Permissions and ownership
* `services.md` → System services
* `users.md` → Users and groups
