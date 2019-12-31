### config
/etc/odoo/odoo.conf
data_dir = /home/ubuntu/.local/share/Odoo

### backup db
pw ten anh xa
http://my_host/web/database/manager

### config domain name
/etc/apache2/sites-available/my_host.conf
sudo systemctl restart apache2

### backup source code
/opt
tar -czvf opt.tar.gz /opt
tar -xzvf opt.tar.gz -C /opt

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

