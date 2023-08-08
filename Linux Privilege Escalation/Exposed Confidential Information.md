.bashrc
sudo -l

### Inspecting Service Footprints

watch -n 1 "ps -aux | grep pass"

sudo tcpdump -i lo -A | grep "pass"