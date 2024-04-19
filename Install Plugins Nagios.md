Installation of Plugins on the server want to monitor
============

## 1 Step:
Execute the following command to install NRPE and Nagios plugins:

    sudo apt-get install nagios-nrpe-server nagios-plugins

## 2 Step:
Open the NRPE configuration file:

    sudo nano /etc/nagios/nrpe.cfg

## 3 Step:
In this file, find the line containing allowed_hosts and add the IP address of your Nagios server. For example:

    allowed_hosts=127.0.0.1,ip_nagios_server

Replace ip_nagios_server with the actual IP address of your Nagios server.

## 4 Step
After making configuration changes, restart the NRPE service:

    sudo /etc/init.d/nagios-nrpe-server restart
