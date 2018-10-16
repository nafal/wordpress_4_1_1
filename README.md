Wordpress Staging
-----------------
```
sudo su
apt-get update
apt-get upgrade -y
apt-get dist-upgrade -y
apt-get autoremove -y
apt-get install apache2 php php-cli php-fpm php-gd php-ssh2 libapache2-mod-php php-mysql git unzip zip postfix php-curl mailutils php-json php-xml -y
a2enmod rewrite headers
phpenmod mcrypt

nano /etc/apache2/sites-enabled/000-default.conf

<VirtualHost *:80>
        #ServerName example.com
        #ServerAlias www.example.com
        DocumentRoot /var/www/staging

        <Directory /var/www/staging>
                Options -Indexes
                AllowOverride All
                Order allow,deny
                Allow from all
        </Directory>
</VirtualHost>

cd /var/www/html
rm -rf *
cd ../
mkdir staging
cd staging
git clone https://github.com/andrewpuch/wordpress_4_1_1.git .
chmod -R 744 .
chown -R www-data:www-data .

service apache2 restart
```
After Wordpress Is Configured
-----------------------------
```
define('WP_REDIS_HOST', '');
```
