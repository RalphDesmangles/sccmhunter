# Using the admin module

### Description

what does it do

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


### Examples


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
### Usage
### Example

# get_device
### Description
### Usage
### Example

# get_lastlogon
### Description
### Usage
### Example

# get_puser
### Description
### Usage
### Example

# get_user
### Description
### Usage
### Example

# add_admin
### Description
### Usage
### Example

# backdoor
### Description
### Usage
### Example

# backup
### Description
### Usage
### Example

# delete_admin
### Description
### Usage
### Example

# restore
### Description
### Usage
### Example

# script
### Description
### Usage
### Example

# show_admins
### Description
### Usage
### Example

# interact
### Description
### Usage
### Example

# administrators
### Description
### Usage
### Example

# cat
### Description
### Usage
### Example

# cd
### Description
### Usage
### Example

# console_users
### Description
### Usage
### Example

# disk
### Description
### Usage
### Example

# environment
### Description
### Usage
### Example

# ipconfig
### Description
### Usage
### Example

# list_disk
### Description
### Usage
### Example

# ls
### Description
### Usage
### Example

# osinfo
### Description
### Usage
### Example

# ps
### Description
### Usage
### Example

# services
### Description
### Usage
### Example

# sessions
### Description
### Usage
### Example

# shares
### Description
### Usage
### Example

# software
### Description
### Usage
### Example








