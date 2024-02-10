## Using the show command

### Description

### Requirements

Valid Active Directory credentials

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
                                                                                                                                                                                                                                       
╭─ Options ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│         -siteservers        Show SiteServers table                                                                                                                                                                                  │
│         -mps                Show ManagementPoints table                                                                                                                                                                             │
│         -users              Show SCCM related users.                                                                                                                                                                                │
│         -computers          Show SCCM related computers.                                                                                                                                                                            │
│         -groups             Show SCCM related groups.                                                                                                                                                                               │
│         -all                Show all recon results.                                                                                                                                                                                 │
│         -json               Export chosen results in JSON.                                                                                                                                                                          │
│         -csv                Export chosen results in CSV.                                                                                                                                                                           │
│         -debug              Enable Verbose Logging                                                                                                                                                                                  │
│ --help  -h                  Show this message and exit.                                                                                                                                                                             │
╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯

```