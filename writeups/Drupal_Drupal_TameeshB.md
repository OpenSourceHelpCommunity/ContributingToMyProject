# Contributing to Drupal


## What is Drupal 
Drupal is content management software.  
It's used to make many of the websites and applications you use every day.  
Drupal has great standard features, like easy content authoring, reliable performance, and excellent security.  
But what sets it apart is its flexibility; modularity is one of its core principles.  
[More about the Drupal project here.](https://www.drupal.org/about)

## The Drupal community
The Drupal community is one of the largest open source communities in the world. 
We're more than 1,000,000 passionate developers, designers, trainers, strategists, coordinators, editors, and sponsors working together.
We build Drupal, provide support, create documentation, share networking opportunities, and more. 
Our shared commitment to the open source spirit pushes the Drupal project forward. 
New members are always welcome.

## Setting it up
### Prerequisites  
* Git
* XAMPP/LAMP/MAMP (respectively for Windows/Linux/Mac OS)
* phpmyadmin (XAMPP and MAMP stack already have it installed
* Composer

### Installing the server
* [Video on installing MAMP on Mac OS.](https://drupalize.me/videos/installing-mamp-web-server)
* [Guide on installing LAMP on Linux.](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-16-04)
* [Guide on installing XAMPP on Windows.](https://www.drupal.org/node/2559943)
* [Guide on installing phpmyadmin on LAMP stack.](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-12-04)

### Setup Steps:  
1. Download and install XAMPP/LAMP/MAMP depending on the operating system you use.    
2. Start Apache and MySQL servers.     
3. Start your terminal and navigate to your web server's directory. Enter one of the following commands:     
~~~~
   cd c:/xampp/htdocs on Windows.   
   cd /var/www on Linux.   
   cd /Applications/MAMP/htdocs on Mac.   
~~~~
4. Run the following command in the command line window:
~~~~
   git clone --branch 8.3.x http://git.drupal.org/project/drupal.git drupal8
~~~~
This will clone Drupal 8 in the 'drupal8' folder.   
You might need admin permissions to perform the above step.    
5. Provide Read and Write Permissions to 'sites/default' and all its subfolders.     
6. Run the following command in the command line window:     
`cd drupal8` to move to drupal8 folder.    
`composer update` to install all dependencies required by Drupal.     
7. Copy the 'default.settings.php', rename it 'settings.php' and paste it in the same folder.      
8. Open localhost/phpmyadmin from your favourite browser. Click 'Database' on the top left and enter the name of the new database as 'drupal8' (without quotes). Select UTF Unicode from the drop-down box and click Create.    
9. Set your password for MySQL for the “root” user by going to the 'User Accounts' tab in phpmyadmin.     
10. Now we are all set to install Drupal on our local server.    
11. Navigate to localhost/drupal8 .     
12. Select your preferred language and the default installation profile.    
13. Add information about the database server (mysql), site database (drupal8), database user (root) and database password (the password you set) .      
14. After all core modules are installed, complete the form regarding the site configuration.     

## [Ways to contribute](https://www.drupal.org/contribute)
## [Ladder to begin contributing](http://drupalladder.org/ladder/47217ef7-9bf5-4c7f-926f-aeee247aac78)
