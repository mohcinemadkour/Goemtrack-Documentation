
title: backup database and remove mysql and reinstall it and restore db
created at: Sun Aug 29 2021 02:51:36 GMT+0000 (Coordinated Universal Time)
updated at: Sun Aug 29 2021 03:00:58 GMT+0000 (Coordinated Universal Time)
---

# backup database and remove mysql and reinstall it and restore db

1-

mysqldump -u root -p –all-databases > C:\\MySQLBackup\\all_databases_20200424.sql

mysqldump -u root -p traccar > C:\\MySQLBackup\\all_databases_20200424.sql

2-

    sudo apt-get remove --purge mysql*
    sudo apt-get purge mysql*
    sudo apt-get autoremove
    sudo apt-get autoclean
    sudo apt-get remove dbconfig-mysql

3-

add use traccar on top of backup.sql

4-

    apt update && apt -y install unzip mysql-server
    mysql -u root --execute="ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root'; GRANT ALL ON *.* TO 'root'@'localhost' WITH GRANT OPTION; FLUSH PRIVILEGES; CREATE DATABASE traccar;"

5-

    mysql -u root -p < 08_28_21.sql

          