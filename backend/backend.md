Backend areas

- APIs
- Data analytics
- Security
- Reliability
- Databases
- Platform

## Buy a VPS

Buy one from a cloud provider. Digital Ocean has a nice setup experience for beginners.

## SSH

Generate an ssh key, this provides a public and private key pair.

Give a server your public ssh key and your machine has the private key. This is how they setup a secure tunnel to communicate

Creating a SSH key:

```
cd ~/.ssh

ls // to see files

ssh-keygen // generate ssh key
```

- Give it a unique name

Getting into a server:

```
ssh root@SERVER_IP

// or

ssh -i ~/.ssh/{private_key_name} root@SERVER_IP // use specific ssh key file
```

Add private key to keychain (sometimes not needed):

```
vi ~/.ssh/config

Host *
  AddKeysToAgent yes
  UseKeychain yes

ssh-add -K ~/.ssh/{private_key_name} // add private key to keychain
```

## Domains

DNS Records:

A record - mops name to IP Address
CNAME - maps name to name

jemyoung.com -> 23.23.185.61 this is an A Record

dig blog.jemyoung.com

## Server setup

1. Update software

- apt update
- apt upgrade

2. Create a new user

- adduser \$USERNAME

3. Make that user a super user

- usermod -aG sudo \$USERNAME
- su \$USERNAME
- sudo cat /var/log/auth.log

4. Enable login for new user
5. Disable root login

```
// Change to home directory
cd ~

// If Digital Ocean server: (rest is not needed)
rsync --archive --chown=$USERNAME:$USERNAME ~/.ssh /home/$USERNAME

// May need to add your own pub key to authorized_keys

// Create new directory if it doesn't exist
mkdir -p ~/.ssh

// Create authorized_keys file
vi ~/.ssh/authorized_keys
```

Change file permissions:

```
chmod 644 ~/.ssh/authorized_keys

// Disable root login
sudo vi /etc/ssh/sshd_config -> PermitRootLogin no

// Restart ssh daemon
sudo service sshd restart
```

### Nginx

- Reverse proy
- Web server
- Proxy server

Show nginx config:

```
sudo less /etc/nginx/sites-available/default
```

### NodeJS

Install nodejs, npm and git on the server

```
sudo apt install nodejs npm git
```

Add NodeJS server to server

```
sudo chown -R $USER:$USER /var/www

mkdir /var/www/app

cd /var/www/app && git init
```

Run application:

```
node app.js
```

## Configuring nginx for express

## What about server restarts?

Use a process manager

- Keeps your application running
- Handles errors and restarts
- Can handle logging and clustering

```
sudo npm install --save pm2
```

### Security

- Controlling access
- Securing applications
- Firewalls
- Permissions
- Upgrading NodeJS

Use:

- SSH
- Firewalls
- Updates
- Two factor authentication
- VPN

sudo apt install unattended-upgrades

Use ufw for port security

```
sudo ufw allow ssh

sudo ufw enable
```

https://explainshell.com/ is great for explain shell commands

Download and setup new nodejs

```
curl -sL https://deb.nodesource.com/setup_10.x -o nodesource_setup.sh

sudo bash nodesource_setup.sh

sudo apt install nodejs
```
