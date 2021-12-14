# WEB STACK IMPLEMENTATION (LEMP STACK)

## STEP 1 – INSTALLING THE NGINX WEB SERVER

`sudo apt update`

`sudo apt install nginx`

To verify that nginx was successfully installed and is running as a service in Ubuntu, run:

`sudo systemctl status nginx`


## STEP 2 — INSTALLING MYSQL
`sudo apt install mysql-server`

interactive script by running:

`sudo mysql_secure_installation`

test if you’re able to log in to the MySQL console by typing:

`sudo mysql`


## Step 3 – Installing PHP

You’ll need to install php-fpm, which stands for “PHP fastCGI process manager”, and tell Nginx to pass PHP requests to this software for processing. Additionally, you’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. Core PHP packages will automatically be installed as dependencies.

To install these 2 packages at once, run:

`sudo apt install php-fpm php-mysql`


## STEP 4 — CONFIGURING NGINX TO USE PHP PROCESSOR

Create the root web directory for your_domain as follows:

`sudo mkdir /var/www/edumixlemp`

`sudo chown -R $USER:$USER /var/www/edumixlemp`
Then, open a new configuration file in Nginx’s sites-available directory using your preferred command-line editor. Here, we’ll use nano:

`sudo nano /etc/nginx/sites-available/edumixlemp`
This will create a new blank file. Paste in the following bare-bones configuration:

`#/etc/nginx/sites-available/edumixlemp

server {
    listen 80;
    server_name edumixlemp www.edumixlemp;
    root /var/www/edumixlemp;

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

}`

Here’s what each of these directives and location blocks do:

### listen 
Defines what port Nginx will listen on. In this case, it will listen on port 80, the default port for HTTP.
### root
Defines the document root where the files served by this website are stored.
### index
Defines in which order Nginx will prioritize index files for this website. It is a common practice to list index.html files with a higher precedence than index.php files to allow for quickly setting up a maintenance landing page in PHP applications. You can adjust these settings to better suit your application needs.
### server_name 
Defines which domain names and/or IP addresses this server block should respond for. Point this directive to your server’s domain name or public IP address.
### location / 
The first location block includes a try_files directive, which checks for the existence of files or directories matching a URI request. If Nginx cannot find the appropriate resource, it will return a 404 error.
### location ~ \.php$ 
This location block handles the actual PHP processing by pointing Nginx to the fastcgi-php.conf configuration file and the php7.4-fpm.sock file, which declares what socket is associated with php-fpm.
### location ~ /\.ht 
The last location block deals with .htaccess files, which Nginx does not process. By adding the deny all directive, if any .htaccess files happen to find their way into the document root ,they will not be served to visitors.


Activate your configuration by linking to the config file from Nginx’s sites-enabled directory:

`sudo ln -s /etc/nginx/sites-available/edumixlemp /etc/nginx/sites-enabled/`
This will tell Nginx to use the configuration next time it is reloaded. You can test your configuration for syntax errors by typing:

`sudo nginx -t`

disable default Nginx host that is currently configured to listen on port 80, for this run:

`sudo unlink /etc/nginx/sites-enabled/default`

reload Nginx to apply the changes:

`sudo systemctl reload nginx`

then write inside the index.html file
`sudo echo '<!DOCTYPE html>
<html>
<head>
<title>Welcome to EDUmix on Nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to EDUmix!</h1>
<p>best Education.</p>

<p><em>Thank you for using our service.</em></p>
</body>
</html>' > /var/www/edumixlemp/index.html`





##

##


##


##


##


##


##
