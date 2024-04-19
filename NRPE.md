How Install NRPE for Nagios
=================

## 1 Step:
Visit this link to find the latest version of NRPE https://github.com/NagiosEnterprises/nrpe/releases
Right-click on the .tar.gz file to copy its link.

![image](https://github.com/marcos65333/Nagios-monitoring-guide/assets/87570461/e7c46903-1b60-47cd-bc6a-d4017d644f36)

## 2 Step:
On the Nagios server where you want to install NRPE, navigate to the root home directory.
Execute the following command, replacing  https://github.com/NagiosEnterprises/nrpe/releases with the NRPE link you copied from GitHub 

    wget  https://github.com/NagiosEnterprises/nrpe/releases

## 3 Step:
Let’s unpack the downloaded file using the following command:

    tar -xzvf nrpe-<NRPE_version>.tar.gz

Make sure to replace <NRPE_version> with the specific version of NRPE that you downloaded. You can use the Tab key to autocomplete the filename.

## 4 Step:
Navigate to the directory created after extracting the file:

    cd nrpe<tab to autocomplete>

Then, execute the following command to configure NRPE:

    ./configure

## 5 Step:
Once the installation is done, execute the following command. This command is the executable used to query the server and will be useful for plugins:

    make check_nrpe

After completing the installation, execute the following command to install the plugins:

    make install-plugins

## 6 Step:
We’ll create a command that allows Nagios to use the NRPE command we just set up.
Navigate to the following location:

    cd /usr/local/nagios/etc/objects/

Next, open the commands.cfg file using the vim editor:

    vim commands.cfg

Scroll to the end of the file and add the following command definition:

    define command{
          command_name check_nrpe
          command_line $USER1$/check_nrpe -H $HOSTADDRESS$ -c $ARG1$
    }

Press the Esc key to switch to command mode, then save the file by typing:

    :wq
