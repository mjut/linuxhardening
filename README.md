# Linux Hardening

https://www.ubuntu.com/download/server



## Change Apache default port to a custom port

`sudo vi /etc/apache2/ports.conf`

Find the following line:

`Listen 80`

And change it to a random number of your choice, for example 8090.

`Listen 8090`

This entry make the server to accept connections on port 8090 on all interfaces. To make the server accept connections on port 8090 for a specific interface, just include the corresponding network interface’s IP address as shown below.

`Listen 192.168.1.101:8090`

This will be helpful if your server has multiple IP addresses or network interfaces.

Save and close the file.

Additionally, in Ubuntu and Debian, you will likely also have to change the port number in /etc/apache2/sites-enabled/000-default.conf file too.

`sudo vi /etc/apache2/sites-enabled/000-default.conf`

Find the following line and change the port number.

`<VirtualHost *:8090>`
Save and close the file.

Then, restart Apache service to take effect the changes.
`sudo systemctl restart apache2`



## Firewall

    Allow SSH Connections

This will create firewall rules that will allow all connections on port 22, which is the port that the SSH daemon listens on. UFW knows what "ssh", and a bunch of other service names, means because it's listed as a service that uses port 22 in the /etc/services file.

We can actually write the equivalent rule by specifying the port instead of the service name. For example, this command works the same as the one above:

    sudo ufw allow 22

If you configured your SSH daemon to use a different port, you will have to specify the appropriate port. For example, if your SSH server is listening on port 2222, you can use this command to allow connections on that port:

    sudo ufw allow 2222

Now that your firewall is configured to allow incoming SSH connections, we can enable it.

### Enable UFW

To enable UFW, use this command:

    sudo ufw enable

You will receive a warning that says the "command may disrupt existing ssh connections." We already set up a firewall rule that allows SSH connections so it should be fine to continue. Respond to the prompt with y.

The firewall is now active. Feel free to run the sudo ufw status verbose command to see the rules that are set.




## Resources
- https://www.computerworld.com/article/3144985/linux/linux-hardening-a-15-step-checklist-for-a-secure-linux-server.html
- https://mattwilcox.net/web-development/setting-up-a-secure-home-web-server-with-raspberry-pi

