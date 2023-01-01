### Setup Nginx in a ubuntu server

```shell
sudo apt-get update
sudo apt-get install nginx -y
ps auwx | grep nginx
```

### Add a http server to deployment

```shell
cd /etc/nginx/sites-available
sudo nano <domain_name eg: imagery.rajivharlalka.me>
```

Nginx config of http server

```nginx
server {
        listen 80;
        listen [::]:80;

        server_name imagery.rajivharlalka.me;
        access_log /var/log/nginx/reverse-access.log;
        error_log /var/log/nginx/reverse-error.log;

        location / {
                    proxy_pass http://127.0.0.1:3000;
  }
```

- save and exit

- create symlink from sites-available to sites-enabled

```shell
sudo ln -s /etc/nginx/sites-available/<file-name> /etc/nginx/sites-enabled/<file-name>
```

- test nginx config and reload

```
sudo nginx -t && sudo nginx -s reload
```

if everything ok then server should be start serving

### HTTPS config through certbot

- PreRequisites:
  Add the name as a A name to dns cloud-providers first.

Install certbot

```shell
sudo apt-get update
sudo apt-get install certbot
sudo apt-get install python3-certbot-nginx
```

Now Run to create certificates

```shell
sudo certbot --nginx -d <domain-name>
```

This should do everything.
