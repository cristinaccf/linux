# ⚙️ Linux Processes

> A process is a running instance of a program. Linux assigns each process a unique **PID** (Process ID).

---

## 🧩 Processes & PIDs

Every running process has a unique **PID**.

For example:

```text id="8qf2mx"
PID    COMMAND
1      systemd
842    sshd
1250   bash
```

The process with **PID 1** is normally `systemd`, which is responsible for starting and managing many system services.

---

## 🔎 Viewing processes

### `ps`

Displays information about running processes.

Basic:

```bash id="8k4n2c"
ps
```

Show processes for all users:

```bash id="m7v5p1"
ps aux
```

A very common command:

```bash id="j3r8w6"
ps aux
```

Useful columns include:

```text
USER   → Process owner
PID    → Process ID
%CPU   → CPU usage
%MEM   → Memory usage
STAT   → Process state
COMMAND → Command that started the process
```

---

### `ps -ef`

Another common way to display all running processes:

```bash id="q5x9k2"
ps -ef
```

This format includes the **PPID**, the Parent Process ID.

```text
PID   → Process ID
PPID  → Parent Process ID
```

💡 The parent process is the process that started another process.

---

## 🎯 Finding a process

### `pgrep`

Searches for processes by name.

```bash id="n4w8s2"
pgrep <process>
```

Example:

```bash id="y6r1v9"
pgrep ssh
```

Show the process name together with its PID:

```bash id="c8m3q7"
pgrep -a ssh
```

---

### `pidof`

Returns the PID of a running program.

```bash id="t2k7x5"
pidof <program>
```

Example:

```bash id="f9v4m1"
pidof sshd
```

---

## 📊 Monitoring processes

### `top`

Displays processes in real time.

```bash id="z5q8n3"
top
```

Useful information includes:

* CPU usage
* Memory usage
* Process IDs
* Running processes
* System load

Press:

```text id="k6m1p4"
q → Quit
```

---

### `htop`

An interactive alternative to `top`.

```bash id="r3x7v8"
htop
```

It is usually easier to read and navigate.

> 💡 `htop` may need to be installed separately on some systems.

---

## 🛑 Stopping processes

### `kill`

Sends a signal to a process.

```bash id="p8c2m6"
kill <PID>
```

Example:

```bash id="x4v9k1"
kill 1234
```

By default, `kill` sends `SIGTERM`, asking the process to terminate gracefully.

---

### Force a process to stop

```bash id="b7n5q2"
kill -9 <PID>
```

`-9` sends `SIGKILL`, which immediately terminates the process.

> ⚠️ Use `kill -9` only when necessary. It doesn't give the process an opportunity to clean up properly.

---

### `pkill`

Kills processes based on their name.

```bash id="m2r6x8"
pkill <process>
```

Example:

```bash id="w5k9c3"
pkill firefox
```

⚠️ Be careful with `pkill`, especially when running it as root.

---

## 🔢 Useful signals

Linux processes can receive different signals.

| Signal    | Number | Purpose                         |
| --------- | -----: | ------------------------------- |
| `SIGTERM` |   `15` | 🛑 Request graceful termination |
| `SIGKILL` |    `9` | 💀 Force termination            |
| `SIGSTOP` |   `19` | ⏸️ Stop a process               |
| `SIGCONT` |   `18` | ▶️ Continue a stopped process   |

Send a specific signal:

```bash id="x3q8m7"
kill -<signal> <PID>
```

Example:

```bash id="j6v2n9"
kill -15 1234
```

---

# 🏃 Background & foreground processes

A command normally runs in the **foreground**, meaning your terminal waits for it to finish.

Run a command in the background by adding `&`:

```bash id="c5m8r2"
command &
```

Example:

```bash id="v7n3q9"
sleep 60 &
```

The terminal remains available while the command runs in the background.

---

### `jobs`

Shows jobs running in the current shell.

```bash id="s4k1x8"
jobs
```

---

### `fg`

Brings a background job to the foreground.

```bash id="n9p3v6"
fg
```

Or specify a job:

```bash id="h2m7c5"
fg %1
```

---

### `bg`

Continues a stopped job in the background.

```bash id="q8x4r1"
bg
```

---

### `Ctrl + Z`

Suspends the current foreground process.

```text id="e6v2k9"
Ctrl + Z
```

The process is stopped rather than terminated.

You can then use:

```bash id="w1m5s7"
bg
```

to continue it in the background.

---

## 🌳 Process hierarchy

Processes can have parent and child processes.

You can view the hierarchy with:

```bash id="r4n8c2"
pstree
```

Example:

```text id="u7x3m1"
systemd
├── sshd
│   └── bash
└── NetworkManager
```

Show PIDs:

```bash id="k9q5v4"
pstree -p
```

💡 Understanding parent/child relationships can be useful when investigating a Linux system.

---

# 📂 `/proc`

Linux exposes information about running processes through the `/proc` virtual filesystem.

Each process has a directory named after its PID:

```text id="p2x7m5"
/proc/<PID>/
```

For example:

```bash id="c8v1n6"
ls /proc/1234
```

Some useful files:

```text id="z4m9q2"
/proc/<PID>/cmdline
/proc/<PID>/status
/proc/<PID>/exe
/proc/<PID>/cwd
```

View the command used to start a process:

```bash id="y5r8k3"
cat /proc/<PID>/cmdline
```

Check its status:

```bash id="n7q2v6"
cat /proc/<PID>/status
```

Find the executable:

```bash id="m3x9c1"
readlink /proc/<PID>/exe
```

Find the process's current working directory:

```bash id="t6k4p8"
readlink /proc/<PID>/cwd
```

💡 `/proc` is a **virtual filesystem**. The information is generated by the kernel rather than stored as normal files on disk.

---

# 🔍 Processes in HTB

When investigating a Linux machine, checking running processes can reveal:

* Services running in the background
* Programs running as `root`
* Unusual processes
* Scripts being executed
* Parent/child relationships
* Applications that may expose useful information

A quick overview:

```bash id="q3v8m6"
ps aux
```

Search for a specific process:

```bash id="f7k2n5"
pgrep -a <process>
```

Check processes in real time:

```bash id="x1m9r4"
top
```

Check the process tree:

```bash id="c6p3w8"
pstree -p
```

---

## 🧠 Quick reference

| Command       | What it does                              |
| ------------- | ----------------------------------------- |
| `ps aux`      | 📋 List all running processes             |
| `ps -ef`      | 📋 List processes with parent information |
| `pgrep`       | 🔎 Find processes by name                 |
| `pidof`       | 🔢 Find a program's PID                   |
| `top`         | 📊 Monitor processes in real time         |
| `htop`        | 📊 Interactive process monitor            |
| `kill`        | 🛑 Send a signal to a process             |
| `pkill`       | 🛑 Kill processes by name                 |
| `jobs`        | 📋 Show shell jobs                        |
| `fg`          | ⬆️ Bring job to foreground                |
| `bg`          | ⬇️ Continue job in background             |
| `pstree`      | 🌳 Show process hierarchy                 |
| `/proc/<PID>` | 🔍 Process information                    |

---

## 🧪 Example workflow

List running processes:

```bash id="s8n4k2"
ps aux
```

Find SSH processes:

```bash id="j5x1q7"
pgrep -a ssh
```

Get a process's information:

```bash id="v3m9c6"
cat /proc/<PID>/status
```

Check its executable:

```bash id="k2r7p5"
readlink /proc/<PID>/exe
```

Monitor processes:

```bash id="m6q8x1"
top
```

---

### 🔗 Related topics

* `services.md` → System services
* `users.md` → Users and groups
* `permissions.md` → Permissions and ownership
* `filesystem.md` → Files and directories
