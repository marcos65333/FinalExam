Nagios monitoring guide
=================

## Authors 
| Author                | Origin                               |
| --------------------- | ------------------------------------ |
| Marcos Tovar          | UniBarranquilla - IUB                |
| Juan Muñoz            | UniBarranquilla - IUB                |

## Abstract
	
This guide is designed to provide a comprehensive overview of implementing and utilizing Nagios for effective monitoring of IT infrastructure. Created by experts from UniBarranquilla, this document details the essential prerequisites, installation steps, and operational procedures necessary to deploy Nagios effectively. Through real-time monitoring of servers, networks, services, and applications, Nagios offers invaluable insights into system performance and health. This guide aims to equip system administrators with the necessary tools and knowledge to proactively address issues, minimize downtime, and optimize resources. Furthermore, it includes practical examples, such as screenshots and detailed descriptions of key ICT tools, to assist in the practical application of Nagios in a variety of IT environments.
	

## Screenshots 

![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570461/204c0915-6257-4855-b581-aad857ea3f5d)

![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570461/956beefc-7092-40b7-b62c-55f5657388df)


## TOOLS TIC'S 
    * Oracle Virtual Box
    * Ubuntu Server
    * Putty
    * Nginx
    * Nagios
    * Docker

## Status

| Status            | Description                          |
| ----------------- | ------------------------------------ |
| <img src="https://img.shields.io/badge/Study%20Status-Design%20Finalized-brightgreen.svg" alt="Study Status: Design Finalized"> | The study was finished | 

## Keyworks 
   * Nagios
   * Linux
   * Apache
   * Monitoring
   * Tcp
   * Ubuntu
   * Docker
   * Cloud
   * Ip
   * Plugin
   * Email
   * Sftp

## Roadmap

    Pre-requisitos 
	  * Linux Proficiency: Acquaintance with Linux command-line operations and basic administrative tasks such as package installation, configuration file editing, and service restarting.
	  * Networking Fundamentals: Understanding basic networking concepts like IP addresses, ports, network protocols (TCP/IP, UDP), and firewall configuration.
	  * System Administration Skills: Basic knowledge of system administration, including server setup, service installation, and configuration.
	  * Shell Scripting: Basic proficiency in Linux shell scripting (e.g., bash) can prove helpful for customizing and automating tasks within Nagios.
	  * Service Configuration and Monitoring: Understanding the workings of the services you intend to monitor with Nagios, as well as the ability to configure these services to enable monitoring.
		
    Installation 
	  * Linux Ubuntu 20.04
	  * Apache
	  * Docker
          

## Steps for Nagios installation
    
### Step 1: Update the System
    sudo apt update sudo apt upgrade  
### Step 2: Install packages 
    sudo apt install wget unzip vim curl gcc openssl build-essential libgd-dev libssl-dev libapache2-mod-php php-gd php apache2 ```

### Step 3: Download Nagios Core on Ubunto 20.04. execute the follow command
    export VER="4.4.6" 
    curl -SL https://github.com/NagiosEnterprises/nagioscore/releases/download/nagios-$VER/nagios-$VER.tar.gz | tar -xzf - 
This downloads a directory called nagios-4.4.6 to your current working directory. 
![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570696/5b6a25a3-8796-442f-a8e8-808e32e95351)	

### Step 4: How install Nagios on Ubuntu
    cd nagios-4.4.6
### Execute the configuration script
    ./configure
    
> [!NOTE]
> This will take a few seconds and make sure you get an example output shown below towards the end.

![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570696/79f62b61-4a38-4926-962b-37f049044aab)

### To compile the main program along with the CGIs, run the make all command as follows.
    sudo make all
### Next, create the group users as follows.
    sudo make install-groups-users
    sudo usermod -a -G nagios www-data
![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570696/99d86155-4378-4c81-a603-636a83fa5b90)

### Next, install Nagios Core 4.x on your Ubuntu 20.04 system
    sudo make install 
![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570696/b80272c3-95ee-4861-8801-0fd444168c56)
### Towards the end, some additional instructions will print as shown above.

### Therefore, run the following command to install the init script to the /lib/systemd/system path.
    sudo make install-init
### Next, install and configure permissions on the directory that contains the external command file.
    sudo make install-commandmode
### Next, install the example configuration files in /usr/local/nagios/etc/
    sudo make install-config
### At this point, activate the Apache module necessary for the Nagios web interface
    sudo make install-webconf
    sudo a2enmod rewrite cgi
    sudo systemctl restart apache2
### Also, feel free to install the Nagios exfoliation theme as follows: 
    sudo make install-exfoliation
### For the classic Nagios theme, run the following command.
    sudo make install-classicui
    
###  Step 5: Create a Nagios access web user
### You need to create a login user that will be used to log in to the Nagios interface. We will create a user named nagiosadmin using the command.
    sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
    
> [!IMPORTANT]
> You will be asked to provide a password for the user and confirm it.

![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570696/7feb9fbe-b474-4a2c-a515-bcdeece6774e)
> The password is written to the /usr/local/nagios/etc/htpasswd.users file.

###  Step 6: Install the Nagios plugins
Plugins are used to extend the functionality of Nagios. You can check out the latest plugins from GitHub.
### To download the plugins, run the command
     VER="2.3.3"
     curl -SL https://github.com/nagios-plugins/nagios-plugins/releases/download/release-$VER/nagios-plugins-$VER.tar.gz | tar -xzf -
![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570696/93bee41f-eb20-467a-8724-e7bb42dbbf85)

### In your current working directory, you will have another directory – nagios-plugins-2.3.3
![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570696/942cfa1a-c6e6-4b9a-8874-ee0530c8846c)

### To install the plugins, navigate to the plugins source directory:
    cd nagios-plugins-2.3.3
### Next, compile the Nagios plugins from source as follows:
    ./configure --with-nagios-user=nagios --with-nagios-group=nagios
    sudo make install
### Once the installation is complete, verify that all the configurations are in order as shown.
    sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570696/c96e4cd1-79e8-4c8a-b43d-3bdfefe2ded4)

### Step 7: Start and enable the Nagios daemon
With all the configurations established and ready, proceed to start the nagios service as follows:
### To start the Nagios service run:
    sudo systemctl enable --now nagios
### Confirm that the Nagios service is running.
    sudo systemctl status nagios
![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570696/af277a30-508c-42c4-abc4-56fbe285a7ef)
> [!IMPORTANT]
> The output confirms that Nagios is working.

### Step 8: Access Nagios
### And finally, we reach the last step where we will access Nagios. To do this, simply open your web browser and go to the displayed URL.
    http://ip_servidor/nagios
![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570696/1633def4-6ef1-4fcf-ae93-42f2f54b561d)

### Once authenticated, you will be taken to the control panel shown below
![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570696/a20acacb-6039-41b2-b1d0-f9c9e15e68c3)



![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570696/95aea846-49b3-46e4-985f-1a56b569aaa5)

> [!IMPORTANT]
> ## [How Install Agent NRPE](/NRPE.md)
>



## Usage 
-Nagios is important for several reasons:

 * Infrastructure Monitoring: Nagios enables real-time monitoring of IT infrastructure, including servers, networks, services, and applications. This is essential for identifying performance 
   or availability issues before they impact end users.
 * Proactive Alerts: Nagios automatically notifies system administrators of any detected problems or anomalies in the infrastructure. These alerts enable IT operations teams to respond quickly 
   and address issues before they escalate into crises.
 * Downtime Reduction: By proactively detecting and resolving issues, Nagios helps minimize unplanned downtime. This increases the availability of critical business services and applications.
 * Resource Optimization: Nagios enables efficient management of IT resources by providing detailed insights into system performance and utilization. This helps identify areas for improvement 
   and optimize infrastructure capacity.
 * Historical Data and Analysis: Nagios logs monitoring data over time, facilitating trend analysis and long-term planning. This helps identify behavioral patterns and predict future resource 
   needs.
Place text here

## FAQ 
### How do you configure an HTTP service monitoring service in Nagios?
To configure the HTTP service, we need to enter the 'clients.cfg' file. We must specify the command to execute, in this case, we'll use the 'check_http' command, which requires two parameters: the IP address of the host and the port on which our web server is running.

clients.cfg
![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570696/292138b2-1ded-4eda-addd-2705dcd02914)

## Contacts (Contactos)
 * mantoniotovar@unibarranquilla.edu.co
 * juandmunoz@unibarranquilla.edu.co

## Acknowledgements 
 1. Nazareno Anselmi
    - [How install Ubunto - nagios](https://tecnolitas.com/blog/como-instalar-nagios-en-ubuntu-20-04/)
    - [How install nagios NRPE](https://www.youtube.com/watch?v=7qZv50kweys )
 2. Pavel Saavedra
    - [Monitoring devices and network services using nagios](https://www.youtube.com/watch?v=40nUAYv-zQs&ab_channel=PavelSaavedra)
   




