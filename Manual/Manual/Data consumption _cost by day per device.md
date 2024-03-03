
title: Data consumption /cost by day per device
created at: Sat Feb 27 2021 21:18:02 GMT+0000 (Coordinated Universal Time)
updated at: Mon Aug 14 2023 13:23:45 GMT+0000 (Coordinated Universal Time)
---

# Data consumption /cost by day per device

One message with GPS info is less than 100 bytes (GPS103 protocol), but if you add communication protocol overhead (establishing connection, headers etc) it would probably be slightly more than 100 bytes. Then you need to add heartbeat messages (about 20 bytes long). So, let's say roughly 200 bytes per message, then the device would use 25KB of data per hour.Note that this calculation assumes ideal connection. If connection is lost most likely your telecom operator will charge minimum chargeable unit (which I guess is 20KB in your case). This means you can get changed for 20KB even if you used only 100 bytes if the reception is poor.

          