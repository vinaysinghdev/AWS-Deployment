# Deploy Node on AWS

> Don't add .env file in gitignore file
> make repo public for some time

> #### create an instance
> #### set instance  config = ubuntu 

> #### go to security group and edit it and edit inbounds rules


##### Add Rule 1.
```
type = http  
port = 80
source = anywhere
```
##### Add Rule 1.
```
type = https  
port = 443
source = anywhere
```
##### Add Rule 1.
```
type = Custom TCP  
port = [Your Port]
source = anywhere
```

> #### go to instance and connect to linux cmd
##### sudo su -
##### curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
##### . ~/.nvm/nvm.sh
##### nvm install node
##### node -v
##### npm -v
##### apt-get update -y
##### apt-get install git -y
##### git — version
##### git clone [your repo url]
##### cd [your repo]
##### npm install
##### npm start
##### stop app using [ctrl+c]

> #### installation of pm2 for always running server

##### npm install pm2 -g
##### pm2 start app.js -n [app name]

> #### Other pm2 commands
##### pm2 show [your app.js]
##### pm2 status
##### pm2 stop [your app.js]
##### pm2 logs (Show log stream)
##### pm2 flush (Clear logs)
##### pm2 restart [your app.js]

> #### To make sure app starts when reboot
##### pm2 startup ubuntu

> #### Setup ufw firewall

##### sudo ufw enable
##### sudo ufw status
##### sudo ufw allow ssh <--(Port 22)-->
##### sudo ufw allow http <--(Port 80)-->
##### sudo ufw allow https <--(Port 443)-->

> #### Install NGINX and configure

##### sudo apt install nginx
##### sudo nano /etc/nginx/sites-available/default

> #### use up and down key for moving add domain name  and  remove location and paste this
```
server_name domain.com www.domain.com;
location / {
    proxy_pass http://localhost:PORT;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
}
```

> #### Check NGINX config
##### sudo nginx -t

> #### Restart NGINX
##### sudo service nginx restart

> #### connect domain 
##### go to GoDaddy and update
##### A @ record and put value of your public url
##### and update www subdomain value to your domain like value=[domain.com]


> ####  Install Certbot in Ubuntu with snapd
##### sudo apt install snapd;
##### sudo snap install core; sudo snap refresh core;

> #### Install Certbot with snapd:
##### sudo snap install --classic certbot

> #### Create a symlink to ensure Certbot runs
##### sudo ln -s /snap/bin/certbot /usr/bin/certbot


> #### add ssl to your site using lets encrypt
##### sudo certbot --nginx


#### Here your site is deployed with ssl.
#### If You want to add redirection non www to www also enable http/2 protocol go to hostinger deployment repo
##### 😃😃😃😃😃😃😃😃😃😃😃😃😃😃😃😃😃😃


#### FOR UPDATE THE APPLICATION

> #### go to instance and run
##### sudo su -

> #### after that you have go inside your repo by ls command
##### git pull origin main

😃😃😃😃😃😃😃😃😃😃😃😃😃😃😃😃😃😃