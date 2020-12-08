# Wordpress Installation Guide
#### Lochlan Dorman
Note, any quotes in **bold** are user selected credentials.

## Assuming Apache2 and Static IP are set:
1. #### Remove Apache2 index.php in web root directory
	> sudo rm index.php
2. #### Make sure SSH port is set to 6597
	> sudo nano /etc/ssh/sshd_config
	- Change port 22 to port 6597
	- Change permit root login to yes
	- save
	> sudo service ssh restart
3. #### SSH in via SSH terminal of your choice (I am using code anywhere for this purpose)
4. #### Add php repository
	> sudo add-apt-repository -y ppa:ondrej/php
	> sudo apt-get update
5. #### Install PHP 7.2
	> sudo apt-get install php7.2
	> y
6. #### Install mysql Server
	> sudo apt-get install mysql-server
	> y
	- create mysql password
	> sudo mysql_secure_installation
	> n
	> n
	> y
	> n
	> n
	> y
7. #### Check php Status
	> php -v
	- Php should say 7.2
8. #### Check mysql
	> sudo service mysql status
	- Should say mysql is active
9. #### Install libApache2 Mod
	> sudo apt-get install libApache2-mod-php7.2
10. #### Install mysql Extension
	> sudo apt-get install php7.2-mysql
11. #### Install mbstring
	> sudo apt-get install php7.2-mbstring
12. #### Navigate to directory containing web root directory
	> cd /var/www
	- grant user privileges in root directory
	> sudo chown -R **SSH username** root
	- navigate to root directory
	> cd root
	- download latest wordpress zip
	> curl -O https://wordpress.org/latest.zip
13. #### Install Unzip
	> sudo apt-get install unzip
14. #### Unzip latest.zip
	> unzip latest.zip
15. #### restart apache2
	> sudo service apache2 restart
16. #### Visit static IP in browser and confirm wordpress is installed
17. #### Click "lets go" and then return to SSH terminal
18. #### Manually Configure mysql
	> sudo mysql -u root -p
	- enter mysql password
19. #### Inside of mysql terminal
	> CREATE DATABASE **databasename**;
	> CREATE USER '**wordpressuser**'@'localhost' IDENTIFIED BY '**password**';
	> GRANT ALL PRIVILEGES ON **databasename**.* TO '**wordpressuser**'@'localhost';
	> SHOW DATABASES;
	- Here you should see your **databasename** in the table
	> FLUSH PRIVILEGES;
	> exit
20. #### Restart mysql and apache2
	> sudo service mysql restart
	> sudo service apache2 restart
21. #### Navigate back to your browser
	- #### Enter
		- **databasename**
		- **user**
		- **password**
	- #### Leave local host
	- change prefix from _wp__ to _sc__
	- Click "submit"
22. #### Copy text from page to clipboard
23. #### Navigate back to SSH terminal
24. #### Navigate to wordpress folder
	> cd /var/www/root/wordpress
25. #### Create wp-config.php and paste text from clipboard
	> sudo nano wp-config.php
	- Paste text copied to clipboard in step 22
	- Save and exit
26. #### Navigate back to browser
	- Click "run installation"
	- Input your info for your wordpress site
	- Click "install wordpress"
	- Click "log in"
	- Enter your credentials
	- Click "log in"
27. ## Wordpress is installed. YAY!
