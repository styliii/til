We had issues with running Apache + Node JS + PM2 in production. We were seeing lots of 502 Proxy Errors. It was suggested on some sites (e.g. PM2's issue queue) that we should instead use Nginx in place of Apache. Below was what we documented when we installed Nginx, Node JS, and PM2 on Ubuntu. PM2 is a Node JS process manager that has clustering capabilities. Will report back on whether this solves our 502 issues.


### Update ubuntu and install nginx
1. `sudo apt-get update`
2. `sudo apt-get upgrade`
3. `sudo apt-get install htop git python-software-properties curl libm17n-0 rcconf dialog graphicsmagick build-essential openssl libssl-dev libpcre3 libpcre3-dev zlib1g-dev`
4. `sudo apt-get install libgoogle-perftools-dev google-perftools`
2. `wget http://nginx.org/download/nginx-1.10.1.tar.gz`
3. `tar zxvf nginx-1.10.1.tar.gz`
4. `rm nginx-1.10.1.tar.gz`
5. `cd nginx-1.10.1`
6. `sudo ./configure --with-google_perftools_module --with-http_stub_status_module --with-http_ssl_module`
7. `sudo make`
8. `sudo make install`
9. `sudo ln -s /usr/local/nginx/sbin/nginx /usr/bin/nginx`
10. Add `/etc/init/nginx.conf` with info from https://www.nginx.com/resources/wiki/start/topics/examples/ubuntuupstart/#
11. In above script, may need to change DAEMON to `env DAEMON=/usr/bin/nginx`
11. `sudo initctl list | grep nginx`
12. `sudo initctl start nginx`
3. Visit `http://{ip_address}` to verify successful nginx install
5. Create your web directory: `sudo mkdir -p /var/www/{site}/html`
6. Configure permissions: `sudo chown -R $USER:$USER /var/www/{site}/html`
7. `sudo chmod -R 755 /var/www`

### Install Git, checkout repo
1. `sudo apt-get install git`
2. `git config --global user.name "name"`
3. `git config --global user.email "email"`
4. Create ssh keys, upload to git user's account
5. Clone your repo to `/var/www/{site}/html`

### Install node and npm
1. Install nvm from `https://github.com/creationix/nvm`
2. `nvm install 4.4.7`
3. `nvm use 4.4.7`
4. `nvm alias default 4.4.7`
5. Update npm: `cd ~/.nvm/versions/node/v4.4.7/lib` and then `npm install npm`

### Install PM2
1. `npm install pm2 -g`
2. `pm2 startup ubuntu`
3. `pm2 start app.js`
4. `pm2 startup ubuntu`
1. Follow instructions from CLI

### Nginx configuration
1. Tweak the config from https://keymetrics.io/2014/06/17/high-performance-server-configuration-with-ubuntunginxpm2/

### Rotate logs
1. Create file in /etc/logrotate.d/nginx.
2. Paste and modify the following:
```bash
/var/log/nginx/*.log {
        daily
        missingok
        rotate 52
        compress
        delaycompress
        notifempty
        create 640 nginx adm
        sharedscripts
        postrotate
                [ -f /var/run/nginx.pid ] && kill -USR1 `cat /var/run/nginx.pid`
        endscript
}
```
4. Run `sudo logrotate -f /etc/logrotate.d/nginx` to confirm that your log rotate works.
