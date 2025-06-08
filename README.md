ICT171-Assignment 2
Cloud Server Project

Cloud-Hosted WordPress Deployment Report

Student: Chandra Chhetri

Student ID: 35381453

Website: https://easyaccountinggroup.com

Server IP: 52.65.119.7

1. Project Objective
The aim of this assignment is to demonstrate the deployment of a secure, cloud-hosted web server running WordPress on an EC2 Ubuntu instance, configured manually via Linux commands. The final product is a publicly accessible website for "Easy Accounting and Mortgage Services".
2. High-Level Process Overview
1. Launch EC2 instance on AWS
2. Connect via SSH
3. Install Apache, PHP, MariaDB
4. Secure MySQL and create WordPress DB/user
5. Download and configure WordPress
6. Set proper file permissions
7. Obtain SSL with Certbot
8. Configure Apache virtual hosts for HTTP/HTTPS
9. Attach domain (GoDaddy DNS)
10. Test access and document troubleshooting
2. WordPress Setup
Accessed https://easyaccountinggroup.com and completed the WordPress installation wizard.
- Site Title: Easy Accounting and Mortgage Services
- Username: admin
- Email: chandra_ctr@yahoo.com
- Search Engine Visibility: Disabled during setup
Pages created: Home, Accounting Services, Mortgage, Contact
3. Troubleshooting Notes
- DNS propagation delay caused site to show static HTML instead of WordPress (fixed by DNS flush)
- Certbot failed initially due to DNS misconfiguration (resolved after correct A record setup)
- Apache default index.html overrode WordPress until it was deleted
- Forced HTTPS redirect using Apache rules
4. Security Practices
- All unused ports are blocked via AWS Security Group
- SSL encryption enabled using Let's Encrypt
- File and directory permissions restricted
- MariaDB secured and isolated to localhost
6. Conclusion
The cloud-hosted WordPress site for Easy Accounting and Mortgage Services has been successfully deployed using a secure, manually configured EC2 Ubuntu instance. All operations including Apache, MariaDB, DNS, and SSL were completed via CLI and tested for functionality from public browsers.


3. Detailed Steps
Step 1: Launch EC2 Instance
•	EC2 Ubuntu 24.04 instance created.
•	Security Group configured to allow ports: 22 (SSH), 80 (HTTP), 443 (HTTPS) from 0.0.0.0/0.
•	Elastic IP allocated and assigned: 52.65.119.7

Step 2: SSH into EC2
ssh -i my-key.pem ubuntu@52.65.119.7

Step 3: Install Required Packages
sudo apt update && sudo apt install apache2 php php-mysql libapache2-mod-php mariadb-server curl unzip -y

Step 4: Secure MariaDB
sudo mysql_secure_installation
Prompts answered to:
•	Set root password: Yes
•	Remove anonymous users: Yes
•	Disallow root remote login: Yes
•	Remove test DB: Yes
•	Reload privileges: Yes

Step 5: Create WordPress Database & User
sudo mariadb
CREATE DATABASE wordpress;
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'Bunbury11$';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;

Step 6: Download and Configure WordPress
cd /tmp
curl -O https://wordpress.org/latest.tar.gz
sudo tar -xvzf latest.tar.gz
sudo cp -r wordpress/* /var/www/html/
Remove default index.html:
sudo rm /var/www/html/index.html
Copy and edit config:
cd /var/www/html
sudo cp wp-config-sample.php wp-config.php
sudo nano wp-config.php
Update with:
DB_NAME: wordpress
DB_USER: wpuser
DB_PASSWORD: Bunbury11$
DB_HOST: localhost

Step 7: Set Permissions
sudo chown -R www-data:www-data /var/www/html/
sudo find /var/www/html/ -type d -exec chmod 755 {} \;
sudo find /var/www/html/ -type f -exec chmod 644 {} \;

Step 8: Enable Apache Rewrite & SSL
sudo a2enmod rewrite ssl
sudo systemctl restart apache2

Step 9: Get SSL with Certbot
sudo apt install certbot python3-certbot-apache -y
sudo certbot --apache
•	Domain: easyaccountinggroup.com, www.easyaccountinggroup.com
•	Email: chandra_ctr@yahoo.com
•	Selected redirect to HTTPS

Step 10: Edit Apache Virtual Hosts
HTTP redirect (000-default.conf):
<VirtualHost *:80>
    ServerName easyaccountinggroup.com
    Redirect permanent / https://easyaccountinggroup.com/
</VirtualHost>
HTTPS config (000-default-le-ssl.conf):
<VirtualHost *:443>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html
    ServerName easyaccountinggroup.com
    Include /etc/letsencrypt/options-ssl-apache.conf
    SSLCertificateFile /etc/letsencrypt/live/easyaccountinggroup.com/fullchain.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/easyaccountinggroup.com/privkey.pem
</VirtualHost>
Reload:
sudo systemctl reload apache2
Step 11: DNS Setup (GoDaddy)
•	A record pointing to 52.65.119.7
•	TTL: 1 hour
________________________________________
4. WordPress Setup
•	Accessed https://easyaccountinggroup.com
•	Completed WP installation wizard:
o	Site Title: Easy Accounting and Mortgage Services
o	Username: admin
o	Email: chandra_ctr@yahoo.com
o	Search Engine Visibility: Disabled during setup
•	Added Homepage content based on Assignment 1:
o	Welcome section
o	Blog: Tailored content for small business clients
o	Pages created: Home, Accounting Services, Mortgage, Contact
________________________________________
5. Troubleshooting Notes
•	DNS propagation delay caused site to show static HTML instead of WordPress (fixed by DNS flush)
•	Certbot failed initially due to DNS misconfiguration (resolved after correct A record setup)
•	Apache default index.html overrode WordPress until it was deleted
•	Forced HTTPS redirect using Apache rules
________________________________________
6. Security Practices
•	All unused ports are blocked via AWS Security Group
•	SSL encryption enabled using Let's Encrypt
•	File and directory permissions restricted
•	MariaDB secured and isolated to localhost
________________________________________
7. Conclusion
The cloud-hosted WordPress site for Easy Accounting and Mortgage Services has been successfully deployed using a secure, manually configured EC2 Ubuntu instance. All operations including Apache, MariaDB, DNS, and SSL were completed via CLI and tested for functionality from public browsers.

