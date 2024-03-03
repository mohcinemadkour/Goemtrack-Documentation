
title: Add Secure Connection
created at: Sat Feb 27 2021 19:56:22 GMT+0000 (Coordinated Universal Time)
updated at: Mon Aug 14 2023 13:23:45 GMT+0000 (Coordinated Universal Time)
---

# Add Secure Connection

Traccar serves web interface and API using regular HTTP protocol which does not use any encryption. This guide provides instructions on how to configure Traccar to use secure HTTPS protocol with SSL/TLS encryption of all traffic. Examples are for Ubuntu and other Debian-based systems only, but the general idea can be applied to all platforms. For Windows system you can follow [this blog post from Freek](https://freek.ws/2017/12/09/tutorial-how-to-secure-traccar-with-ssl-https-for-free-using-iis-and-lets-encrypt-on-windows-server/).

Traccar does not support secure connection out of the box, but a proxy server can be used to tunnel all data through secure protocol. In this guide we will use Apache server with proxy module.

First step is to install Apache server and enable required modules:

    sudo apt-get install ssl-cert apache2
    sudo a2enmod ssl
    sudo a2enmod proxy_http
    sudo a2enmod proxy_wstunnel
    sudo service apache2 restart

As a next step we need to add new site configuration:

    sudo nano /etc/apache2/sites-available/traccar.conf

Content for the site configuration (replace "demo.traccar.org" with your domain):

    <IfModule mod_ssl.c>
            <VirtualHost _default_:443>

                    ServerName demo.traccar.org
                    ServerAdmin webmaster@localhost

                    DocumentRoot /var/www/html

                    ProxyPass /api/socket ws://localhost:8082/api/socket
                    ProxyPassReverse /api/socket ws://localhost:8082/api/socket

                    ProxyPass / http://localhost:8082/
                    ProxyPassReverse / http://localhost:8082/

                    SSLEngine on
                    SSLCertificateFile /etc/ssl/certs/ssl-cert-snakeoil.pem
                    SSLCertificateKeyFile /etc/ssl/private/ssl-cert-snakeoil.key

            </VirtualHost>
    </IfModule>

Enable site and restart Apache service:

    sudo a2ensite traccar
    sudo service apache2 restart

To get a valid SSL certificate you need to have a domain name. Check our documentation on how register and to configure a [custom domain name](https://www.traccar.org/domain-name/) with Traccar.

After you configured a domain name, you can generate an SSL certificate for your server using [Let’s Encrypt service](https://certbot.eff.org/).

### Traccar in subdirectory (non root path)

If you want Traccar to be in a subdirectory, you also need to adjust cookies path. Here is a proxy configuration example:

    ProxyRequests off

    ProxyPass /gps/api/socket ws://localhost:8082/api/socket
    ProxyPassReverse /gps/api/socket ws://localhost:8082/api/socket

    ProxyPass /gps/ http://localhost:8082/
    ProxyPassReverse /gps/ http://localhost:8082/
    ProxyPassReverseCookiePath / /gps/

    Redirect permanent /gps /gps/

### Redirect unsecure connections

If you want to redirect HTTP to HTTPS&#x3A;

    sudo a2enmod rewrite
    sudo a2dissite 000-default
    sudo nano /etc/apache2/sites-available/traccar.conf

Add following lines to the configuration:

    <VirtualHost *:80>
      ServerName demo.traccar.org
      Redirect / https://demo.traccar.org/
    </VirtualHost>

Restart Apache server:

    sudo service apache2 restart

          