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
