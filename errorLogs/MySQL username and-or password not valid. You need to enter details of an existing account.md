# MySQL username and/or password not valid You need to enter details of an existing account

![image](https://user-images.githubusercontent.com/75790837/143217772-b2f34d65-0559-4610-a7e5-26f216de751a.png)

This was the main issue I faced, and lost time on. It appeared at the end of the NextCloud configuration, when creating my admin NextCloud account and linking my MariaDB to NextCloud.

_**Root**_: From whatever reason, NextCloud cannot find the user account of the MariaDB database you mentionned...

_**Solution**_: 
To solve the issue, I **deleted my MariaDB data base** (originally created via the DSM interface) and created a new database using the terminal.
The idea is to GRANT ALL priviledge to the user. I did this at the beggining and added the FLUSH PRIVILEGES and it worked....

1- Delete your MariaDB database.

2- Access MariaDB via the terminal with the following command `mysql -u root -p`

3- Run the following lines one after the others.
```
CREATE DATABASE your_NextCloud_Data_Base_Name; #replace your_NextCloud_Data_Base_Name

CREATE USER 'your_Next_Cloud_User'@'localhost' IDENTIFIED BY 'your_Password'; #replace your_Next_Cloud_User

GRANT ALL ON your_NextCloud_Data_Base_Name .* TO 'your_NextCloud_User'@'localhost'; #your_NextCloud_User

FLUSH PRIVILEGES;
EXIT;
```

_**sources**_:
[#21690](https://github.com/nextcloud/server/issues/21690)
