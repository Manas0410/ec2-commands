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

# Nginx Setup

### Install Nginx

```bash
sudo apt install nginx
```

### Unlink Default Configurations

```bash
sudo unlink /etc/nginx/sites-available/default
sudo unlink /etc/nginx/sites-enabled/default
```

### Create Domain Configuration File

```bash
sudo touch /etc/nginx/sites-available/domain.com
sudo vim /etc/nginx/sites-available/domain.com
```

### Paste the Following Code into the Domain Configuration File

```nginx
server {
    listen 80;
    server_name domain.com;

    location / {
        proxy_pass http://127.0.0.1:3000;
    }
}
```

### Create Symbolic Link and Test Configuration

```bash
sudo ln -s /etc/nginx/sites-available/domain.com /etc/nginx/sites-enabled/
sudo nginx -t
```

### Start Nginx

```bash
sudo systemctl start nginx
```

### Stop Nginx

```bash
sudo systemctl dtop nginx
```

### Restart Nginx

```bash
sudo systemctl restart nginx
```

### Reload Nginx

```bash
sudo systemctl reload nginx
```

### Check status of Nginx

```bash
sudo systemctl status nginx
```

### commands to remove nginx 
```bash
sudo systemctl stop nginx
sudo apt-get purge nginx nginx-common nginx-full -y
sudo rm -rf /etc/nginx
sudo rm -rf /var/www/html
sudo rm -rf /var/log/nginx
sudo apt-get autoremove -y
sudo apt-get autoclean -y
```

# Deployment of backend application via NGINX

###1 make sure all the needed dependencies , pm2 and nginx is installed

###2 clone ur project and install all the dependencies

###3 unlink the default configuration of nginx

```bash
sudo unlink /etc/nginx/sites-available/default
sudo unlink /etc/nginx/sites-enabled/default
```

###4 create confiuration file 
```bash
sudo touch /etc/nginx/sites-available/domain.com
```

###5 paste the below code in configuration file
```bash
sudo vim /etc/nginx/sites-available/domain.com
```

##1 => to serve on main url
```nginx
server {
    listen 80;
    server_name domain.com;

    location / {
        proxy_pass http://127.0.0.1:3000;
    }
}
```

##2=> ton serve on mainurl/backend
```nginx
server {
    listen 80;
    server_name domain.com;

    location /backend/ {
        proxy_pass http://127.0.0.1:3000/;
    }
}
```


###6 Create Symbolic Link and Test Configuration

```bash
sudo ln -s /etc/nginx/sites-available/domain.com /etc/nginx/sites-enabled/
sudo nginx -t
```



// symlink was not created

// pm2 startup

// enable in mongo

// sudo systemctl enable mongo
