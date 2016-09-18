---
title: "Install wordpress on OSX/MAC"
date: 2016-09-18 11:08
---

# Tools

1. Apache HTTP Server
2. MySQL Community Server 
3. wordpress
4. PHP Interpreter

# Installation 
## Apache HTTP Server
1. Go to <https://httpd.apache.org/>, then download the lastest version. It'a bz2 or gz package.
2. Extract the package, entering into main directory.
3. sudo ./configure
4. sudo make && make install
5. sudo apachectl start/stop, or sudo apachectl -k restart

## MySQL Community Server
1. Go to <https://dev.mysql.com/downloads/mysql/> , download the format DMG Archive.
2. Open this DMG file to install it. Before the installation is completely finish,  **a password dialog** will prompt, and the random password is given. Please store it!
3. Via Spotlight opening MySQL.prefPane, and start MySQL Server.
4. Using `mysql -uroot -p` with the given random password to login under command window(zsh). Then update the password with ALTER USER, `ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass';`
5. To create database for wordpress 
	- `create database wordpress;` (wordpress is database name)
	- `grant all privileges on wordpress.* to "username"@"localhost" identified by "password";` username and password for wordpress admin.
	- `flush privileges;`
	- `exit`

## wordpress
1. Download source code of wordpress.
2. Extract it and put it in "/var/www/" .
3. Enter root directory of wordpress, create wp-config.php by copying wp-config-sample.php.
4. Configure Database relevant options.
	- define('DB_NAME', 'wordpress');
	- define('DB_USER', 'root');
	- define('DB_PASSWORD', 'mysql');
	- define('DB_HOST', 'localhost:/tmp/mysql.sock'); 
	
### Errors
1. mysqli_real_connect(): (HY000/2002): No such file or directory in /private/var/www/wordpress/wp-includes/wp-db.php on line 1529
	- change define('DB_HOST', 'localhost'); to define('DB_HOST', 'localhost:/tmp/mysql.sock'); 

## PHP Interpreter
1. To install PHP using command `curl -s http://php-osx.liip.ch/install.sh | bash -s 7.0`
2. Enter directory "/var/www/" which is the root path of your website, `sudo php -S localhost:80`
3. Open <http://localhost:80/wordpress/>


