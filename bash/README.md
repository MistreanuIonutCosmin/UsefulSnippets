```bash
### 1. Find and remove empty files/directories
find ./ -type f -empty	
find ./ -type d -empty

find ./ -type f -size 0 -delete
find ./ -type d -empty -delete

### 2. [Mounting a new hdd](https://medium.com/@sh.tsang/partitioning-formatting-and-mounting-a-hard-drive-in-linux-ubuntu-18-04-324b7634d1e0)

sudo fdisk -l
sudo parted /dev/sdb <- if this is the new hdd installed
(parted) mklabel gpt
(parted) mkpart primary 0GB 4GB
quit
sudo mkfs.ext4 /dev/sdb

! temporary mount:
sudo mkdir /mnt/sdb
sudo mount /dev/sdb /mnt/sdb

! Auto mount after reboot
nano /etc/fstab
/dev/sdb     /mnt/sdb      ext4        defaults      0       0

! Change partition permission
sudo chown <user>:<group> /mnt/sdb -R
```
### 3. connecting via ssh using public/private key
cat ~/.ssh/id_rsa.pub | ssh <user>@<hostname> 'cat >> .ssh/authorized_keys && echo "Key copied"'
