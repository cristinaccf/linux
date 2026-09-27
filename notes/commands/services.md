# ⚙️ Linux Services

> `systemctl` is used to manage and inspect services controlled by `systemd`.

---

## 📌 What is `systemctl`?

`systemctl` is the main command used to interact with **systemd**, the service manager used by many modern Linux distributions.

Services are programs that run in the background and provide functionality to the system, such as:

* 🔐 `ssh` → Remote access
* 🌐 `apache2` → Web server
* 🌐 `nginx` → Web server
* 🗄️ `mysql` → Database server
* ⏰ `cron` → Scheduled tasks
* 🌐 `NetworkManager` → Network management

---

## 🔎 Checking services

### Check the status

```bash
systemctl status <service>
```

For example:

```bash
systemctl status ssh
```

This shows whether the service is running, stopped, or has failed.

Useful states:

```text
active (running)   → Service is running
inactive (dead)    → Service is stopped
failed             → Service failed to start
```

---

## ▶️ Starting & stopping

### Start a service

```bash
sudo systemctl start <service>
```

Starts the service **immediately**.

### Stop a service

```bash
sudo systemctl stop <service>
```

Stops the service **immediately**.

### Restart a service

```bash
sudo systemctl restart <service>
```

Stops and starts the service again.

💡 Useful after changing a service's configuration.

### Reload configuration

```bash
sudo systemctl reload <service>
```

Reloads the configuration without completely restarting the service, if supported.

---

## 🚀 Starting services automatically

There is an important difference between **starting** a service and **enabling** it.

### Enable

```bash
sudo systemctl enable <service>
```

Makes the service start automatically when Linux boots.

> ⚠️ `enable` does **not** start the service immediately.

### Disable

```bash
sudo systemctl disable <service>
```

Prevents the service from starting automatically at boot.

> ⚠️ `disable` does **not necessarily** stop a service that is already running.

### Enable + start

```bash
sudo systemctl enable --now <service>
```

Enables the service at boot **and** starts it immediately.

For example:

```bash
sudo systemctl enable --now ssh
```

### Disable + stop

```bash
sudo systemctl disable --now <service>
```

Disables automatic startup **and** stops the service immediately.

---

## 📋 Listing services

### Running services

```bash
systemctl list-units --type=service --state=running
```

Shows currently running services.

### All loaded services

```bash
systemctl list-units --type=service
```

Shows the service units currently loaded by `systemd`.

---

## 🧠 Quick reference

| Command                             | What it does                   |
| ----------------------------------- | ------------------------------ |
| `systemctl status <service>`        | 🔎 Check status                |
| `systemctl start <service>`         | ▶️ Start                       |
| `systemctl stop <service>`          | ⏹️ Stop                        |
| `systemctl restart <service>`       | 🔄 Restart                     |
| `systemctl reload <service>`        | ♻️ Reload configuration        |
| `systemctl enable <service>`        | 🚀 Start automatically at boot |
| `systemctl disable <service>`       | 🚫 Disable automatic startup   |
| `systemctl enable --now <service>`  | 🚀 Enable + start              |
| `systemctl disable --now <service>` | 🚫 Disable + stop              |

---

## 🧪 Example

Check whether SSH is running:

```bash
systemctl status ssh
```

If it is stopped, start it:

```bash
sudo systemctl start ssh
```

If you also want SSH to start automatically when the machine boots:

```bash
sudo systemctl enable ssh
```

Or do both at once:

```bash
sudo systemctl enable --now ssh
```

---

### 🔗 Related commands

* `service` → Another way to manage services
* `journalctl` → View service and system logs
* `ps` → View running processes
* `ss` → View network connections and listening ports
