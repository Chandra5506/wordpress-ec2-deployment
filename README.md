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

