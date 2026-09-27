# 🔎 Linux Text Processing

> Linux provides powerful commands for searching, filtering, transforming and analysing text directly from the terminal.

These tools are especially useful when working with **logs, command output, configuration files and enumeration results**.

---

## 🔍 `grep`

Searches for text matching a pattern.

```bash id="v3m8q2"
grep <pattern> <file>
```

Example:

```bash id="x7r1k5"
grep "admin" users.txt
```

### Case-insensitive search

```bash id="n4c9p6"
grep -i "admin" users.txt
```

### Show line numbers

```bash id="m2q8v7"
grep -n "admin" users.txt
```

### Invert the match

Show lines that **do not** contain the pattern:

```bash id="k6x3r9"
grep -v "admin" users.txt
```

### Search recursively

```bash id="p8m4c1"
grep -r "password" /etc/
```

### Useful combination

```bash id="q5v9x2"
ps aux | grep ssh
```

💡 `grep` is one of the most important commands to know for Linux and HTB.

---

# ✂️ `cut`

Extracts specific parts of each line.

For example, given:

```text id="c7m2x8"
alice:x:1000:1000::/home/alice:/bin/bash
bob:x:1001:1001::/home/bob:/bin/zsh
```

Extract the usernames:

```bash id="r4n8v1"
cut -d: -f1 /etc/passwd
```

Here:

```text id="z6q3m9"
-d:   → Use ":" as the delimiter
-f1   → Select field 1
```

Extract the home directories:

```bash id="w2k7p5"
cut -d: -f6 /etc/passwd
```

Extract multiple fields:

```bash id="j9x4c3"
cut -d: -f1,6 /etc/passwd
```

---

# 🔢 `sort`

Sorts lines alphabetically or numerically.

```bash id="m5r8q1"
sort file.txt
```

Numerical sorting:

```bash id="x3v7k2"
sort -n numbers.txt
```

Reverse order:

```bash id="p6c9m4"
sort -r file.txt
```

Sort by a specific field:

```bash id="k8q2v5"
sort -t: -k3 -n /etc/passwd
```

Here:

```text id="r1m6x9"
-t:   → Field delimiter
-k3   → Sort by field 3
-n    → Numerical sorting
```

---

# 🔁 `uniq`

Removes consecutive duplicate lines.

```bash id="v4x8n2"
uniq file.txt
```

Count occurrences:

```bash id="q7m3c5"
uniq -c file.txt
```

💡 `uniq` works on **consecutive** duplicates, so it is often combined with `sort`:

```bash id="n9r2k6"
sort file.txt | uniq
```

Count unique values:

```bash id="c5v8m1"
sort file.txt | uniq -c
```

---

# 📏 `wc`

Counts lines, words and bytes.

```bash id="x2q7m4"
wc file.txt
```

Count lines:

```bash id="k6r9v3"
wc -l file.txt
```

Count words:

```bash id="p4m8x1"
wc -w file.txt
```

Count characters/bytes:

```bash id="j7c2n5"
wc -c file.txt
```

Example:

```bash id="m9v3q6"
cat users.txt | wc -l
```

Counts the number of lines returned by `cat`.

---

# 🔤 `tr`

Translates or removes characters.

Convert lowercase to uppercase:

```bash id="r8x4k2"
echo "hello" | tr 'a-z' 'A-Z'
```

Output:

```text id="v5m1q9"
HELLO
```

Remove a character:

```bash id="c3n7p8"
echo "hello" | tr -d 'l'
```

Output:

```text id="x6q2r4"
heo
```

Replace characters:

```bash id="k9m5v1"
echo "hello world" | tr ' ' '_'
```

Output:

```text id="j2c8x7"
hello_world
```

---

# 🧮 `awk`

`awk` is a powerful tool for processing structured text.

Basic syntax:

```bash id="m7r3q9"
awk '{print $1}' file.txt
```

Example:

```text id="w4x8c2"
alice 1000 admin
bob 1001 users
```

Get the first column:

```bash id="p5n2v6"
awk '{print $1}' users.txt
```

Output:

```text id="j8m4r1"
alice
bob
```

Get the second column:

```bash id="c7x3q9"
awk '{print $2}' users.txt
```

---

## `awk` with a delimiter

For `/etc/passwd`, fields are separated by `:`.

Get usernames:

```bash id="n6v1m8"
awk -F: '{print $1}' /etc/passwd
```

Get usernames and home directories:

```bash id="q3r9x5"
awk -F: '{print $1, $6}' /etc/passwd
```

Find users with UID 1000 or higher:

```bash id="m8c4v2"
awk -F: '$3 >= 1000 {print $1}' /etc/passwd
```

💡 `awk` becomes extremely powerful when you start filtering and processing structured output.

---

# 📝 `sed`

`sed` is a stream editor used to transform text.

Replace the first occurrence on each line:

```bash id="x5m2q8"
sed 's/old/new/' file.txt
```

Replace all occurrences on each line:

```bash id="r7c3v1"
sed 's/old/new/g' file.txt
```

Example:

```bash id="k9n4m6"
echo "hello hello" | sed 's/hello/hi/g'
```

Output:

```text id="p2x8r5"
hi hi
```

Delete lines containing a pattern:

```bash id="v6m1q3"
sed '/password/d' file.txt
```

💡 `sed` is useful when you need to modify or clean text without opening a text editor.

---

# 🔗 Combining commands

The real power comes from combining these tools with pipes.

### Count unique values

```bash id="m3r7x9"
sort file.txt | uniq -c
```

---

### Find users with Bash

```bash id="c8v2k5"
grep "/bin/bash" /etc/passwd
```

---

### Extract usernames

```bash id="q6m1r4"
cut -d: -f1 /etc/passwd
```

Or:

```bash id="x9k3v7"
awk -F: '{print $1}' /etc/passwd
```

---

### Count users

```bash id="n5r8c2"
cut -d: -f1 /etc/passwd | wc -l
```

---

### Find unique shells

```bash id="j4m7x1"
cut -d: -f7 /etc/passwd | sort | uniq
```

---

### Count users by shell

```bash id="p8c3v6"
cut -d: -f7 /etc/passwd | sort | uniq -c
```

---

## 🧪 Useful HTB examples

Search configuration files for passwords:

```bash id="r2x6m9"
grep -Ri "password" /etc/ 2>/dev/null
```

Find lines containing a username:

```bash id="v7k1q4"
grep -Ri "admin" . 2>/dev/null
```

Count results:

```bash id="m5c9x2"
grep -Ri "password" /etc/ 2>/dev/null | wc -l
```

Extract usernames from `/etc/passwd`:

```bash id="q3n8v6"
cut -d: -f1 /etc/passwd
```

Find users with interactive Bash shells:

```bash id="x4m7r1"
grep "/bin/bash" /etc/passwd | cut -d: -f1
```

---

# 🧠 Quick reference

| Command | What it does                   |
| ------- | ------------------------------ |
| `grep`  | 🔎 Search text                 |
| `cut`   | ✂️ Extract fields              |
| `sort`  | 🔢 Sort lines                  |
| `uniq`  | 🔁 Remove/count duplicates     |
| `wc`    | 📏 Count lines/words/bytes     |
| `tr`    | 🔤 Translate/delete characters |
| `awk`   | 🧮 Process structured text     |
| `sed`   | ✏️ Transform text              |

---

## ⚡ Most useful combinations

```text id="s4m8x2"
grep "pattern" file
    → Search for text

cut -d: -f1 file
    → Extract first field

sort file | uniq
    → Get unique values

sort file | uniq -c
    → Count occurrences

grep "pattern" file | wc -l
    → Count matching lines

command | grep "pattern"
    → Filter command output
```

---

### 🔗 Related topics

* `shell.md` → Shell, pipes and redirection
* `filesystem.md` → Files and directories
* `users.md` → Users and groups
* `networking.md` → Network commands
