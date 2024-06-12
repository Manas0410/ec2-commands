# EC2 Setup Commands (Ubuntu Jammy)

## Connect to EC2 via SSH

```bash
chmod 400 <key>
ssh -i <key> ubuntu@<ip>
sudo apt update
```

## Install Node.js

#### Install NVM

```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.0/install.sh | bash
```

#### Activate NVM

```bash
. ~/.nvm/nvm.sh
```

#### Install Node.js (choose version or use `node` for the latest version)

```bash
nvm install node
```

## Install MongoDB

```bash
sudo apt-get install gnupg curl
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
```

#### Start MongoDB

```bash
sudo systemctl start mongod
```

#### Check MongoDB Status

```bash
sudo systemctl status mongod
```

## PM2 Commands

#### Installation

```bash
npm install pm2 -g
```

#### Start Instance with PM2

```bash
pm2 start app.js
```

#### Check Logs

```bash
pm2 logs
```

#### Check All Logs

```bash
pm2 ls
```

#### Managing Processes

```bash
pm2 restart app_name
pm2 reload app_name
pm2 stop app_name
pm2 delete app_name
```

#### Act on All Processes

```bash
pm2 restart all
pm2 stop all
pm2 delete all
```

#### Act on a Specific Process ID

```bash
pm2 restart <id>
pm2 stop <id>
pm2 delete <id>
```