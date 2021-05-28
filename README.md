# Splunk-UF-for-Windows-Installer
Deploy the Splunk Universal Forwarder (UF) for Windows via MSIEXEC

Steps/Instructions:

1. Download the Splunk Universal Forwarder for Windows (requires username/password for Splunk.com): https://www.splunk.com/en_us/download/universal-forwarder.html 
2. Put the MSI installer in a folder accessible over the network. ex: \\fileserver\splunkUF-installer\
3. Run your choice of CLI, cmd.exe or Powershell with the appropriate priveledges (run as Administrator)
4. Configure your command below:

Required Configuration Inputs to change:
Copy/paste the file name of the installer below

DEPLOYMENT_SERVER=IP or FQDN of your Deployment Server or Splunk server (if a single, all-in-one Splunk Server)

RECEIVING_INDEXER=IP or FQDN of your Splunk Indexer or Splunk server (if a single, all-in-one Splunk Server)

SPLUNKUSERNAME=anything you want

`
msiexec.exe /i splunkforwarder-8.1.3-63079c59e632-x64-release.msi AGREETOLICENSE=Yes DEPLOYMENT_SERVER=10.0.0.21:8089 LAUNCHSPLUNK=1 SERVICESTARTTYPE=auto SPLUNKUSERNAME=admin MINPASSWORDLEN=16  MINPASSWORDDIGITLEN=4 MINPASSWORDLOWERCASELEN=4 MINPASSWORDUPPERCASELEN=4 MINPASSWORDSPECIALCHARLEN=4 GENRANDOMPASSWORD=1 /quiet /L*v uf-install-logfile.txt
`

Splunk UF Windows Static Configuration Documentation: https://docs.splunk.com/Documentation/Forwarder/8.2.0/Forwarder/InstallaWindowsuniversalforwarderfromthecommandline#List_of_supported_flags

Basic Troubleshooting steps:
1. If the install fails, make sure you're running the command with admin/elevated rights: Run as Administrator
2. The MSI command drops a log file, check that for errors. Drag and Drop that into Splunk for faster searching
