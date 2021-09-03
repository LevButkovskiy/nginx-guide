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

1. Move to ``` /var/www/html ```
2. Create new directory
3. In new directory place build from React
4. Move to ``` /etc/nginx/sites-available/ ```
5. Edit default.json
6. In line: ``` root /var/www/html/ ``` add your new folder: ``` root /var/www/html/your_folder ``` 
7. In command line type: ``` sudo systemctl restart nginx ``` to restart nginx
8. Done. Your project build on server
