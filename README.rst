=========================================
Splunk-UF-for-Windows-Installer
=========================================

Deploy the Splunk Universal Forwarder (UF) for Windows via MSIEXEC

=========================================
Considerations:
========================================
1. Splunk Cloud customers should use just the DEPLOYMENT_SERVER parameter to get the UF connected to the Deployment Server and push the Splunk Cloud App to the UF via Deployment Server's Server Class
2. Splunk On-Prem customers with a single, all-in-one Splunk Server should use both DEPLOYMENT_SERVER and RECEIVING_INDEXER parameters.
3. Splunk On-Prem with Indexer Cluster should use just use DEPLOYMENT_SERVER parameter to get the UF connected to the Deployment Server and push the Indexer Cluster App to the UF via Deployment Server's Server Class.



=========================================
Steps/Instructions:
=========================================
1. Download the Splunk Universal Forwarder for Windows (requires username/password for Splunk.com): https://www.splunk.com/en_us/download/universal-forwarder.html 
2. Put the MSI installer in a folder accessible over the network. ex: \\\\fileserver\\\splunkUF-installer\\\splunkforwarder.msi
3. Run your choice of CLI, cmd.exe or Powershell with the appropriate priveledges (run as Administrator)
4. Configure your command below:

=========================================
Required Configuration Inputs to Change
=========================================
Copy and paste the file name of the install file below

DEPLOYMENT_SERVER=IP or FQDN of your Deployment Server.
..............................................................................................................................


Default port is 8089

.. code-block:: bash

    DEPLOYMENT_SERVER="10.1.13.64:8089"


.. code-block:: bash
    
    DEPLOYMENT_SERVER="splunk-ds.yourdomain.com:8089"



**OPTIONAL** RECEIVING_INDEXER=IP or FQDN of your Splunk Indexer or Splunk server (if a single, all-in-one Splunk Server)
..............................................................................................................................


Default port is 9997

Example


.. code-block:: bash

    RECEIVING_INDEXER="10.1.13.60:9997"

.. code-block:: bash

    RECEIVING_INDEXER="splunk-idx02.yourdomain.com:9997"


Splunk Username and Password
..............................................................................................................................

Some admins do not want to put passwords into a command or script or as Plain Text.  To avoid doing so, use ``GENRANDOMPASSWORD=1``
Additionally, you can increase the complexity of the password with the following.


.. code-block:: bash

    MINPASSWORDLEN=16
    
    MINPASSWORDDIGITLE=4
    
    MINPASSWORDLOWERCASELEN=4
    
    MINPASSWORDUPPERCASELEN=4
    
    MINPASSWORDSPECIALCHARLEN=4
    
The installer writes the credentials to ``%TEMP%\splunk.log``.  Open the file in a text editor such as Notepad and ``CTRL+F`` PASSWORD


For the ``SPLUNKUSERNAME`` you can use any username you wish

.. code-block:: bash

    SPLUNKUSERNAME=splunker

====================================================================================================================================================================
Example msiexec command. 
====================================================================================================================================================================

**Splunk On-Prem w/ All-In-One Splunk Server**
Replace the DEPLOYEMENT_SERVER and RECEIVING_INDEXER with the respective IP or FQDN and respective port numbers.

.. code-block:: powershell

  msiexec.exe /i splunkforwarder-file.msi AGREETOLICENSE=Yes DEPLOYMENT_SERVER="192.168.10.51:8089" RECEIVING_INDEXER="192.168.1.51:9997" LAUNCHSPLUNK=1 SERVICESTARTTYPE=auto SPLUNKUSERNAME=admin GENRANDOMPASSWORD=1 MINPASSWORDLEN=16  MINPASSWORDDIGITLEN=4 MINPASSWORDLOWERCASELEN=4 MINPASSWORDUPPERCASELEN=4 MINPASSWORDSPECIALCHARLEN=4  /quiet /L*v uf-install-logfile.txt


**Splunk On-Prem w/ Indexer Cluster** or **Splunk Cloud Customer**

.. code-block:: powershell

  msiexec.exe /i splunkforwarder-file.msi AGREETOLICENSE=Yes DEPLOYMENT_SERVER="192.168.10.51:8089" LAUNCHSPLUNK=1 SERVICESTARTTYPE=auto SPLUNKUSERNAME=admin GENRANDOMPASSWORD=1 MINPASSWORDLEN=16  MINPASSWORDDIGITLEN=4 MINPASSWORDLOWERCASELEN=4 MINPASSWORDUPPERCASELEN=4 MINPASSWORDSPECIALCHARLEN=4  /quiet /L*v uf-install-logfile.txt





Splunk UF Windows Static Configuration Documentation: https://docs.splunk.com/Documentation/Forwarder/latest/Forwarder/InstallaWindowsuniversalforwarderfromthecommandline#List_of_supported_flags

Basic Troubleshooting steps:

1. If the install fails, make sure you're running the command with admin/elevated rights: Run as Administrator

2. The MSI command drops a log file, check that for errors. Drag and Drop that into Splunk for faster searching and troubleshooting.


=========================================
Credits
=========================================
- Dylan Simmers
- Paul Jeffery
