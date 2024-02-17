## Using the smb command

### Description

Profile discovered SCCM infrastructure to determine their site system roles. Enumerates multiple services for default configuations. Services checked are SMB, HTTP(S), and MSSQL. The recon is broken down into 3 components:

1. Site server profiling
- Confirms connectivity 
- Checks whether the site server is hosting the MSSQL service
- Checks whether the site server is an active or passive site server
- Checks if the site server is a central administration site

2. Management point checks
- Confirms connectivity to the HTTP endpoints

3. Role and config checks
-  Checks for associated site codes from default file shares
-  Checks if SMB signing is disabled
-  Checks for the following site system roles:
    1. Site Server
    2. Management Point
    3. Distribution Point - If the distribution point is found hosting a variables file, the path is logged and optionally saved automatically to the logs directory
    4. SMS Provider
    5. MSSQL
    6. WSUS


### Requirements

- Valid Active Directory credentials
- Network connectivity to the various services being checked


### Usage

```
└─# python3 sccmhunter.py smb -h                                                          

                                                                                          (
                                    888                         d8                         \
 dP"Y  e88'888  e88'888 888 888 8e  888 ee  8888 8888 888 8e   d88    ,e e,  888,8,        )
C88b  d888  '8 d888  '8 888 888 88b 888 88b 8888 8888 888 88b d88888 d88 88b 888 "    ##-------->
 Y88D Y888   , Y888   , 888 888 888 888 888 Y888 888P 888 888  888   888   , 888           )
d,dP   "88,e8'  "88,e8' 888 888 888 888 888  "88 88"  888 888  888    "YeeP" 888          /
                                                                                         (
                                                                 vdev0.0.3                   
                                                                 @garrfoster                    
    
    
    
                                                                                                                                                                                                      
 Usage: sccmhunter smb [OPTIONS] COMMAND [ARGS]...                                                                                                                                                    
                                                                                                                                                                                                      
 Profile and Enumerate SMB shares of discovered SCCM servers.                                                                                                                                         
                                                                                                                                                                                                      
╭─ Options ──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│            -u            TEXT           Username [default: None]                                                                                                                                   │
│            -p            TEXT           Password [default: None]                                                                                                                                   │
│ *          -d            TEXT           Target domain [default: None] [required]                                                                                                                   │
│ *          -dc-ip        TEXT           IP address or FQDN of domain controller [default: None] [required]                                                                                         │
│            -ldaps                       Use LDAPS instead of LDAP                                                                                                                                  │
│            -k                           Use Kerberos authentication                                                                                                                                │
│            -no-pass                     don't ask for password (useful for -k)                                                                                                                     │
│            -hashes       LMHASH:NTHASH  LM and NT hashes, format is LMHASH:NTHASH [default: None]                                                                                                  │
│            -aes          HEX KEY        AES key to use for Kerberos Authentication (128 or 256 bits) [default: None]                                                                               │
│            -debug                       Enable Verbose Logging                                                                                                                                     │
│            -save                        Save PXEBoot variables files if found.                                                                                                                     │
│    --help  -h                           Show this message and exit.                                                                                                                                │
╰────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```

### Examples
#### Basic Run
```
└─# python3 sccmhunter.py smb -u administrator -p P@ssw0rd -d internal.lab -dc-ip 10.10.100.100 

                                                                                          (
                                    888                         d8                         \
 dP"Y  e88'888  e88'888 888 888 8e  888 ee  8888 8888 888 8e   d88    ,e e,  888,8,        )
C88b  d888  '8 d888  '8 888 888 88b 888 88b 8888 8888 888 88b d88888 d88 88b 888 "    ##-------->
 Y88D Y888   , Y888   , 888 888 888 888 888 Y888 888P 888 888  888   888   , 888           )
d,dP   "88,e8'  "88,e8' 888 888 888 888 888  "88 88"  888 888  888    "YeeP" 888          /
                                                                                         (
                                                                 vdev0.0.3                   
                                                                 @garrfoster                    
    
    
    
[16:25:22] INFO     [+] Finished profiling Site Servers.                                                                                                                                              
[16:25:23] INFO     +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | Hostname             | SiteCode   | CAS   | SigningStatus   | SiteServer   | SMSProvider   | Config   | MSSQL   |                                                               
                    +======================+============+=======+=================+==============+===============+==========+=========+                                                               
                    | sccm2.internal.lab   | ABC        | False | False           | True         | True          | Active   | True    |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | passive.internal.lab | ACT        | False | False           | True         | True          | Passive  | True    |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | active.internal.lab  | ACT        | False | False           | True         | True          | Active   | False   |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | sccm.internal.lab    | LAB        | False | False           | True         | True          | Active   | False   |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | cas.internal.lab     | CAS        | True  | False           | True         | True          | Active   | True    |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
[16:25:32] INFO     [+] Finished profiling Management Points.                                                                                                                                         
[16:25:32] INFO     +---------------------+------------+-----------------+                                                                                                                            
                    | Hostname            | SiteCode   | SigningStatus   |                                                                                                                            
                    +=====================+============+=================+                                                                                                                            
                    | sccm2.internal.lab  | ABC        | False           |                                                                                                                            
                    +---------------------+------------+-----------------+                                                                                                                            
                    | active.internal.lab | ACT        | False           |                                                                                                                            
                    +---------------------+------------+-----------------+                                                                                                                            
                    | mp.internal.lab     | LAB        | False           |                                                                                                                            
                    +---------------------+------------+-----------------+                                                                                                                            
                    | sccm.internal.lab   | LAB        | False           |                                                                                                                            
                    +---------------------+------------+-----------------+                                                                                                                            
[16:26:12] INFO     [+] Finished profiling all discovered computers.                                                                                                                                  
[16:26:12] INFO     +----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                               
                    | Hostname             | SiteCode   | SigningStatus   | SiteServer   | ManagementPoint   | DistributionPoint   | SMSProvider   | WSUS   | MSSQL   |                               
                    +======================+============+=================+==============+===================+=====================+===============+========+=========+                               
                    | sccm2.internal.lab   | ABC        | False           | True         | True              | False               | True          | False  | True    |                               
                    +----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                               
                    | passive.internal.lab | ACT        | False           | False        | False             | False               | True          | False  | True    |                               
                    +----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                               
                    | active.internal.lab  | ACT        | False           | True         | True              | False               | True          | False  | False   |                               
                    +----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                               
                    | sccm.internal.lab    | LAB        | False           | True         | True              | False               | True          | False  | False   |                               
                    +----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                               
                    | cas.internal.lab     | CAS        | False           | True         | False             | False               | True          | False  | True    |                               
                    +----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                               
                    | mp.internal.lab      | LAB        | False           | False        | True              | False               | False         | False  | False   |                               
                    +----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+ 
```

#### Finding and saving PXE boot files
```
└─# python3 sccmhunter.py smb -u administrator -p P@ssw0rd -d internal.lab -dc-ip 10.10.100.100 -save     
SCCMHunter vdev0.0.3 by @garrfoster
[11:52:38] INFO     Profiling 5 site servers.                                                                                                                                                         
[11:53:00] INFO     [+] Finished profiling Site Servers.                                                                                                                                              
[11:53:00] INFO     +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | Hostname             | SiteCode   | CAS   | SigningStatus   | SiteServer   | SMSProvider   | Config   | MSSQL   |                                                               
                    +======================+============+=======+=================+==============+===============+==========+=========+                                                               
                    | active.internal.lab  | ACT        | False | False           | True         | True          | Active   | False   |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | sccm.internal.lab    | LAB        | False | False           | True         | True          | Active   | False   |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | passive.internal.lab | ACT        | False | False           | True         | True          | Passive  | True    |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | cas.internal.lab     | CAS        | True  | False           | True         | True          | Active   | True    |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | sccm2.internal.lab   | ABC        | False | False           | True         | True          | Active   | True    |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
[11:53:00] INFO     Profiling 4 management points.                                                                                                                                                    
[11:53:16] INFO     [+] Finished profiling Management Points.                                                                                                                                         
[11:53:16] INFO     +---------------------+------------+-----------------+                                                                                                                            
                    | Hostname            | SiteCode   | SigningStatus   |                                                                                                                            
                    +=====================+============+=================+                                                                                                                            
                    | mp.internal.lab     | LAB        | False           |                                                                                                                            
                    +---------------------+------------+-----------------+                                                                                                                            
                    | sccm.internal.lab   | LAB        | False           |                                                                                                                            
                    +---------------------+------------+-----------------+                                                                                                                            
                    | sccm2.internal.lab  | ABC        | False           |                                                                                                                            
                    +---------------------+------------+-----------------+                                                                                                                            
                    | active.internal.lab | ACT        | False           |                                                                                                                            
                    +---------------------+------------+-----------------+                                                                                                                            
[11:53:16] INFO     Profiling 11 computers.                                                                                                                                                           
[11:54:01] INFO     [*] Searching dp.internal.lab for PXEBoot variables files.                                                                                                                        
[11:54:02] INFO     [+] Variables files downloaded!                                                                                                                                                   
[11:54:02] INFO     [+] Results saved to /root/.sccmhunter/logs/smbhunter.log                                                                                                                         
[11:54:02] INFO     [+] Finished profiling all discovered computers.                                                                                                                                  
[11:54:02] INFO     +-----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                              
                    | Hostname              | SiteCode   | SigningStatus   | SiteServer   | ManagementPoint   | DistributionPoint   | SMSProvider   | WSUS   | MSSQL   |                              
                    +=======================+============+=================+==============+===================+=====================+===============+========+=========+                              
                    | active.internal.lab   | ACT        | False           | True         | False             | False               | True          | False  | False   |                              
                    +-----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                              
                    | sccm.internal.lab     | LAB        | False           | True         | False             | False               | True          | False  | False   |                              
                    +-----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                              
                    | passive.internal.lab  | ACT        | False           | False        | False             | False               | True          | False  | True    |                              
                    +-----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                              
                    | cas.internal.lab      | CAS        | False           | True         | False             | False               | True          | False  | True    |                              
                    +-----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                              
                    | sccm2.internal.lab    | ABC        | False           | True         | False             | False               | True          | False  | True    |                              
                    +-----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                              
                    | mp.internal.lab       | LAB        | False           | False        | True              | False               | False         | False  | False   |                              
                    +-----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                              
                    | share.internal.lab    | None       | False           | False        | False             | False               | False         | False  | False   |                              
                    +-----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                              
                    | sql2.internal.lab     | None       | False           | False        | False             | False               | False         | False  | True    |                              
                    +-----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                              
                    | wsus.internal.lab     | None       | False           | False        | False             | False               | False         | True   | False   |                              
                    +-----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                              
                    | provider.internal.lab | None       | False           | False        | False             | False               | False         | False  | False   |                              
                    +-----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                              
                    | dp.internal.lab       | LAB        | False           | False        | False             | True                | False         | False  | False   |                              
                    +-----------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+ 
```
