- SSH connection to OSCP machines
```
ssh -o "UserKnownHostsFile=/dev/null" -o "StrictHostKeyChecking=no" learner@192.168.50.52
```
- Bash One-Liners
```
	for ip in $(cat list.txt); do host $ip.megacorpone.com; done
```
- SecLists Project - collection of wordlists
- 