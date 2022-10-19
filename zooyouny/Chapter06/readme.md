# Install MySQL

install

`> brew install mysql`

To restart mysql after upgrade

`> brew services restart mysql`

Set root password

`> mysql_secure_installation`

To connect run

`> mysql -u root` or `> mysql -u root -p`

Server operation
```
> mysql.server start
> mysql.server status
> mysql.server stop
```