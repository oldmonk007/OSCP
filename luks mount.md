sudo apt-get install cryptsetup
sudo cryptsetup luksOpen /dev/sdb3 my_encrypted_volume
sudo cryptsetup luksOpen /dev/sdb3 my_encrypted_volume
sudo mkdir /media/my_device
sudo mount /dev/mapper/my_encrypted_volume /media/my_device
sudo vgdisplay
sudo vgrename boss-vg sito-vg
modprobe dm-mod  
sudo vgchange -ay
sudo lvscan
sudo mount /dev/sito-vg/root  /media/my_device
