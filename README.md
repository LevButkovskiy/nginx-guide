# Server guide
#### Guide for setup Nginx Ubuntu server

## Contents

- [System requirements](#sys_requirements)

- [Software requirements](#soft_requirements)

- [Nginx](#nginx_guide)

	- [Nginx installation](#nginx_installation)
	- [Nginx settings](#nginx_settings)

- [SSL](#ssl)
	- [Certbot](#certbot) 

- [Clonning project from git](#clone_from_git)
	- [Prepare folder for git](#prepare_folder_for_git)
	- [Installing node](#node_install)

<a name="sys_requirements"></a>
## System requirements

- Ubuntu 20.04

<a name="soft_requirements"></a>
## Software requirements
- HTTP
	- nginx 1.20.1
- SSL
	- snapd 2.51.4
	- certbot 1.18.0
- Project
	- Node JS LTS 14.17.6	 

<a name="nginx_guide"></a>
## Nginx

<a name="nginx_installation"></a>
### Install Nginx

1. ``` sudo apt-get update ``` - Check Ubuntu updates
2. ``` sudo apt install nginx ``` - Install nginx
3. ``` sudo systemctl start ``` - Start nginx
4. ``` sudo systemctl enable nginx ```- Start nginx with server (Auto launch)
5. Done 
![Result of install](https://sun9-53.userapi.com/impg/rfxwM-tJAYnZ1Kbct26lhnVEFudIZRB6D8lk0g/GJnJHTGiIEw.jpg?size=2560x420&quality=96&sign=52afe6d74016ccca424e820f1599e943&type=album)

<a name="nginx_settings"></a>
### Nginx settins

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
8. Create new directory ``` mkdir /var/www/%hostname%/ ```
9. Create directory ``` mkdir /var/www/%hostname%/public_html ```
10. In new directory place project build 
11. In command line type: ``` sudo systemctl restart nginx ``` to restart nginx
12. Done. Your project build on server

<a name="ssl"></a>
## SSL (HTTPS)

<a name="certbot"></a>
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

P.S To set certs for new nginx configuration type ``` sudo certbot --nginx ```

<a name="clone_from_git"></a>
## Clonning project from Git

<a name="prepare_folder_for_git"></a>
### Prepare folder

1. Clear folder for your project from git ``` rm -r /var/www/%hostname%/public_html/ ```
2. Cd to folder: ``` /var/www/%hostname%/
3. Clone git repo ``` git clone https://github.com/%user name%/%repository name% public_html ```
4. Cd to public_html ``` cd public_html ```
5. Done

<a name="node_install"></a>
### Installing node
1. Check updates ``` sudo apt update ```
2. Install node js ``` sudo apt install nodejs ```
3. Install npm ``` sudo apt install npm ```
4. Install npm into your project ``` npm install ```
5. Build latest version of your project ``` npm run build ```
6. Edit  ``` /etc/nginx/sites-available/%hostname%-ru.conf  ```
``` 
	root /var/www/%hostname%/public_html; 
``` 
Change to
``` 
	root /var/www/%hostname%/public_html/build; 
```
7. Check nginx syntax ``` nginx -t ```
8. Restart nginx ``` sudo systemctl resart nginx ```
9. Done

P.S. To further get updates from git in ``` /var/www/%hostname%/public_html ``` type ``` git pull ``` and then ``` npm install```, ``` npm run build ```
