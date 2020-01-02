### How to setting multiple sites in apache

```
https://www.liquidweb.com/kb/configure-apache-virtual-hosts-ubuntu-18-04/

Step 1: Make a Directory for Each Site
mkdir -p /var/www/domain.com/public_html
mkdir -p /var/www/domain2.com/public_html

Step 2: Set Folder Permissions
chmod -R 755 /var/www

Step 3: Set up an Index Page
vim /var/www/domain.com/public_html/index.html
testing for domain.com
:wq

Repeat the steps for your second domain, using the command below.
vim /var/www/domain2.com/public_html/index.html

Step 4: Copy the Config File for Each Site
Copy the default configuration file for each site, this will also ensure that you always have a default copy for future site creation.

cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/domain.com.conf

cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/domain2.com.conf

Step 5: Edit the Config File for Each Site
vim /etc/apache2/sites-available/domain.com.conf

<VirtualHost *:80>
ServerAdmin admin@example.com
ServerName domain.com
ServerAlias www.domain.com
DocumentRoot /var/www/domain.com/public_html
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

Step 6: Disable default config and Enable Your Config File
a2dissite 000-default.conf
a2ensite domain.com.conf
a2ensite domain2.com.conf

We restart the Apache service to register our changes.
systemctl restart apache2

```
### some aws services
```
aws email ses Oregon
aws ec2 instance Ohio
```
### Restart odoo
>sudo odoo restart

### config
```
/etc/odoo/odoo.conf
data_dir = /home/ubuntu/.local/share/Odoo
```
### Backup database
```
pw ten anh xa
http://my_host/web/database/manager
```
### Config domain name
```
/etc/apache2/sites-available/my_host.conf
sudo systemctl restart apache2
```
### Backup source code
```
/opt
tar -czvf opt.tar.gz /opt
tar -xzvf opt.tar.gz -C /opt
```
### connect to gostuffs_2019 database (usr: sync or ubuntu)
```
psql -U sync -h 127.0.0.1 -d gostuffs_2019
psql gostuffs_2019
\q
\dt product_product
\d product_product

select COLUMN_NAME from information_schema.COLUMNS
where TABLE_NAME = 'product_product';

select TABLE_NAME from information_schema.TABLES 
WHERE TABLE_NAME like '%product%';
```
### postgresql port
>select * from pg_settings where name='port';

#### Enable postgres from ec2 to access remotely, not recommend in PROD
```
https://progblog10.blogspot.com/2013/06/enabling-remote-access-to-postgresql.html
```
### add port 5432 to ec2 outbound setting
```
- from security group 
add: Postgresql tpc port:5432 Source:0.0.0.0/0
add: Postgresql tpc port:5432 ::/0
```
### SSH:
```
cd /etc/postgresql/10/main
sudo vim pg_hba.conf

after: 
host    all             all             127.0.0.1/32            md5
add:
host    all             all             0.0.0.0/0               md5

then save file

sudo vim postgresql.conf

replace:
#listen_addresses = 'localhost'
with
listen_addresses = '*'

then save file
```
### Restart postgres
>sudo /etc/init.d/postgresql restart

### How to reset master password
```
-open:
/etc/odoo/odoo.conf
-comment out admin_password by ';'
;admin_password = xxxx

-restart odoo
open http://18.191.163.254:8069/web/database/manager to set new password

```
