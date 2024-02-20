# SCCMHunter

SCCMHunter is a post-ex tool built to streamline identifying, profiling, and attacking SCCM related assets in an Active Directory domain. The basic function of the tool is to query LDAP with the find module for potential SCCM related assets. This is achieved through ACL recon of objects created during the deployment process when extending the AD schema, resolving any published Management Points, as well as by performing queries for the keywords "SCCM" or "MECM". This list of targets is then profiled with the SMB module by checking the remarks for default shares required by assets configured with certain SCCM roles. Additionally, the module checks for the SMB signing status of the host and performs further profiling of other SCCM services, such as if if the MSSQL service is running or if the host is an SMS Provider. All of this helps paint a picture for potential attack paths in the environment. Once profiling is complete, the operator can target abusing client enrollment with the HTTP (@\_xpn\_) module accounts, use the MSSQL (@_mayyhem) module to grab the necessary syntax for complete site server takeover, or use the DPAPI module to extract Network Access Accounts from a comprimised SCCM client. Finally, if a hierarchy takeover is successful, the admin module is available for post exploitation and lateral movement.

This tool was developed and tested in a lab environment. Your mileage may vary on performance. If you run into any problems please don't hesitate to open an issue.

## Table of Contents

- [Modules](#modules)
  - [Find](#find)
  - [SMB](#smb)
  - [Http](#http)
  - [Mssql](#mssql)
  - [Admin](#admin)
  - [Show](#show)

# Modules

## [Find](https://github.com/garrettfoster13/sccmhunter/wiki/find)

The find module queries LDAP for default ACLs created during extension of the AD schema during deployment. During installation, under the "System" container, the "System Management" container is created and the site server machine account is granted GenericAll permissions on the container object. Additionally, when configuring a server with the "Management Point" (MP) role in SCCM, the site server publishes this information in the "System Management" container in a mSSMSManagementPoint class object. The MP's dNSHostName attribute is stored here and is how clients will resolve available management points from AD. The last step is to simply query AD for acronyms related to SCCM or MECM based on administrators tendency use descriptive labels for related users, groups,  and systems. All potential site server hostnames are logged for use with the SMB and Http modules.


## SMB

The SMB module takes the results from Find and enumerates the remote hosts SMB shares, SMB signing status, and checks if the server is running MSSQL. During setup of particular roles in SCCM, such as the MP or distribution point (DP) roles, the remarks for default file shares disclose what the particular server's role is. This is useful due to requirements during deployment for the site server machine account to have local administrator rights for servers configured with the MP, DP, and SQL database roles and are vulnerable to relay attacks if SMB signing is disabled or not required. Through this profiling the operator can streamline the process of identifying this condition. Additionally, the SMB module checks for the existence of the "REMINST" file share found on DPs that indicate the use of PXEBoot. If found, this share is spidered for the presence of media variables files which can be leveraged to potentially obtain, sometimes privileged, domain users credentials as detailed by Christopher Panayi [here](https://github.com/MWR-CyberSec/PXEThief).


## HTTP

The HTTP module also takes the results from Find and enumerates the remote hosts for SCCM enrollment web services. If found, the module leverages Adam Chester's [sccmwtf.py](https://github.com/xpn/sccmwtf) script to spoof client enrollment with provided machine account credentials or with the -auto flag attempts to create a new machine. In some cases, the flow from registration to resultant policy takes longer than the hard coded 10 second wait time between requests. Because of this, the data required for the policy request is cached and the operator is able to manually request the policy at a later time. More info on this attack can be found at Adam's blog [here](https://blog.xpnsec.com/unobfuscating-network-access-accounts/)

## MSSQL

The MSSQL module accepts arguments to provide the correct MSSQL query syntax to abuse the site server takeover attack discovered and detailed by Chris Thompson [here](https://posts.specterops.io/sccm-site-takeover-via-automatic-client-push-installation-f567ec80d5b1). The hex-formatted SID of the user being granted "Full Administrator" permissions is queried and provided in the terminal. Once the first round of queries are complete, the operator is prompted to provide the minted administrator account’s AdminID and the second round of queries printed to the terminal.  

## Admin

The Admin module is a post hierarchy takeover module intended to run post exploitation commands through the AdminService API. The module stores recovered users, devices, collections and device relationship data in a local SQLite database. Additional commands available include situational awareness commands to enumerate information on endpoints as well as performing arbitrary script execution on devices. All of my testing was performed in a controlled lab environment so your mileage may vary. If you run into any issues please open and issue and provide as much information as possible to explain the issue.


## Show

The show module is intended simply to present the stored data and to export any of that data if necessary

