# SETING UP A LINUX SERVER

# LINUX Necessary Setup

## 1st Steps

Connect via Terminal to control the server
```bash
ssh root@<your-linode-ip-address>
```
Update the server
```bash
apt update && apt upgrade -y
```
## Add User (not Root)

Add a user to the server
```bash
adduser yourusername
```

Make it possible for the user to use SUDO commads
```bash
usermod -aG sudo yourusername
```

## Setup a Firewall 

```bash
apt install ufw
ufw allow OpenSSH
ufw enable
```
## Switch to personal user 
```bash
su - yourusername
```

## CUSTOMIZATION

# INSTALLATION OF SOFTWARE 

## Python and Git

Install Python
```bash
apt install python3 python3-pip -y
```

Install Git
```bash
apt install git -y
```

Install Supervisor
```bash
apt install supervisor -y
```
# Making Repo Run

## Installing the repo 

Install the repository
```bash
git clone reponame
```
Navigate to the repository
```bash
cd reponame
```
Create a virtual Env for python
```bash
python3 -m venv venv
```
Activate the venv 
```bash
source venv/bin/activate
```
Intall all pip requirements
```bash
pip3 install -r requirements.txt
```

Making sure everything runs smoothly
```bash
python3 main.py
```

## Setting up a Supervisor for the python script

Create a supervisor file 
```bash
sudo nano /etc/supervisor/conf.d/quackers.conf
```

Complete the config file
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
Restart the supervisor 
```bash
sudo supervisorctl reread
sudo supervisorctl update
sudo supervisorctl start quackers
```
Check for log 
```bash
tail -f /var/log/quackers.out.log
```