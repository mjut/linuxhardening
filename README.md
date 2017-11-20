# Linux Hardening

https://www.ubuntu.com/download/server



## Change Apache default port to a custom port

sudo vi /etc/apache2/ports.conf

Find the following line:

Listen 80

And change it to a random number of your choice, for example 8090.

Listen 8090

This entry make the server to accept connections on port 8090 on all interfaces. To make the server accept connections on port 8090 for a specific interface, just include the corresponding network interface’s IP address as shown below.

Listen 192.168.1.101:8090

This will be helpful if your server has multiple IP addresses or network interfaces.

Save and close the file.

Additionally, in Ubuntu and Debian, you will likely also have to change the port number in /etc/apache2/sites-enabled/000-default.conf file too.

sudo vi /etc/apache2/sites-enabled/000-default.conf

Find the following line and change the port number.

<VirtualHost *:8090>

Save and close the file.

Then, restart Apache service to take effect the changes.

sudo systemctl restart apache2







## Resources
- https://www.computerworld.com/article/3144985/linux/linux-hardening-a-15-step-checklist-for-a-secure-linux-server.html
- https://mattwilcox.net/web-development/setting-up-a-secure-home-web-server-with-raspberry-pi

