# 🐚 Linux Shell

> The shell is a command-line interface that allows you to interact with the operating system by executing commands and programs.

Kali Linux commonly uses **Bash** as its default shell.

---

## 🧩 What is a shell?

The shell interprets the commands you type and executes them.

For example:

```bash id="k3x8m1"
ls
```

The shell finds the `ls` program and executes it.

Common shells include:

```text id="v7q2n5"
bash
zsh
sh
fish
```

Check your current shell:

```bash id="j4m9r6"
echo $SHELL
```

Check the shell of the current process:

```bash id="c6p1x8"
ps -p $$ 
```

---

# 📍 Basic commands

### `echo`

Prints text or variable values to the terminal.

```bash id="w8q3m5"
echo "Hello"
```

It can also display variables:

```bash id="s2k7v9"
echo $USER
```

```bash id="h5r1x4"
echo $HOME
```

---

### `clear`

Clears the terminal screen.

```bash id="p9m4c2"
clear
```

Shortcut:

```text id="k3v7n1"
Ctrl + L
```

---

### `history`

Shows previously executed commands.

```bash id="z6q2w8"
history
```

Search through command history:

```bash id="m1x8r4"
history | grep ssh
```

Run a command from history:

```bash id="q5n3v7"
!123
```

where `123` is the history entry number.

---

# 🔎 Finding commands

### `which`

Shows the path of an executable.

```bash id="f8k2m6"
which <command>
```

Example:

```bash id="w4p7x1"
which nmap
```

Possible output:

```text id="e3n9q5"
/usr/bin/nmap
```

---

### `whereis`

Searches for the binary, source and manual pages associated with a command.

```bash id="c7m2v8"
whereis <command>
```

Example:

```bash id="n5q1r6"
whereis bash
```

---

### `type`

Shows how the shell interprets a command.

```bash id="y8v3k4"
type <command>
```

Example:

```bash id="p2m6x9"
type cd
```

You may see:

```text id="r4w7n1"
cd is a shell builtin
```

This is useful because not every command is an external program. Some are built directly into the shell.

---

# 🌱 Environment variables

Environment variables store information that programs can use.

View a variable:

```bash id="x6q3m8"
echo $VARIABLE
```

Some important variables:

```bash id="j9v2k5"
echo $USER
echo $HOME
echo $SHELL
echo $PATH
```

---

## 📌 Important variables

| Variable  | Meaning                              |
| --------- | ------------------------------------ |
| `$USER`   | 👤 Current username                  |
| `$HOME`   | 🏠 User's home directory             |
| `$SHELL`  | 🐚 Default shell                     |
| `$PATH`   | 📍 Directories searched for commands |
| `$PWD`    | 📂 Current working directory         |
| `$OLDPWD` | ↩️ Previous working directory        |

Example:

```bash id="q7m4x2"
echo $PWD
```

---

# 🛣️ `$PATH`

`$PATH` contains the directories where the shell looks for executable commands.

View it:

```bash id="n8c3v6"
echo $PATH
```

Example:

```text id="k2r9m5"
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

The directories are separated by `:`.

When you type:

```bash id="w4x7p1"
nmap
```

the shell searches the directories in `$PATH` until it finds the executable.

This is why:

```bash id="j6q2v8"
which nmap
```

might return:

```text id="m9r3c5"
/usr/bin/nmap
```

---

# ➡️ Command output redirection

The shell allows command output to be redirected to files.

### `>`

Writes output to a file.

```bash id="p4x8m1"
echo "Hello" > file.txt
```

If the file already exists, its contents are **overwritten**.

---

### `>>`

Appends output to a file.

```bash id="v7q2n5"
echo "Another line" >> file.txt
```

The existing contents are preserved.

---

### `<`

Uses a file as input for a command.

```bash id="k5m9r3"
command < file.txt
```

---

## ⚠️ `>` vs `>>`

```text id="x8c4v2"
>   → Overwrite
>>  → Append
```

This distinction is very important.

---

# 🔗 Pipes

### `|`

A pipe sends the output of one command directly into another command.

```bash id="m3q7x9"
command1 | command2
```

Example:

```bash id="n6v2k8"
ps aux | grep ssh
```

Here:

```text id="s1r5c7"
ps aux
   ↓
output
   ↓
grep ssh
   ↓
only lines containing "ssh"
```

Pipes can be chained:

```bash id="q8m4x2"
cat file.txt | grep admin | sort
```

💡 This is one of the most powerful ideas in the Linux command line: small commands can be combined to perform more complex tasks.

---

# 🔀 Command operators

### `;`

Runs commands sequentially regardless of whether the previous command succeeds.

```bash id="v5n9r1"
command1 ; command2
```

Example:

```bash id="c7x2m8"
echo "Hello" ; echo "World"
```

---

### `&&`

Runs the second command **only if the first succeeds**.

```bash id="m4q8v3"
command1 && command2
```

Example:

```bash id="p6r1x9"
mkdir test && cd test
```

---

### `||`

Runs the second command **only if the first fails**.

```bash id="z3m7c5"
command1 || command2
```

Example:

```bash id="w8x2n6"
ping -c 1 192.168.1.1 || echo "Host unreachable"
```

---

## 🧠 Operators at a glance

```text id="j4v9m2"
;    → Run both
&&   → Run second if first succeeds
||   → Run second if first fails
|    → Send output to another command
```

---

# 📤 Standard input, output and errors

Linux programs normally use three standard streams:

```text id="x6r1q8"
stdin   (0) → Input
stdout  (1) → Normal output
stderr  (2) → Error output
```

---

### Redirect standard output

```bash id="m9c3v7"
command > output.txt
```

---

### Redirect errors

```bash id="k2x8n5"
command 2> errors.txt
```

---

### Redirect both output and errors

```bash id="q7m4r1"
command > output.txt 2>&1
```

A common shortcut in Bash:

```bash id="v5n9c2"
command &> output.txt
```

---

### Discard output

Linux has a special device:

```text id="n3x7m8"
/dev/null
```

Anything sent there is discarded.

For example:

```bash id="r6q2p4"
command > /dev/null
```

Discard errors:

```bash id="t8m1x5"
command 2> /dev/null
```

Discard both:

```bash id="c4v9k7"
command > /dev/null 2>&1
```

💡 You'll see `/dev/null` **all the time** in Linux and HTB.

---

# 🔐 Command substitution

The shell can use the output of one command as part of another command.

```bash id="p8x3m6"
$(command)
```

Example:

```bash id="w5q1r9"
echo "Current user: $(whoami)"
```

Output:

```text id="j7c2v4"
Current user: kali
```

Another example:

```bash id="n6m8x2"
cd $(dirname /home/kali/file.txt)
```

---

# 📝 Aliases

An alias creates a shortcut for a command.

Create one:

```bash id="q3v7m1"
alias ll='ls -la'
```

Now:

```bash id="x8c4r5"
ll
```

runs:

```bash id="m2k9v6"
ls -la
```

View existing aliases:

```bash id="f7n3x8"
alias
```

💡 Aliases created this way normally disappear when the shell session ends unless they are added to a shell configuration file such as `~/.bashrc`.

---

# 🧪 Useful shell combinations

Search running processes:

```bash id="v4m8q2"
ps aux | grep ssh
```

Search files while hiding permission errors:

```bash id="j9x3c6"
find / -name "*.conf" 2>/dev/null
```

Update packages only if the package list update succeeds:

```bash id="n5r7m1"
sudo apt update && sudo apt upgrade
```

Save command output to a file:

```bash id="c8q2v9"
ip a > network.txt
```

Append another command's output:

```bash id="m4x6p3"
ip r >> network.txt
```

---

## 🧠 Quick reference

| Command / operator | What it does                           |
| ------------------ | -------------------------------------- |
| `echo`             | 📢 Print text or variables             |
| `history`          | 📜 Show command history                |
| `which`            | 📍 Show executable path                |
| `whereis`          | 🔎 Find binary/source/man pages        |
| `type`             | 🧩 Show how shell interprets a command |
| `$VARIABLE`        | 🌱 Access environment variable         |
| `$PATH`            | 🛣️ Command search path                |
| `>`                | 📤 Redirect output, overwrite          |
| `>>`               | 📤 Redirect output, append             |
| `<`                | 📥 Redirect input                      |
| `\|`               | 🔗 Pipe output into another command    |
| `;`                | ➡️ Run commands sequentially           |
| `&&`               | ✅ Run if previous succeeds             |
| `\|\|`             | ❌ Run if previous fails                |
| `2>`               | ⚠️ Redirect errors                     |
| `/dev/null`        | 🗑️ Discard output                     |
| `$(...)`           | 🔄 Command substitution                |
| `alias`            | ⚡ Create command shortcuts             |

---

## ⚡ The most important things to remember

```text id="k3v7m9"
command1 | command2
    → Pipe output

command1 > file
    → Write output

command1 >> file
    → Append output

command1 2>/dev/null
    → Hide errors

command1 && command2
    → Run second if first succeeds

command1 || command2
    → Run second if first fails

$(command)
    → Use command output as a value
```

---

### 🔗 Related topics

* `filesystem.md` → Files and directories
* `networking.md` → Network commands
* `processes.md` → Running processes
* `permissions.md` → Permissions and ownership
