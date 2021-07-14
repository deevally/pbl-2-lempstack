# DEPLOY LEMP STACK APPLICATION ON AWS

___

> Step 1

- Install NGINX Server 
- __sudo__ apt update & __sudo__ apt install nginx

- Verify NGINX is running 
-   __sudo__ systemctl status nginx
- if color is green, than everything is installed corrected.

-   Go to the security group and allow port 80 and then access nginx server locally and from the Internet.

1.  Access it locally in our Ubuntu shell, run:

- __curl__ http://localhost:80 or curl http://127.0.0.1:80

2.  Access it from the internet, open a web browser and type http://Public-IP-Address:80

- ![](images/nginx.png)


- To get the public IP Address, use 
- __curl__ -s http://169.254.169.254/latest/meta-data/public-ipv4

> Step 2 
- Install MySql Server

- __sudo__ apt install mysql-server  

- Run a security script that comes pre-installed with MySQL  
__sudo__ mysql_secure_installation  
You can enable VALIDATE PASSWORD PLUGIN by pressing Y or press other keys to continue without enabling it.  
- Login to MySQL console  
__sudo__ mysql. Run __exit__ to exit out of the mysql console.

> Step 3 
- Install PHP

- __sudo__ apt install php-fpm php-mysql
- When prompted, type Y and press ENTER to confirm installation.

> Step 4

- Configure NGINX to use PHP processor.

- Nginx has one server block enabled by default and is configured to serve documents out of a directory at /var/www/html. But to serve multiple sites,  create a directory structure within /var/ww ,leaving /var/www/html in place as the default directory to be served if a client request does not match any other sites. 

- Create the root web directory for your_domain as follows:

- __sudo__ mkdir /var/www/projectLEMP

- Next, assign ownership of the directory with the $USER environment variable, which will reference your current system user:

- __sudo__ chown -R $USER:$USER /var/www/projectLEMP

- Open a new configuration file in Nginx’s sites-available directory

- __sudo__ nano /etc/nginx/sites-available/projectLEMP

- Paste in the following configuration

```
#/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}
```

- Save and Close. If you’re using nano, you can do so by typing CTRL+X and then y and ENTER to confirm.




