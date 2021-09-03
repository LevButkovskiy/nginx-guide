# Server guide
#### Guide for setup Nginx Ubuntu server

## System requirements 

- Ubuntu 20.04

## Nginx
### Install Nginx

1. ``` sudo apt-get update ``` - Check Ubuntu updates
2. ``` sudo apt install nginx ``` - Install nginx
3. ``` sudo systemctl start ``` - Start nginx
4. ``` sudo systemctl enable nginx ```- Start nginx with server (Auto launch)
5. Done 
![Result of install](https://sun9-53.userapi.com/impg/rfxwM-tJAYnZ1Kbct26lhnVEFudIZRB6D8lk0g/GJnJHTGiIEw.jpg?size=2560x420&quality=96&sign=52afe6d74016ccca424e820f1599e943&type=album)

### Loading build to server

1. Move to ``` /etc/nginx/sites-available/ ```
2. Create ``` %hostname%-ru.conf ```
3. In file type: 
``` 
server {
	listen 80;
	server_name %hostname%.ru www.%hostname%.ru;

	root /var/www/%hostname%.ru/public_html;

	index index.html index.htm;

	location / {
		try_files $uri $uri/ =404;
	}
}
```
4. In command line type: ``` ln -s /etc/nginx/sites-available/%hostname%-ru.conf /etc/nginx/sites-enabled/ ``` to create link between sites-available and sites-enabled
5. Delete default file from  ``` /etc/nginx/sites-enabled/ ``` (``` rm -rf /etc/nginx/sites-enabled/default ```)
6. Type ``` nginx -t ``` To check syntax. Result should be: ``` nginx: the configuration file /etc/nginx/nginx.conf syntax is ok ```
7. Move to ``` /var/www/ ```
8. Create new directory ``` /var/www/%hostname%/public_html ```
9. In new directory place project build 
10. In command line type: ``` sudo systemctl restart nginx ``` to restart nginx
11. Done. Your project build on server

## SSL (HTTPS)

### Certbot
#### Certbot using for LetsEncrypt certificates

1. ``` sudo apt install snapd ``` to install snapd (Using for certbot)
2. ``` sudo snap install core; sudo snap refresh core ``` Install and update snap core
3. ``` sudo apt-get remove certbot ```, ``` sudo dnf remove certbot ```, or ``` sudo yum remove certbot ```
4. ``` sudo snap install --classic certbot ``` Install certbot
5. ``` sudo ln -s /snap/bin/certbot /usr/bin/certbot ``` Execute the following instruction on the command line on the machine to ensure that the certbot command can be run.
6. ``` sudo certbot --nginx ``` Install ssl in all configurations
7. ``` sudo certbot renew --dry-run ``` To authomaticaly renew certificates
8. Done. Go to https://%hostname%.ru
![Result](https://sun9-80.userapi.com/impg/FJyZ0rnNfZLO3EVofTbilBPzOalhHPm8p0CPqw/qyUg0GZ3v3Y.jpg?size=1166x332&quality=96&sign=b9f25a1a4812b7588b40e11640dffae5&type=album)
