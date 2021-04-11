### Step 1 : Check the server status

###### Ping your server

Before proceeding with the mentioned steps,First we need to check if you are able to access the server itself. 
Sometimes the Server itself may have went down.You can verify this with ping and ssh command

`ping your_server_ip`

If you able ping your server and its UP,You will get the output as below

    e2e@compaqlaptop:~$ ping 8.8.8.8
    
    PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
    
    64 bytes from 8.8.8.8: icmp_seq=1 ttl=57 time=18.0 ms
    
    64 bytes from 8.8.8.8: icmp_seq=2 ttl=57 time=20.1 ms
    
    64 bytes from 8.8.8.8: icmp_seq=3 ttl=57 time=21.3 ms
    
    ^C
    
    --- 8.8.8.8 ping statistics ---
    
    3 packets transmitted, 3 received, 0% packet loss, time 2002ms
    
    rtt min/avg/max/mdev = 18.042/19.837/21.342/1.362 ms
    
    e2e@compaqlaptop:~$ 

> If your server is down,in that case you will get not get any ping.You can Check your server console for any error 
and restart your server. 
> **Note : You may sometimes not be able to ping the server even when your server is UP and this may be due to ping 
being disabled on your server.**

###### SSH to your server

You should also be able to SSH and login to the server to verify if its up and running fine,You can access your server 
via ssh with below command

    ssh username@xx.xx.xx.xx

if you are not able to login to your server,Chances are that your server is down or in hanged state and Check your 
server console for any error and restart your server.

### Step 2 : Check the Logs

Before tracking down any of the problems, We need to check the Logs first of our web server and related components. 
If we found any error logs or any suspicious logs on access logs, We will be able to identify the problems Precisely.

###### Apache

The logs will be usually present at directory `/var/log`. if you have an Apache server running on an Ubuntu server, 
by default the logs will be kept in `/var/log/apache2`. Check the files in this directory to see what kind of error 
messages are being generated.If you’re using a distribution that refers to Apache as httpd by default the logs will be 
kept at

    /var/log/httpd.log

###### NGINX

If you are using NGINX as your web server, The logs are usually located at below location

    /var/log/nginx/access.log
    /var/log/nginx/error.log
    /var/log/nginx/nginx_error.log
    /var/log/nginx/access_error.log

Check the files in this directory to see what kind of error messages are being generated. Alternately you can also 
check the web-server configuration files if you have configured a manual path for logs.

To check the latest logs generated from the server,You can run below tail command as shown in below example

    tail -f /var/log/nginx/access.log
    tail -f /var/log/httpd.log

### Step 3 : Make sure your web server is running

You can verify if your services are up and running fine,One method to check if the services are running is 
distribution’s preferred method is to check with below shared command.

Use status command to check if the service is up or not.If the service is not running you can start it with below start 
command

###### Apache

If you’re using a distribution that refers to Apache as Apache2,commands to use apache2 functionality is as below

    service apache2 start
    service apache2 stop
    service apache2 restart
    service apache2 reload
    service apache2 status

If you’re using a distribution that refers to Apache as httpd, then the commands are as follows:

    service httpd start
    service httpd stop
    service httpd restart
    service httpd reload
    service httpd status

###### NGINX

The commands to use Nginx functionality is as below

    service nginx start
    service nginx stop
    service nginx restart
    service nginx reload
    service nginx status

### Step 4 : Verifying the Syntax of Web server

If your web server is failing to start,this means that there can be an issue with your configuration file.

> Each of these web servers also provide you with the ability to check the configuration syntax of your files.

Both Apache and NGINX need correct directive syntax in order for the files to be read. The configuration files are 
located as below:

###### Apache

Debian and Ubuntu distributions: 

`/etc/apache2/`

Fedora, CentOS distributions: 

`/etc/httpd/`

To check the syntax of your Apache configuration files without needing to restart the server, you can run the following 
command on Debian and Ubuntu systems

    apache2ctl -t
    httpd -t

###### NGINX

`/etc/nginx/`

To check configuration Syntax on NGINX, use below command

    nginx -t

Once you run the above command you will get message like Syntax OK or Test is successful. This means that your there is 
no error at your web server configuration.if you get message like “test failed”,There is an invalid argument which are 
provided in the configuration file and that needs to be edited.

### Step 5 : Is your Database back-end running Fine

If you have configured your site to connect with database back-end like MySQL, PostreSQL, MongoDB, etc. you need to make sure that it is up and running.You can do this as you checked for Web server.

Run the below command to verify if your database MySQL/MongoDB whichever you are running.

    service mysql status
    service mysqld status
    service mongod status

Alternately you can also verify with below netstat command

    netstat -ntlp | grep mysql

You will receive output as below,if your MySQL is up and running.

    tcp 0 0 127.0.0.1:3306 0.0.0.0:* LISTEN 3356/mysqld

### Step 6 : Verify if your Web/App server is able to connect to Database backend

Even though if your web server and Database server is Up and running fine,Sometime we may face issue with its 
connectivity as your Application will not be able to connect to Database successfully.

You can test whether the file has the correct information by trying to connect to the database manually by changing appropriate Value in below command

    mysql -hDB_Host -uDB_USER -pDB_PASSWORD 

### Step 7: Make sure the Ports are open

Even if the all the configuration and connectivity are right,Some times you not be able to access the site since the 
configured ports must be accessible.Web servers run on port 80 for normal web traffic and use port 443 for traffic 
encrypted with SSL.

You can check whether if the configured ports are open with `telnet` command

    telnet your_server_ip 80
    telnet your_server_ip 443

You will get output like below if your ports are open

    e2e@compaqlaptop:~$ telnet xx.xx.xx.xx 80
    Trying xx.xx.xx.xx…
    Connected to xx.xx.xx.xx.
    Escape character is ‘^]’.

You can also verify if your App/Web server is able to connect to your database port on back-end. MySQL server by 
default run on port 3306

    telnet your_database_server_ip 3306

If your web ports or Database ports is not accessible, you should look at your **firewall configuration**. You may need 
to open up port 80,port 443 or Port 3306 respectively.

#### Step 9: Verifying the DNS Setting

You also need to make sure that your domain is correctly pointed to Server IP. If you can access the site with IP and 
not with your domain name,you may need to take a look at your DNS settings.

You can verify if your site is pointed to the right IP with below dig command

    dig A example.com +short

You will get the output as below

    e2e@compaqlaptop:~$ dig A example.com +short
    xx.xx.xx.xx
    e2e@compaqlaptop:~$

Apart from that, check your Apache virtual host files or the NGINX server block files to make sure they are configured 
to respond to requests for your domain.





















