# Splunk-UF-for-Windows-Installer
Deploy the Splunk Universal Forwarder (UF) for Windows via MSIEXEC

Steps/Instructions:

1. Download the Splunk Universal Forwarder for Windows (requires username/password for Splunk.com): https://www.splunk.com/en_us/download/universal-forwarder.html 
2. Put the MSI installer in a folder accessible over the network. ex: \\fileserver\splunkUF-installer\
3. Run your choice of CLI, cmd.exe or Powershell with the appropriate priveledges (run as Administrator)
4. Configure your command below:

Required Configuration Inputs to change:
Copy/paste the file name of the install file below

DEPLOYMENT_SERVER=IP or FQDN of your Deployment Server or Splunk server (if a single, all-in-one Splunk Server)
Default port is 8089
Example: 
DEPLOYMENT_SERVER="10.1.13.64:8089"
DEPLOYMENT_SERVER="splunk-ds.yourdomain.com:8089"

RECEIVING_INDEXER=IP or FQDN of your Splunk Indexer or Splunk server (if a single, all-in-one Splunk Server)
Default port is 9997
Example: 
RECEIVING_INDEXER="10.1.13.60:9997"
RECEIVING_INDEXER="splunk-idx02.yourdomain.com:9997"

SPLUNKUSERNAME=anything you want

.. code-block:: powershell

  msiexec.exe /i splunkforwarder-file.msi AGREETOLICENSE=Yes DEPLOYMENT_SERVER=<host:port> RECEIVING_INDEXER="<host:port>"LAUNCHSPLUNK=1 SERVICESTARTTYPE=auto SPLUNKUSERNAME=admin MINPASSWORDLEN=16  MINPASSWORDDIGITLEN=4 MINPASSWORDLOWERCASELEN=4 MINPASSWORDUPPERCASELEN=4 MINPASSWORDSPECIALCHARLEN=4 GENRANDOMPASSWORD=1 /quiet /L*v uf-install-logfile.txt


Splunk UF Windows Static Configuration Documentation: https://docs.splunk.com/Documentation/Forwarder/latest/Forwarder/InstallaWindowsuniversalforwarderfromthecommandline#List_of_supported_flags

Basic Troubleshooting steps:
1. If the install fails, make sure you're running the command with admin/elevated rights: Run as Administrator
2. The MSI command drops a log file, check that for errors. Drag and Drop that into Splunk for faster searching and troubleshooting.
