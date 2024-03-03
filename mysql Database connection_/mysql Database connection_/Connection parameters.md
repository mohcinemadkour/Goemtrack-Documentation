
title: Connection parameters
created at: Tue Jan 19 2021 03:01:10 GMT+0000 (Coordinated Universal Time)
updated at: Mon Aug 14 2023 15:05:57 GMT+0000 (Coordinated Universal Time)
---

# Connection parameters

Out of the box, MySQL will only allow access from the localhost address 127.0.0.1. To change this, you need to open the _/etc/mysql/mysql.conf.d/mysqld.cnf_ file and change the line:

    bind-address = 127.0.0.1

to:

    bind-address = 0.0.0.0

Save and close that file. Restart the MySQL server with the command:

    systemctl restart mysql.service

## Step two: Granting access to the user

Let's say you have your WordPress server set up (running on IP address 192.168.1.100) to access a MySQL database named wordpressdb on the MySQL server with user wpadmin. On the MySQL server, you must grant access to the wordpressdb to that user from that IP address. Here's how to grant the user access (I'm assuming you already created the user wpadmin on the MySQL server and given it password %u#098Tl3).

1.


    GRANT ALL ON wordpressdb.* TO 'wpadmin'@'192.168.1.100' IDENTIFIED BY '%u#098Tl3' WITH GRANT OPTION;

1.
2.  Flush the MySQL privileges with the command _FLUSH PRIVILEGES;_
3.  Exit out of the MySQL prompt with the command _exit;_

Your WordPress instance (set up with the proper user credentials for the database) should be able to use the remote MySQL server as its database host.

Congratulations! You successfully set up MySQL for remote connections.

## Keep it secure

Although you can open MySQL for connections from remote servers, you should only grant privileges for select users to avoid possible security breaches. Also, be sure those users use very strong passwords. When you combine that with keeping your MySQL server up to date, you should be good to go.

<https://www.techrepublic.com/article/how-to-set-up-mysql-for-remote-access-on-ubuntu-server-16-04/>

and

<https://www.techrepublic.com/article/how-to-connect-to-a-remote-mysql-database-with-dbeaver/>

**Or **

One has to create a `new MySQL User` and assign privileges as below in `Query prompt` via phpMyAdmin or command prompt:

    CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
    GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost' WITH GRANT OPTION;
    CREATE USER 'username'@'%' IDENTIFIED BY 'password';
    GRANT ALL PRIVILEGES ON *.* TO 'username'@'%' WITH GRANT OPTION;
    FLUSH PRIVILEGES;

Once done with all four queries, it should connect with `username / password`

          