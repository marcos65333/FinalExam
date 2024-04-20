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

![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570461/c5999dde-352a-4182-b3a1-35cc289c7df9)


Replace ip_nagios_server with the actual IP address of your Nagios server.
    
    command[check_sda]=/usr/lib/nagios/plugins/check_disk -w 20% -c 10% -p /

![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570461/191bb9c4-95e3-43d8-9b95-e24574c2bf59)



Review your commands in the file and modify the disk command so that you can see all the remaining space on your server.



## 4 Step
After making configuration changes, restart the NRPE service:

    sudo /etc/init.d/nagios-nrpe-server restart


## Now, on our Nagios server, we will do the following:
Create the “servers” Directory:
Create a directory named “servers” within the path

    cd /usr/local/nagios/etc/

    mkdir servers

    cd servers
Create the “clients.cfg” File:

    nano clients.cfg

Add the following configuration for the monitored client (replace placeholders with actual values):

    define host {
        use                     linux-server
        host_name               client
        alias                   client
        address                 <IP of the server to be monitored>
        max_check_attempts      5
        check_period            24x7
        notification_interval   30
        notification_period     24x7
    }

    define service {
        use                     generic-service
        host_name               client
        service_description     HTTP
        check_command           check_http!-H <IP of the page> -p <port of the page>
        notifications_enabled   1
    }

    define service {
        use                     generic-service
        host_name               client
        service_description     Connected Users
        check_command           check_nrpe!check_users
        notifications_enabled   1
    }    

    define service {
        use                     generic-service
        host_name               client
        service_description     Disk Space (sd)
        check_command           check_nrpe!check_sda
        notifications_enabled   1
    }

    define service {
        use                     generic-service
        host_name               client
        service_description     Zombie Processes
        check_command           check_nrpe!check_zombie_procs
        notifications_enabled   1
    }

    define service {
        use                     generic-service
        host_name               client
        service_description     Total Processes
        check_command           check_nrpe!check_total_procs
        notifications_enabled   1
    }
