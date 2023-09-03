sudo msfdb init
sudo systemctl enable postgresql

sudo msfconsole
db_status
workspace -a pen200
db_nmap
hosts
services
services -p 445

### Auxillary Modules

show auxillary
search type:auxiliary smb
vulns
search type:auxiliary ssh


