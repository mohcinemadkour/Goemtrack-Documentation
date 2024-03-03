
title: install / Uninstall Traccar
created at: Tue Feb 02 2021 04:26:53 GMT+0000 (Coordinated Universal Time)
updated at: Mon Aug 14 2023 13:23:45 GMT+0000 (Coordinated Universal Time)
---

# install / Uninstall Traccar

## Install

-   [Download](https://www.traccar.org/download/) and extract the installer package
-   Execute **traccar.run** file
    -   `sudo ./traccar.run`
-   Start systemd service
    -   `sudo systemctl start traccar`

## **Uninstall**

Stop service:

sudo systemctl stop traccar.service

    Uninstall service:

sudo systemctl disable traccar.service

sudo rm /etc/systemd/system/traccar.service

sudo systemctl daemon-reload

    Remove traccar directory:

sudo rm -R /opt/traccar

          