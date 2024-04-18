![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570696/5b6a25a3-8796-442f-a8e8-808e32e95351)Nagios monitoring guide
=================

### Authors 
| Author                | Origin                               |
| --------------------- | ------------------------------------ |
| Marcos Tovar          | UniBarranquilla - IUB                |
| Juan Muñoz            | UniBarranquilla - IUB                |

### Abstract
	
This guide is designed to provide a comprehensive overview of implementing and utilizing Nagios for effective monitoring of IT infrastructure. Created by experts from UniBarranquilla, this document details the essential prerequisites, installation steps, and operational procedures necessary to deploy Nagios effectively. Through real-time monitoring of servers, networks, services, and applications, Nagios offers invaluable insights into system performance and health. This guide aims to equip system administrators with the necessary tools and knowledge to proactively address issues, minimize downtime, and optimize resources. Furthermore, it includes practical examples, such as screenshots and detailed descriptions of key ICT tools, to assist in the practical application of Nagios in a variety of IT environments.
	

### Screenshots 

Place text here

### TOOLS TIC'S 

	

### Status

| Status            | Description                          |
| ----------------- | ------------------------------------ |
| <img src="https://img.shields.io/badge/Study%20Status-Design%20Finalized-brightgreen.svg" alt="Study Status: Design Finalized"> | The study was finished | 

### Keyworks 
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

### Roadmap

    Pre-requisitos 
	  * Linux Proficiency: Acquaintance with Linux command-line operations and basic administrative tasks such as package installation, configuration file editing, and service restarting.
	  * Networking Fundamentals: Understanding basic networking concepts like IP addresses, ports, network protocols (TCP/IP, UDP), and firewall configuration.
	  * System Administration Skills: Basic knowledge of system administration, including server setup, service installation, and configuration.
	  * Shell Scripting: Basic proficiency in Linux shell scripting (e.g., bash) can prove helpful for customizing and automating tasks within Nagios.
	  * Service Configuration and Monitoring: Understanding the workings of the services you intend to monitor with Nagios, as well as the ability to configure these services to enable monitoring.
		
    Instalación 
	  * Linux Ubuntu 20.04
	  * Apache
	  * Docker
    
    Servidor (Server)
		Item1
		Item2
		Item3 - plugins 
    Clientes (Client)

### Steps for Nagios installation
    
    Step 1: Update the System
	``` sudo apt update sudo apt upgrade  ```
    Step 2: Install packages 
	``` sudo apt install wget unzip vim curl gcc openssl build-essential libgd-dev libssl-dev libapache2-mod-php php-gd php apache2 ```
    Step 3: Download Nagios Core on Ubunto 20.04. execute the follow command
	```  export VER="4.4.6" ```
	```  curl -SL https://github.com/NagiosEnterprises/nagioscore/releases/download/nagios-$VER/nagios-$VER.tar.gz | tar -xzf - ```
	```  This downloads a directory called nagios-4.4.6 to your current working directory. ```
(https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570696/45aada01-49b9-4430-88c3-192c3100f3e3)
	
	```  ```

### Usage 
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

### FAQ 

5 preguntas y respuestas

### Contacts (Contactos)
 * mantoniotovar@unibarranquilla.edu.co
 * juandmunoz@unibarranquilla.edu.co

### Acknowledgements 
 1. Nazareno Anselmi
    - [How install Ubunto - nagios](https://tecnolitas.com/blog/como-instalar-nagios-en-ubuntu-20-04/)
    - [How install nagios NRPE](https://www.youtube.com/watch?v=7qZv50kweys )
 2. Pavel Saavedra
    - [Monitoring devices and network services using nagios](https://www.youtube.com/watch?v=40nUAYv-zQs&ab_channel=PavelSaavedra)


