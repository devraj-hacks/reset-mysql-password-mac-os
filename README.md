## Reset mysql root password in Mac OS:

First Stop MySQL:
------
1. Go to: 'System Preferences' >> 'MySQL' and stop MySQL

OR,

1) sudo /usr/local/mysql/support-files/mysql.server start
2) sudo /usr/local/mysql/support-files/mysql.server stop
3) sudo /usr/local/mysql/support-files/mysql.server status

Process to Reset MySQL Root Pass in Mac:
----------------------
1. Make sure you have Stopped MySQL first (above).
2. Run the server in safe mode with privilege bypass: `sudo mysqld_safe --skip-grant-tables`
3. In a new window connect to the database, set a new password and flush the permissions & quit: `mysql -u root`
4. **For MySQL older than MySQL 5.7 use**: 
   ```sql
   UPDATE mysql.user SET Password=PASSWORD('rootpass') WHERE User='root';
   ``` 

   **For MySQL 5.7+ use:** 
   ```sql 
   UPDATE mysql.user SET authentication_string=PASSWORD("rootpass") WHERE User='root';
   ```	
   
5. Now flush privileges: 
   ```sql
   FLUSH PRIVILEGES;
   ```
6. Restart MySQL server.
7. **More info:** http://stackoverflow.com/questions/6474775/setting-the-mysql-root-user-password-on-os-x
