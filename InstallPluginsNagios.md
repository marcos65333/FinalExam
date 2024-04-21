Installation of Plugins on the server want to monitor
============

## Step 1:
Execute the following command to install NRPE and Nagios plugins:

    sudo apt-get install nagios-nrpe-server nagios-plugins

## Step 2:
Open the NRPE configuration file:

    sudo nano /etc/nagios/nrpe.cfg

## Step 3:
In this file, find the line containing allowed_hosts and add the IP address of your Nagios server. For example:

    allowed_hosts=127.0.0.1,ip_nagios_server

![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570461/c5999dde-352a-4182-b3a1-35cc289c7df9)


Replace ip_nagios_server with the actual IP address of your Nagios server.
    
    command[check_sda]=/usr/lib/nagios/plugins/check_disk -w 20% -c 10% -p /

![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570461/191bb9c4-95e3-43d8-9b95-e24574c2bf59)



Review your commands in the file and modify the disk command so that you can see all the remaining space on your server.



## Step 4:
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
    
> [!NOTE]
> define host:
> 
> This directive defines a host to be monitored. A host can be a physical or virtual computer.
> 
> The components of this definition are:
> 
>   use: Specifies the template to be used for configuring this host. In this case, it’s linux-server.
> 
>      host_name: The name of the host, which in this case is client.
> 
>      alias: A friendlier alias or description for the host.
> 
>      address: The IP address of the server to be monitored.
> 
>      max_check_attempts: The maximum number of check attempts before considering the host as unavailable.
> 
>      check_period: The time period during which checks will be performed (in this case, 24x7, meaning all the time).
> 
>      notification_interval: The interval between problem notifications.
> 
>      notification_period: The time period during which notifications will be sent (also 24x7 in this case).
> 
> define service:
> 
> This directive defines a service that runs on the host.
> 
> Services can be actual services (like POP, SMTP, HTTP) or metrics related to the host (ping response, connected users, disk space, etc.).
> 
> The components of this definition are:
> 
>   use: The template to be used for configuring this service (in this case, generic-service).
> 
>      host_name: The name of the host to which this service applies (in this case, client).
> 
>      service_description: A description of the service (e.g., “HTTP”).
> 
>      check_command: The command to be used for checking the service (e.g., check_http!-H <IP of the page> -p <port of the page>).
> 
>      notifications_enabled: Whether notifications are enabled for this service (in this case, yes).
>
> Commands (check_command):
> 
> Commands specify how a service or host will be checked.
> 
> Some examples:
> 
>     check_http: Verifies if a web server is responding correctly.
> 
>     check_nrpe: Allows executing commands on the remote host via the NRPE (Nagios Remote Plugin Executor) agent.
> 
>     check_users: Verifies the number of connected users.
> 
>     check_sda: Verifies disk space on the /dev/sda partition. This command is named this way due to the modification we made in the NRPE agent, as I am using an SSD (Solid State Drive) instead of an HDD (Hard Disk Drive)

>
>
>     check_zombie_procs: Checks for zombie processes.
> 
>     check_total_procs: Verifies the total number of running processes.

Finally, we'll reboot the server so that all the settings are saved

    sudo service nagios restart

![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570461/effe9144-fea9-43f3-baf7-a84f1d4d3821)
