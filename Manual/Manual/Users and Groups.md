
title: Users and Groups
created at: Sun Jan 31 2021 03:11:03 GMT+0000 (Coordinated Universal Time)
updated at: Mon Aug 14 2023 13:23:45 GMT+0000 (Coordinated Universal Time)
---

# Users and Groups

Service administrator can:

-   Create one _manager_ user for every client
-   Set _user limit_ and _device limit_ according to the subscription. For example, 5 users and 50 devices.
-   Set _expiration time_ to limit subscription period.

## Main user roles

**_Admin_** - superuser that has full unlimited access to the whole Traccar server.

**_Manager_** - user with extended capabilities allowing him to manage his subset of users and register new ones.

**_User_** - ordinary user that can manipulate any of his own objects and add new ones.

\_\_

_**User limit **_- the limit on number of users that manager can have. Manager cannot add users more than his _user limit:_

    - If _user limit_ is set to **-1**, it means that manager has no limit.
    - If _user limit_ is set to **0**, it means that user is not a manager. The difference between _manager_ and _regular user_ is in their _user limit_ value. _Manager_ has limit not equals to 0
    -

**_Device limit_\*\*** \*\*- the limit for number of devices that user can have. User cannot add devices more than his _device limit_.

If _device limit_ is set to **-1**, it means that the user has no limit on number of devices.

If _device limit_ is set to **0**, it means that user cannot add any devices, but he can edit or remove existing ones.

**Token**

Create token to give access without password

<http://198.211.112.250/?token=hLBwObZbaBXoTr7jb6Hnvo0Q27LcQyG8>

Activate and deactivate token access as needed

## Devices names rules

          