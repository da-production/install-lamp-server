# install-lamp-server

# Installation:

1. make sure your server is updated run 
```
apt update
```
2.
```
apt-get install -y apache2
```
3.
```
apt-get install -y php libapache2-mod-php php-mysql
```
4.
```
service apache2 reload
```
5.
```
apt-get install -y mysql-server
```
6.
```
apt-get install -y phpmyadmin
apt install phpmyadmin php-mbstring php-gettext
phpenmod mbstring
systemctl restart apache2
```
7.
```
mysql
```
8.
```
mysql > SELECT user,authentication_string,plugin,host FROM mysql.user;
```
```
Output
+------------------+-------------------------------------------+-----------------------+-----------+
| user             | authentication_string                     | plugin                | host      |
+------------------+-------------------------------------------+-----------------------+-----------+
| root             |                                           | auth_socket           | localhost |
| mysql.session    | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
| mysql.sys        | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
| debian-sys-maint | *8486437DE5F65ADC4A4B001CA591363B64746D4C | mysql_native_password | localhost |
| phpmyadmin       | *5FD2B7524254B7F81B32873B1EA6D681503A5CA9 | mysql_native_password | localhost |
+------------------+-------------------------------------------+-----------------------+-----------+
5 rows in set (0.00 sec)
```
9.
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Pass*2020';
```
```
FLUSH PRIVILEGES;
```
```
SELECT user,authentication_string,plugin,host FROM mysql.user;
```
```
Output
+------------------+-------------------------------------------+-----------------------+-----------+
| user             | authentication_string                     | plugin                | host      |
+------------------+-------------------------------------------+-----------------------+-----------+
| root             | *DE06E242B88EFB1FE4B5083587C260BACB2A6158 | mysql_native_password | localhost |
| mysql.session    | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
| mysql.sys        | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
| debian-sys-maint | *8486437DE5F65ADC4A4B001CA591363B64746D4C | mysql_native_password | localhost |
| phpmyadmin       | *5FD2B7524254B7F81B32873B1EA6D681503A5CA9 | mysql_native_password | localhost |
+------------------+-------------------------------------------+-----------------------+-----------+
5 rows in set (0.00 sec)
```
10.Configuring Password Access for a Dedicated MySQL User
```
sudo mysql
```
```
mysql -u root -p
```
From there, create a new user and give it a strong password:
```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION;
```
Following that, exit the MySQL shell:
```
exit
```
You can now access the web interface by visiting your server’s domain name or public IP address followed by /phpmyadmin:
```
http://your_domain_or_IP/phpmyadmin
```
