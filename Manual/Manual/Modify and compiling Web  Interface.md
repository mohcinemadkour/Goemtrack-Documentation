
title: Modify and compiling Web  Interface
created at: Tue Feb 02 2021 04:00:57 GMT+0000 (Coordinated Universal Time)
updated at: Mon Aug 14 2023 13:23:45 GMT+0000 (Coordinated Universal Time)
---

# Modify and compiling Web Interface

# Modify web interface

If you want to modify web app you should get repo from GitHub, not installer.

    1. Download whole project from GitHub.

<https://github.com/traccar/traccar-web>

    2. Do your modifications.

    3. Compile minified version.

    4. Upload all files from web folder to your server.

# Build Web Interface

Web interface is written in JavaScript, so it doesn't require compiling, but release versions of Traccar use minified version where all files are combined into one and compressed.

If you modify web interface files, there are two deployment options:

-   Upload new files into the server web folder and use debug.html to load non-compressed version of the web interface
-   [Generate minified version ](https://www.traccar.org/build-extjs/)of the web interface using tools/minify.sh shell script

/root/bin/Sencha/Cmd

Compile minified version

There is a minify script in tools that you can use.

Minify ExtJS App

This document provides information on how to build a minified version of the extjs-based Traccar web app. Instuctions are provided for Ubuntu 20.04 operating system. If you are using different OS, you might need to adjust some commands. You can also use a VPS or a virtual machine with Ubuntu 20.04 to use commands as is.

First install required tools and dependencies available from Ubuntu repo:

sudo add-apt-repository ppa:openjdk-r/ppa

sudo apt update

sudo apt install -y git openjdk-11-jdk unzip

Then download and extract ExtJS SDK:

wget <http://cdn.sencha.com/ext/gpl/ext-6.2.0-gpl.zip>

unzip ext-\*-gpl.zip

Then download and install Sencha CDM command line tool:

wget <http://cdn.sencha.com/cmd/7.1.0.15/no-jre/SenchaCmd-7.1.0.15-linux-i386.sh.zip>

unzip SenchaCmd-\*.zip

sudo ./SenchaCmd-\*.sh

Now you can compile a minified version of the Traccar app:

traccar-web/tools/minify.sh

The output will be app.min.js file in the web folder.

          