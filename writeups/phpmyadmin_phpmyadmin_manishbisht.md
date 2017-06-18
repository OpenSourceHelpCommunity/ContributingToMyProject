# About
phpMyAdmin is a free software tool written in PHP, intended to handle the administration of MySQL over the Web. phpMyAdmin supports a wide range of operations on MySQL and MariaDB. Frequently used operations (managing databases, tables, columns, relations, indexes, users, permissions, etc) can be performed via the user interface, while you still have the ability to directly execute any SQL statement.

# Contribute to phpMyAdmin
As a free software project, phpMyAdmin is very open to your contributions.

# Setting up the Development Environment on Linux
## Installing Requirements
1. Install Apache `sudo apt-get install apache2`
2. Install MySQL `sudo apt-get install mysql-server`
3. Install PHP `sudo apt-get install php5 libapache2-mod-php5`
4. Restart Server `sudo /etc/init.d/apache2 restart`

or you can do all these in one step by running this command `sudo apt-get install lamp-server^`

Now go to the web directory the default is `var/www/html` and follow the below steps. 

## Installing from Git

Go to https://github.com/phpmyadmin/phpmyadmin.git and fork the repository.

Now clone the foked repository in your system:

`git clone https://github.com/<yourgithubusername>/phpmyadmin.git`

Additionally you need to install dependencies using the Composer tool:

`composer update`

Now Open your web browser and navigate to `http://locahost/<phpmyadmin-folder>` or `http://server-ip-address/<phpmyadmin-folder>`.

![](https://media.giphy.com/media/7rj2ZgttvgomY/giphy.gif)

Congratulations !! Your developement environment is set up. You are now ready to fix bugs and make improvements.

We welcome your contributions. Submit a pull request against our [GitHub repository](https://github.com/phpmyadmin/). You can also submit a [feature request](https://github.com/phpmyadmin/phpmyadmin/labels/enhancement) explaining your suggested improvements.

If you have any issues feel free to reach out to our following mailing list.

# Mailing Lists
For news/announcements: news@phpmyadmin.net

For developers: developers@phpmyadmin.net

For translators: translators@phpmyadmin.net

Git commit notifications: git@phpmyadmin.net

[Mailing lists overview](https://lists.phpmyadmin.net/)

# Additional Information
- https://docs.phpmyadmin.net/en/latest/setup.html
