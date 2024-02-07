# smb

## Using the smb command

### Description

Profile discovered SCCM infrastructure to determine their site system roles. Enumerates multiple services for default configuations. Services checked are SMB, HTTP(S), and MSSQL.

### Requirements

Valid Active Directory credentials

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