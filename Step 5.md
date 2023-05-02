# STEP 5 – TESTING PHP WITH NGINX

At this point, our LAMP stack is completely installed and fully operational.

We can test it to validate that Nginx can correctly hand .php files off to our PHP processor.

I will do this by creating a test PHP file in my document root. I will open a new file called info.php within my document root in your text editor:

```
sudo nano /var/www/projectLEMP/info.php
```
I will type or paste the following lines into the new file. This is valid PHP code that will return information about my server:
```
<?php
phpinfo();
```
I can now access this page in your web browser by visiting the domain name or public IP address I’ve set up in my Nginx configuration file, followed by /info.php:
```
http://`server_domain_or_IP`/info.php
```
After checking the relevant information about my PHP server through that page, it’s best to remove the file we created as it contains sensitive information about our PHP environment and our Ubuntu server. We can use rm to remove that file:
```
sudo rm /var/www/your_domain/info.php
```
