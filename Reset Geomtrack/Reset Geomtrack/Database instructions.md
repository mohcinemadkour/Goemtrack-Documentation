
title: Database instructions
created at: Mon May 10 2021 16:20:50 GMT+0000 (Coordinated Universal Time)
updated at: Sun Aug 29 2021 15:26:16 GMT+0000 (Coordinated Universal Time)
---

# Database instructions

1 Make sure you have access to database from DBeaver

One has to create a `new MySQL User` and assign privileges as below in `Query prompt` via phpMyAdmin or command prompt:

    CREATE USER 'mohcine3'@'localhost' IDENTIFIED BY 'password';
    GRANT ALL PRIVILEGES ON *.* TO 'mohcine3'@'localhost' WITH GRANT OPTION;
    CREATE USER 'mohcine3'@'%' IDENTIFIED BY 'password';
    GRANT ALL PRIVILEGES ON *.* TO 'mohcine3'@'%' WITH GRANT OPTION;
    FLUSH PRIVILEGES;

Once done with all four queries, it should connect with `username / password`

Problem creating username: [ERROR 1396 (HY000): Operation CREATE USER failed for 'jack'@'localhost'](https://stackoverflow.com/questions/5555328/error-1396-hy000-operation-create-user-failed-for-jacklocalhost)

    drop user admin@localhost;
    flush privileges;
    create user admin@localhost identified by '_admins_password_'

2- Dump the traccar database to local through Dbeaver

    - connect through DBeaver to the old server / mysql database
    -

![image.png](media_Database%20instructions/PZYW~GJ8Eg-image.png)

    -Backup the whole database to local file

![image.png](media_Database%20instructions/NRI9x~JJs-image.png)

methode 2: using mysql command

save the backup command : scp [root@162.243.172.230](mailto:root@162.243.172.230):/opt/backup_05-10-21 .

          