## Using the find command

### Description

Query LDAP for the presence of SCCM related infrastructure via the following three checks:
1. Checks the DACL for the 'System Management' container manually created during AD schema extension
2. Checks for published Managment Points for clients to query
3. Checks for the strings SCCM and MECM in the entire directory due to observed naming convention habits
    - Nested group resolution is not enabled by default, use the `-resolve` flag to dig into nested groups. I've only tested this function in a lab so your results may vary or be inefficient. Please let me know if you run into issues if you choose to use the flag. I've added some terminal output for results and duplicates as they're found to try and help with this.



### Requirements

Valid Active Directory credentials

### Usage

```
└─# python3 sccmhunter.py find -h                                                                
                                                                                                                                                                                                      
 Usage: sccmhunter find [OPTIONS] COMMAND [ARGS]...                                                                                                                                                   
                                                                                                                                                                                                      
 Enumerate LDAP for SCCM assets.                                                                                                                                                                      
                                                                                                                                                                                                      
╭─ Options ──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│            -u            TEXT           Username [default: None]                                                                                                                                   │
│            -p            TEXT           Password [default: None]                                                                                                                                   │
│ *          -d            TEXT           Domain [default: None] [required]                                                                                                                          │
│            -t            TEXT           Target domain. Use if authenticating across trusts. [default: None]                                                                                        │
│ *          -dc-ip        TEXT           IP address or FQDN of domain controller [default: None] [required]                                                                                         │
│            -resolve                     Resolve nested group members. (Can be slow in large environments)                                                                                          │
│            -ldaps                       Use LDAPS instead of LDAP                                                                                                                                  │
│            -k                           Use Kerberos authentication                                                                                                                                │
│            -no-pass                     don't ask for password (useful for -k)                                                                                                                     │
│            -hashes       LMHASH:NTHASH  LM and NT hashes, format is LMHASH:NTHASH [default: None]                                                                                                  │
│            -aes          HEX KEY        AES key to use for Kerberos Authentication (128 or 256 bits) [default: None]                                                                               │
│            -debug                       Enable Verbose Logging                                                                                                                                     │
│    --help  -h                           Show this message and exit.                                                                                                                                │
╰────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯

```

### Examples
#### Basic query
Run the find command to query LDAP.

```
└─# python3 sccmhunter.py find -u 'lowpriv' -p 'P@ssw0rd' -d internal.lab -dc-ip 10.10.100.100

                                                                                          (
                                    888                         d8                         \
 dP"Y  e88'888  e88'888 888 888 8e  888 ee  8888 8888 888 8e   d88    ,e e,  888,8,        )
C88b  d888  '8 d888  '8 888 888 88b 888 88b 8888 8888 888 88b d88888 d88 88b 888 "    ##-------->
 Y88D Y888   , Y888   , 888 888 888 888 888 Y888 888P 888 888  888   888   , 888           )
d,dP   "88,e8'  "88,e8' 888 888 888 888 888  "88 88"  888 888  888    "YeeP" 888          /
                                                                                         (
                                                                 v0.0.2                   
                                                                 @garrfoster                    
    
    
    
[21:15:03] INFO     [*] Checking for System Management Container.                                                                                                                                     
[21:15:03] INFO     [+] Found System Management Container. Parsing DACL.                                                                                                                              
[21:15:03] INFO     [+] Found 3 computers with Full Control ACE                                                                                                                                       
[21:15:03] INFO     [*] Querying LDAP for published Sites and Management Points                                                                                                                       
[21:15:03] INFO     [+] Found 3 Management Points in LDAP.                                                                                                                                            
[21:15:03] INFO     [*] Searching LDAP for anything containing the strings 'SCCM' or 'MECM'                                                                                                           
[21:15:03] INFO     [+] Found 5 principals that contain the string 'SCCM' or 'MECM'.                                                                                                                  
                                                                                     
```
#### Verbose Query
Run the find command with verbose output

```
└─# python3 sccmhunter.py find -u 'lowpriv' -p 'P@ssw0rd' -d internal.lab -dc-ip 10.10.100.100 -debug

                                                                                          (
                                    888                         d8                         \
 dP"Y  e88'888  e88'888 888 888 8e  888 ee  8888 8888 888 8e   d88    ,e e,  888,8,        )
C88b  d888  '8 d888  '8 888 888 88b 888 88b 8888 8888 888 88b d88888 d88 88b 888 "    ##-------->
 Y88D Y888   , Y888   , 888 888 888 888 888 Y888 888P 888 888  888   888   , 888           )
d,dP   "88,e8'  "88,e8' 888 888 888 888 888  "88 88"  888 888  888    "YeeP" 888          /
                                                                                         (
                                                                 v0.0.2                   
                                                                 @garrfoster                    
    
    
    
[21:22:46] DEBUG    [*] Database ready.                                                                                                                                                               
[21:22:46] DEBUG    [+] Bind successful ldap://10.10.100.100:389 - cleartext                                                                                                                          
[21:22:46] INFO     [*] Checking for System Management Container.                                                                                                                                     
[21:22:46] INFO     [+] Found System Management Container. Parsing DACL.                                                                                                                              
[21:22:46] INFO     [+] Found 3 computers with Full Control ACE                                                                                                                                       
[21:22:46] INFO     [*] Querying LDAP for published Sites and Management Points                                                                                                                       
[21:22:46] INFO     [+] Found 3 Management Points in LDAP.                                                                                                                                            
[21:22:46] INFO     [*] Searching LDAP for anything containing the strings 'SCCM' or 'MECM'                                                                                                           
[21:22:46] INFO     [+] Found 5 principals that contain the string 'SCCM' or 'MECM'.                                                                                                                  
[21:22:46] INFO     Site Servers Table                                                                                                                                                                
[21:22:46] INFO     +---------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                                
                    | Hostname            | SiteCode   | CAS   | SigningStatus   | SiteServer   | SMSProvider   | Config   | MSSQL   |                                                                
                    +=====================+============+=======+=================+==============+===============+==========+=========+                                                                
                    | active.internal.lab |            |       |                 | True         |               |          |         |                                                                
                    +---------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                                
                    | sccm.internal.lab   |            |       |                 | True         |               |          |         |                                                                
                    +---------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                                
                    | sccm.internal.lab   |            |       |                 | True         |               |          |         |                                                                
                    +---------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                                
[21:22:46] INFO     Management Points Table                                                                                                                                                           
[21:22:46] INFO     +---------------------+------------+-----------------+                                                                                                                            
                    | Hostname            | SiteCode   | SigningStatus   |                                                                                                                            
                    +=====================+============+=================+                                                                                                                            
                    | active.internal.lab | ACT        |                 |                                                                                                                            
                    +---------------------+------------+-----------------+                                                                                                                            
                    | mp.internal.lab     | LAB        |                 |                                                                                                                            
                    +---------------------+------------+-----------------+                                                                                                                            
                    | sccm.internal.lab   | LAB        |                 |                                                                                                                            
                    +---------------------+------------+-----------------+                                                                                                                            
[21:22:46] INFO     Computers Table                                                                                                                                                                   
[21:22:46] INFO     +-------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                                  
                    | Hostname          | SiteCode   | SigningStatus   | SiteServer   | ManagementPoint   | DistributionPoint   | SMSProvider   | WSUS   | MSSQL   |                                  
                    +===================+============+=================+==============+===================+=====================+===============+========+=========+                                  
                    | sccm.internal.lab |            |                 |              |                   |                     |               |        |         |                                  
                    +-------------------+------------+-----------------+--------------+-------------------+---------------------+---------------+--------+---------+                                  
[21:22:46] INFO     Users Table                                                                                                                                                                       
[21:22:46] INFO     +------+--------+------------------+------------------------+---------------+                                                                                                     
                    | cn   | name   | sAMAAccontName   | servicePrincipalName   | description   |                                                                                                     
                    +======+========+==================+========================+===============+                                                                                                     
                    +------+--------+------------------+------------------------+---------------+                                                                                                     
[21:22:46] INFO     Groups Table                                                                                                                                                                      
[21:22:46] INFO     +------------------+------------------+------------------+-------------------------------------------+---------------+                                                            
                    | cn               | name             | sAMAAccontName   | member                                    | description   |                                                            
                    +==================+==================+==================+===========================================+===============+                                                            
                    | SCCM_SiteServers | SCCM_SiteServers | SCCM_SiteServers | CN=ACTIVE,CN=Computers,DC=internal,DC=lab |               |                                                            
                    |                  |                  |                  | CN=SCCM,CN=Computers,DC=internal,DC=lab   |               |                                                            
                    +------------------+------------------+------------------+-------------------------------------------+---------------+  
```