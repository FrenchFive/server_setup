# 🌐 Setting Up a Linux Server 🚀

A complete guide to set up and customize your Linux server, secure it, and deploy your Python application with Supervisor. 

---

## 📜 Table of Contents

1. [🔧 Initial Setup](#1-initial-setup)
2. [👤 User Management](#2-user-management)
3. [🛡️ Security](#3-security)
4. [🎨 Customization](#4-customization)
5. [🐍 Software Installation](#5-software-installation)
6. [📦 Running a Repository](#6-running-a-repository)
7. [⚙️ Supervisor Configuration](#7-supervisor-configuration)
8. [Monitoring server via command lines](#8-monitoring)
9. [📋 Handy Commands](#8-handy-commands)

---

## 🔧 1. Initial Setup

Connect to your server and update it:
```bash
ssh root@<your-linode-ip-address>
apt update && apt upgrade -y
```

---

## 👤 2. User Management

1. **Add a non-root user**:
   ```bash
   adduser yourusername
   ```
2. **Grant sudo privileges**:
   ```bash
   usermod -aG sudo yourusername
   ```

Switch to the new user:
```bash
su - yourusername
```

---

## 🛡️ 3. Security

### Set Up a Firewall
```bash
apt install ufw
ufw allow OpenSSH
ufw enable
```

### Change SSH Configuration
1. Open the SSH config file:
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```
2. Update these settings:
   - **Port**: Change from `22` to a custom port.
   - **Disable Root Login**: Set `PermitRootLogin no`.
3. Restart SSH:
   ```bash
   sudo systemctl restart ssh
   ```

---

## 🎨 4. Customization

### Install ZSH & Oh My ZSH
```bash
sudo apt update && sudo apt install zsh -y
chsh -s $(which zsh)
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Change Theme & Plugins
1. Edit the ZSH configuration file:
   ```bash
   nano ~/.zshrc
   ```
2. Update:
   - **Theme**: `ZSH_THEME="agnoster"`
   - **Plugins**: `plugins=(git z autojump)`
3. Install Autojump:
   ```bash
   sudo apt install autojump
   ```
4. Apply changes:
   ```bash
   source ~/.zshrc
   ```

---

## 🐍 5. Software Installation

Install Python, Git, and Supervisor:
```bash
apt install python3 python3-pip git supervisor -y
```

---

## 📦 6. Running a Repository

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd <repository-name>
   ```
2. Set up a virtual environment:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   pip install setuptools
   ```
4. Test the application:
   ```bash
   python3 main.py
   ```

---

## ⚙️ 7. Supervisor Configuration

1. Create a Supervisor config file:
   ```bash
   sudo nano /etc/supervisor/conf.d/<project-name>.conf
   ```
2. Add this configuration:
   ```ini
   [program:quackers]
   command=python3 /home/yourusername/quackers/bot.py
   directory=/home/yourusername/quackers
   autostart=true
   autorestart=true
   stderr_logfile=/var/log/quackers.err.log
   stdout_logfile=/var/log/quackers.out.log
   user=yourusername
   ```
3. Apply changes:
   ```bash
   sudo supervisorctl reread
   sudo supervisorctl update
   sudo supervisorctl start quackers
   ```
4. Monitor logs:
   ```bash
   tail -f /var/log/quackers.out.log
   ```

---

## 8. Monitoring server via command lines

1. Install SnapD:
   ```bash
   sudo apt install snapd -y
   ```
2. Install GOTOP:
   ```bash
   sudo snap install gotop
   ```
3. Run Gotop:
   ```bash
   gotop
   ```
4. Quit Gotop:
   <br>Press ```Q```

---

## 📋 9. Handy Stuff to Know

| Action                     | Command                                         |
|----------------------------|-------------------------------------------------|
| Connect as user            | `ssh username@<your-linode-ip-address>`         |
| Reboot the server          | `sudo reboot`                                   |
| Activate virtual environment | `source path/venv/bin/activate`               |
| Deactivate virtual environment | `deactivate`                                |

Rerouting a domain to your server :
<br>Add an Advanced DNS :
<br>
|Hostname | Type | Value | TTL|
|---|---|---|---|
|@ | A | 184.246.0.204 | 3600|

This means that domain.com will resolve to 184.246.0.204

---

Enjoy your newly configured Linux server! 🎉
