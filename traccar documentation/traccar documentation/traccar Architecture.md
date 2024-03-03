
title: traccar Architecture
created at: Sat May 01 2021 14:03:23 GMT+0000 (Coordinated Universal Time)
updated at: Wed Aug 18 2021 02:17:15 GMT+0000 (Coordinated Universal Time)
---

# traccar Architecture

# Traccar Architecture

![media_traccar%20Architecture/OhV10~S_K-architecture.svg](media_traccar%20Architecture/OhV10~S_K-architecture.svg)

## Netty pipeline

Traccar system is based on the Netty network framework. The framework is an asynchronous event-driven network application framework which enables quick and easy development of network applications such as protocol servers.For each network channel or connection Traccar creates a pipeline of event handlers. Incoming messages from GPS devices are received as binary buffers and are separated into frames, decoded into an internal position model and eventually stored in the database. Outgoing messages (commands) are going in the opposite direction and are starting as an internal command model and eventually get converted into binary buffers that are sent to devices. Each protocol has its own pipeline, but most of the supported protocol include following main handlers in their pipelines:

-   Frame decoder (only TCP protocols) – splits incoming buffer into full single frames/messages, which can contain one or more location data points
-   String encoder (only string based protocols) – converts outgoing text message into a network buffer
-   String decoder (only string based protocols) – converts incoming network buffer into a text message ready for parsing
-   Protocol encoder – converting universal command model into a message format specific to the protocol
-   Protocol decoder – converting message in protocol-specific format into a one or several universal position objects
-   Utility handlers – range from handlers calculating travelled distance to handlers that perform reverse geocoding
-   Event handlers – generate events based on the information in the position object
-   Data handler – stores decoded data in the database
-   Main handler – responsible for error handling, logging and network connection management

Pipeline for each protocol is configured in the corresponding protocol class, which also defines additional protocol-specific configuration, including list of supported commands.

## Events and notifications

Events can be reported directly by a GPS device, or events can be generated on the server side based on specific data and conditions. All events, except for the connection status events, are generated in network pipeline handlers based on the data in the position model.Generated events are delivered to appropriate users via following channels:

-   Email – via SMTP service
-   SMS – via SMPP service
-   Web notification – via active WebSocket connection
-   Push notification – via Firebase API

Delivery logic for each channel is implemented in a corresponding Notificator class. Notificators and be enabled and disabled in the configuration file.

## Database

Server can be configured to work with almost any SQL database engine, including popular options like MySQL, PostgreSQL, Microsoft SQL Server and Oracle.Initial database schema creation and subsequent database schema upgrade migrations are done using Liquibase library. It allows to define schema in universal format in changelog XML files and generate database-specific SQL queries at runtime.Traccar system automatically generates most of the SQL queries for data insertion or extraction, but any query can also be overridden through the configuration file. It gives more flexibility and allows performance optimisation to achieve optimal results and balance between speed and utilisation of system resources.For fast access to the data, most of current information is cached internally in memory. Cache is updated only on incoming data from GPS devices or API calls that affect specific data. Even on updates cache is not re-loaded from database, but instead updated based on available in-memory objects. This creates a potential scalability and synchronisation problem for deploying multiple instances of Traccar.

## Web server

Traccar system includes embedded Jetty web server. Jetty is a stable and mature implementation of Java HTTP server and Servlet container. It is used in many popular products and frameworks.In Traccar system Jetty is used to serve following two main components:

-   Web API
-   Web application

Following sections describe each component in more details.

## Web API

Interface consists of the two main parts:

-   REST API
-   WebSocket

REST API is implemented using standard Java EE API for RESTful web services. Each model in the system has its own dedicated endpoint. Most URL endpoints accept following methods:

-   GET – retrieve a collection of objects based on user access and / or query parameters
-   POST – add new object
-   PUT – update existing object
-   DELETE – remove object

In addition to REST API, which only allows client driven request-based usage, Traccar provides WebSocket endpoint to get instant updates from the server. It is used for device status updates, location updates and event notifications.Both REST API and WebSocket connection use same authentication and authorisation mechanisms. For more information about API and security see Traccar API documentation.

## Web application

Traccar system includes web application for managing users, devices and other entities. Web app relies on the API described above.Application is based on the Sencha ExtJS framework and OpenLayers for map view. Architecture utilises MVC pattern with following major app components:

-   Models – represent data models
-   Stores – data storage and API implementation
-   Views – describe and configure widgets
-   Controllers – handle events and update views

Web app is served as a set of static files. Third party libraries and assets are loaded through CloudFlare CDN network to improve performance and reduce load on the server.

<https://www.traccar.org/architecture/>

          