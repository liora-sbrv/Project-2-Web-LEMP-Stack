# STEP 1 – INSTALLING THE NGINX WEB SERVER

In order to display web pages to our site visitors, I'm going to employ Nginx, a high-performance web server. I’ll use the apt package manager to install this package.

I start off by updating my server’s package index. Following that, I will use apt install to get Nginx installed:

```
sudo apt update
sudo apt install nginx
```
When prompted, I entered Y to confirm that I want to install Nginx. Once the installation is finished, the Nginx web server will be active and running on my Ubuntu 20.04 server.

To verify that nginx was successfully installed and is running as a service in Ubuntu, run:

```
sudo systemctl status nginx
```
If it is green and running, then you did everything correctly – you have just launched your first Web Server in the Clouds!

Before I can receive any traffic by our Web Server, I need to open TCP port 80 which is default port that web brousers use to access web pages in the Internet.

I have TCP port 22 open by default on my EC2 machine to access it via SSH, so I need to add a rule to EC2 configuration to open inbound connection through port 80:

My server is running and I can access it locally and from the Internet (Source 0.0.0.0/0 means ‘from any IP address’).

First, let's try to check how I can access it locally in my Ubuntu shell, run:

```
curl http://localhost:80
or
curl http://127.0.0.1:80
```
These 2 commands above actually do pretty much the same – they use ‘curl’ command to request our Nginx on port 80 (actually I can even try to not specify any port – it will work anyway). The difference is that: in the first case I try to access my server via DNS name and in the second one – by IP address (in this case IP address 127.0.0.1 corresponds to DNS name ‘localhost’ and the process of converting a DNS name to IP address is called "resolution"). I will touch DNS in further lectures and projects.

As an output I can see some strangely formatted test, do not worry, I just made sure that our Nginx web service responds to ‘curl’ command with some payload.

Now it is time for me to test how my Nginx server can respond to requests from the Internet.

```
http://<Public-IP-Address>:80
```
Another way to retrieve  Public IP address, other than to check it in AWS Web console, is to use following command:

```
curl -s http://169.254.169.254/latest/meta-data/public-ipv4
```

The URL in browser shall also work if I do not specify port number since all web browsers use port 80 by default.
