
title: mysql conf
created at: Sun Aug 29 2021 16:35:23 GMT+0000 (Coordinated Universal Time)
updated at: Sun Aug 29 2021 16:54:36 GMT+0000 (Coordinated Universal Time)
---

# mysql conf

If having problem: "**Communications link failure The last packet sent successfully to the server was 0 milliseconds ago. The driver has not received any packets from the server. Connection refused: connect Connection refused: connect**"

Look for \*.conf

sudo find / -name "\*.cnf"

My config file was in :

/etc/mysql/mysql.conf.d/mysqld.cnf

change

bind-address="127.0.0.1"

to

bind-address="0.0.0.0"

if having problem :"**public key retrieval is not allowed**"

For **DBeaver** users:

1.  Right click your connection, choose "Edit Connection"
2.  On the "Connection settings" screen (main screen) click on "Edit Driver Settings"
3.  Click on "Driver properties"
4.  Right click the "user properties" area and choose "Add new property"
5.  Add two properties: "useSSL" and "allowPublicKeyRetrieval"
6.  Set their values to "false" and "true" by double clicking on the "value" column

          