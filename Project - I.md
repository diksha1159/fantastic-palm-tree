## WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS

### AWS account setup and provisioning an Ubuntu Server
#### Steps

1. Signed up for an AWS account.
2. Logged in as IAM user
3. In the VPC console, I created a Security Group
![1667209572756](https://user-images.githubusercontent.com/76660222/203963617-5a55b985-c9f9-401f-901c-888c46272331.png)
4. Launched an EC2 instance
5. I selelected the Ubuntu free tier instance
6. I set the required configurations (Enabled public IP, security group, and key pair) and finally launched the instance.
![1667209809108](https://user-images.githubusercontent.com/76660222/203963739-1f023c22-3e27-4588-80d6-3fefdd21dfc6.png)
Next I SSH into the instance using Windows Terminal
8. In the Terminal, I typed cd Downloads to navigate to the locxcation of my key-pair.
9. Inside the Downloads directory, I connect to my instance using its Public DNS.
 ![1667210358904](https://user-images.githubusercontent.com/76660222/203963808-a72f2d7d-0d3f-4459-a195-d64b2c60ae05.png)

![1667210406805](https://user-images.githubusercontent.com/76660222/203963858-6d1af4f9-7dbb-4aee-9468-e0cf8d2572f9.png)

### INSTALLING APACHE AND UPDATING THE FIREWALL

#### Steps

1. Install Apache using Ubuntu’s package manager ‘apt', Run the following commands: To update a list of packages in package manager: **sudo apt update**

![1667210617960](https://user-images.githubusercontent.com/76660222/203964137-761747a7-c160-4992-926f-8e7b4fe9a064.png)

2. To run apache2 package installation: **sudo apt install apache2**
3. Next, verify that Apache2 is running as a service in the OS. run: **sudo systemctl status apache2**
4. The green light indicates Apache2 is running.
![1667210754028](https://user-images.githubusercontent.com/76660222/203964268-ea29ac8b-40e6-4941-8505-a34033197a7c.png)

![1667210831339](https://user-images.githubusercontent.com/76660222/203964303-beed3187-b813-4ac9-9fd2-a666db7835d6.png)

5. Open port 80 on the Ubuntu instance to allow access from the internet.
6. Access the Apache2 service locally in our Ubuntu shell by running: **curl [http://localhost:80](http://localhost/)** or **curl [http://127.0.0.1:80](http://127.0.0.1/)** This command would output the Apache2 payload indicating that it is accessible locally in the Ubuntu shell.
7. Next, test that Apache HTTP server can respond to requests from the Internet. Open a browser and type the public IP of the Ubutun instance: **[http://172.31.81.129/:80](http://3.235.248.184/:80)** This outputs the Apache2 default page.
![1667211722269](https://user-images.githubusercontent.com/76660222/203964434-686e33ea-4dc0-474b-9f51-3556f5978994.png)

### INSTALLING MYSQL

#### Steps

In this step, I install a Database Management System (DBMS) to be able to store and manage data for the site in a relational database.

1. Run ‘apt’ to acquire and install this software, run: **sudo apt install mysql-server**
2. Confirm intallation by typing Y when prompted.
3. Once installation is complete, log in to the MySQL console by running: **sudo mysql**
![1667211918440](https://user-images.githubusercontent.com/76660222/203964660-e98c8c8b-3efd-42b0-b91f-029bc2569a18.png)

4. Next, run a security script that comes pre-installed with MySQL, to remove some insecure default settings and lock down access to your database system. run: **ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';** then exit MySQL shell by typing exit and enter.
5. Run interactive script by typing: **sudo mysql_secure_installation** and following the instrustions.
6. Next, test that login to MySQL console works. Run: **sudo mysql -p**

![1667213350350](https://user-images.githubusercontent.com/76660222/203964766-0d3dcec3-db8f-46dd-bc55-f55122cc64c7.png)


7. Type exit and enter to exit console.

### STEP 3 — INSTALLING PHP

#### Steps

1. To install these 3 packages at once, run: **sudo apt install php libapache2-mod-php php-mysql**
![1667213718529](https://user-images.githubusercontent.com/76660222/203964991-81e093cf-d553-4ad7-86d6-4b912e455898.png)

2. After installation is done, run the following command to confirm your PHP version: **php -v**
3. At this point, your LAMP stack is completely installed and fully operational.

   ### STEP 4 — CREATING A

   ### VIRTUAL HOST FOR YOUR WEBSITE USING APACHE

   #### Steps


   1. Setting up a domain called projectlamp. Create the directory for projectlamp using ‘mkdir’. Run: **sudo mkdir /var/www/projectlamp**
   2. assign ownership of the directory with your current system user, run: **sudo chown -R $USER:$USER /var/www/projectlamp**
   3. Next, create and open a new configuration file in Apache’s sites-available directory. Tpye: **sudo vi /etc/apache2/sites-available/projectlamp.conf**
   4. This will create a new blank file. Paste in the following bare-bones configuration by hitting on i on the keyboard to enter the insert mode, and paste the text: **<VirtualHost *:80> ServerName projectlamp ServerAlias [www.projectlamp](http://www.projectlamp/) ServerAdmin webmaster@localhost DocumentRoot /var/www/projectlamp ErrorLog ${APACHE_LOG_DIR}/error.log CustomLog ${APACHE_LOG_DIR}/access.log combined**

![1667214299791](https://user-images.githubusercontent.com/76660222/203965165-6c70e44d-d8ff-497a-8ffc-f642fdaa3ddb.png)
![1667214458058](https://user-images.githubusercontent.com/76660222/203965880-c82ab90d-290f-40e2-b9c1-8ac11c44bde0.png)

5. .To save and close the file. Hit the esc button on the keyboard, Type :, Type wq. w for write and q for quit and Hit ENTER to save the file. 6. use the ls command to show the new file in the sites-available directory: **sudo ls /etc/apache2/sites-available**
![1667214598913](https://user-images.githubusercontent.com/76660222/203965948-1dba42ab-0d8a-4311-baff-91616113ded6.png)

6. Next, use a2ensite command to enable the new virtual host: **sudo a2ensite projectlamp**
7. Disable the default website that comes installed with Apache. type: **sudo a2dissite 000-default**
8. Esure your configuration file doesn’t contain syntax errors, run: **sudo apache2ctl configtest**
9. Finally, reload Apache so these changes take effect: **sudo systemctl reload apache2**
![1667219014766](https://user-images.githubusercontent.com/76660222/203966055-a90c0883-f87d-4776-9d07-bc46fc695314.png)

10. The website is active, but the web root /var/www/projectlamp is still empty. Create an index.html file in that location so that we can test that the virtual host works as expected: **sudo echo 'Hello LAMP from hostname' $(curl -s [http://169.254.169.254/latest/meta-data/public-hostname](http://169.254.169.254/latest/meta-data/public-hostname)) 'with public IP' $(curl -s [http://169.254.169.254/latest/meta-data/public-ipv4](http://169.254.169.254/latest/meta-data/public-ipv4)) > /var/www/projectlamp/index.html**

11. Relaod the public IP to see changes to the apache2 default page.

 ### STEP 5 — ENABLE PHP ON THE WEBSITE

 #### Steps
1. With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php file. To make index.php file tak precedence need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive.
2. Run: **sudo vim /etc/apache2/mods-enabled/dir.conf** then: **#Change this: #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm #To this: DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm**
3. Save and close file.
4. Next, reload Apache so the changes take effect, type: **sudo systemctl reload apache2**
5. Finally, we will create a PHP script to test that PHP is correctly installed and configured on your server. Create a new file named index.php inside the custom web root folder, run: **vim /var/www/projectlamp/index.php**
6. This will open a blank file. Add the PHP code: **<?php phpinfo();**
7. Save and close the file, then refresh the page to see changes

![1667219811593](https://user-images.githubusercontent.com/76660222/203966114-b8a43b45-97f0-46b2-b19d-cd507ba2cbfd.png)


      
