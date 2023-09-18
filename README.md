# BrainStromTask

This repository contains the configuration and instructions to set up an automated deployment process for a WordPress website using Nginx, the LEMP stack (Linux, Nginx, MySQL, PHP), and GitHub Actions. The deployment process follows security best practices and aims to ensure optimal website performance.

Prerequisites:
A server with a Linux-based operating system (e.g., Ubuntu 20.04 LTS).
A domain name pointed to your server's IP address.
SSH access to your server with sudo privileges.
A GitHub repository containing your WordPress project.


Step 1: Initial Server Setup - I use aws EC2 Instance


sudo apt update

sudo apt upgrade

sudo apt install -y curl git unzip

sudo apt install -y nginx mysql-server php-fpm php-mysql



Step 2: Configure Nginx

sudo nano /etc/nginx/sites-available/brainstrom.serveftp.com


server {
    listen 80;
    server_name brainstrom.serveftp.com www.brainstrom.serveftp.com;

    root /var/www/yourwebsite.com;
    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock; # Adjust the PHP version if needed
    }

    location ~ /\.ht {
        deny all;
    }
}


sudo ln -s /etc/nginx/sites-available/yourwebsite.com /etc/nginx/sites-enabled/

sudo nginx -t

sudo systemctl restart nginx



Step 3: Install WordPress

cd /var/www/

sudo wget https://wordpress.org/latest.tar.gz

sudo tar -xzvf latest.tar.gz

sudo mv wordpress yourwebsite.com

sudo chown -R www-data:www-data /var/www/brainstrom.serveftp.com



Step 4 : SSL configuration

sudo apt install certbot python3-certbot-nginx

sudo certbot --nginx -d brainstrom.serveftp.com







