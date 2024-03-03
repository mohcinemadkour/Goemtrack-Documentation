
title: Server instructions
created at: Mon May 10 2021 16:57:39 GMT+0000 (Coordinated Universal Time)
updated at: Wed Aug 18 2021 02:27:25 GMT+0000 (Coordinated Universal Time)
---

# Server instructions

-   **Create Droplet**

    -   Create new droplet at your account on digitalocean.com
    -   Save credential
    -

-   **Changing port**
    -   change port from 8082 to 80
    -   after changing port on conf/default.xml (web.port)
    -   restrat traccar
    -   if log problem:
        -   2021-01-23 23:58:59 INFO: Waiting for changelog lock....
    -   run in mysql:
        -   update DATABASECHANGELOGLOCK set locked = 0;
    -   (<https://www.traccar.org/forums/topic/waiting-for-changelog-lock-loop/>)
    -   (<https://www.traccar.org/forums/topic/liquibase-waiting-for-changelog-lock/>)
    -   (<https://www.traccar.org/forums/topic/how-to-remove-lock-databasechangeloglock-default-h2-database/>)

          