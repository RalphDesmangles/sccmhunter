## Using the show command

### Description
This module lets you display and export recon results. In larger environments where there's too much information to review from a terminal you can export the data to a csv or json. I've found this most useful when reviewing the users and groups results.

### Requirements
Need results from the `find` and/or `smb` modules

### Usage


```
┌──(root㉿kali)-[/opt/sccmhunter]
└─# python3 sccmhunter.py show -h                                                                         

                                                                                          (
                                    888                         d8                         \
 dP"Y  e88'888  e88'888 888 888 8e  888 ee  8888 8888 888 8e   d88    ,e e,  888,8,        )
C88b  d888  '8 d888  '8 888 888 88b 888 88b 8888 8888 888 88b d88888 d88 88b 888 "    ##-------->
 Y88D Y888   , Y888   , 888 888 888 888 888 Y888 888P 888 888  888   888   , 888           )
d,dP   "88,e8'  "88,e8' 888 888 888 888 888  "88 88"  888 888  888    "YeeP" 888          /
                                                                                         (
                                                                 vdev0.0.3                   
                                                                 @garrfoster                    
    
    
    
                                                                                                                                                                                                                                       
                                                                                                                                                                                                   
 Usage: sccmhunter show [OPTIONS] COMMAND [ARGS]...                                                                                                                                                
                                                                                                                                                                                                   
 Show and/or recon table results.                                                                                                                                                                  
                                                                                                                                                                                                   
╭─ Options ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│         -siteservers        Show SiteServers table                                                                                                                                              │
│         -mps                Show ManagementPoints table                                                                                                                                         │
│         -users              Show SCCM related users.                                                                                                                                            │
│         -computers          Show SCCM related computers.                                                                                                                                        │
│         -groups             Show SCCM related groups.                                                                                                                                           │
│         -creds              Show recovered SCCM credentials.                                                                                                                                    │
│         -all                Show all recon results.                                                                                                                                             │
│         -json               Export chosen results in JSON.                                                                                                                                      │
│         -csv                Export chosen results in CSV.                                                                                                                                       │
│         -debug              Enable Verbose Logging                                                                                                                                              │
│ --help  -h                  Show this message and exit.                                                                                                                                         │
╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
──────────────────────────────────────────────────────────╯

```
### Examples
#### Showing results

```
└─# python3 sccmhunter.py show -siteservers              

                                                                                          (
                                    888                         d8                         \
 dP"Y  e88'888  e88'888 888 888 8e  888 ee  8888 8888 888 8e   d88    ,e e,  888,8,        )
C88b  d888  '8 d888  '8 888 888 88b 888 88b 8888 8888 888 88b d88888 d88 88b 888 "    ##-------->
 Y88D Y888   , Y888   , 888 888 888 888 888 Y888 888P 888 888  888   888   , 888           )
d,dP   "88,e8'  "88,e8' 888 888 888 888 888  "88 88"  888 888  888    "YeeP" 888          /
                                                                                         (
                                                                 vdev0.0.3                   
                                                                 @garrfoster                    
    
    
    
[22:41:59] INFO     [+] Showing SiteServers Table                                                                                                                                                     
[22:41:59] INFO     +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | Hostname             | SiteCode   | CAS   | SigningStatus   | SiteServer   | SMSProvider   | Config   | MSSQL   |                                                               
                    +======================+============+=======+=================+==============+===============+==========+=========+                                                               
                    | sccm2.internal.lab   | ABC        | False | False           | True         | True          | Active   | True    |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | active.internal.lab  | ACT        | False | False           | True         | True          | Active   | False   |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | sccm.internal.lab    | LAB        | False | False           | True         | True          | Active   | False   |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | passive.internal.lab | ACT        | False | False           | True         | True          | Passive  | True    |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | cas.internal.lab     | CAS        | True  | False           | True         | True          | Active   | True    |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                                                                                                                                                                                                      
┌──(root㉿kali)-[/opt/sccmhunter]
```

#### Saving results
```
└─# python3 sccmhunter.py show -siteservers -json -csv

                                                                                          (
                                    888                         d8                         \
 dP"Y  e88'888  e88'888 888 888 8e  888 ee  8888 8888 888 8e   d88    ,e e,  888,8,        )
C88b  d888  '8 d888  '8 888 888 88b 888 88b 8888 8888 888 88b d88888 d88 88b 888 "    ##-------->
 Y88D Y888   , Y888   , 888 888 888 888 888 Y888 888P 888 888  888   888   , 888           )
d,dP   "88,e8'  "88,e8' 888 888 888 888 888  "88 88"  888 888  888    "YeeP" 888          /
                                                                                         (
                                                                 vdev0.0.3                   
                                                                 @garrfoster                    
    
    
    
[22:43:19] INFO     [+] Showing SiteServers Table                                                                                                                                                     
[22:43:19] INFO     +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | Hostname             | SiteCode   | CAS   | SigningStatus   | SiteServer   | SMSProvider   | Config   | MSSQL   |                                                               
                    +======================+============+=======+=================+==============+===============+==========+=========+                                                               
                    | sccm2.internal.lab   | ABC        | False | False           | True         | True          | Active   | True    |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | active.internal.lab  | ACT        | False | False           | True         | True          | Active   | False   |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | sccm.internal.lab    | LAB        | False | False           | True         | True          | Active   | False   |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | passive.internal.lab | ACT        | False | False           | True         | True          | Passive  | True    |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
                    | cas.internal.lab     | CAS        | True  | False           | True         | True          | Active   | True    |                                                               
                    +----------------------+------------+-------+-----------------+--------------+---------------+----------+---------+                                                               
[22:43:19] INFO     [*] CSV files saved to /root/.sccmhunter/logs/csvs/                                                                                                                               
[22:43:19] INFO     [*] JSON files saved to /root/.sccmhunter/logs/json/

```