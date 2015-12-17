#### lylinuxlpiclevel1
- Root User, Sudo Users And Setting Up Your User Account
```
cd /etc/sudoers
visudo
```
Add a user to group
```
usermod -G gpname username
```

- Navigating Linux & The File System
```
cp -r olddir/ newdir/
```

- screen
install dev tools:
Fedora
```
sudo yum update

sudo yum groupinstall "Development Tools" "Legacy Software Development"
```
Debian / Ubuntu / Debian derivatives
```
sudo apt-get update

sudo apt-get install build-essential
```
First,
```
apt-get install screen
```
Try:
```
screen -list
```
Check:
```
screen(create new screen, or `screen -S yourname` to create new session)
w (all logged in users)
uptime
screen -list
```
To detach,
```
screen -d 1234(4-dig id)
```
To reattach,
```
screen -r 1234
```

- xz compression
To zip a file:
```
xz -z filename
```
list filename of zipped file:
```
xz -l filename
```
Unzip:
```
xz -d filename
```
To zip a folder:
First:
```
tar cf folder.tar folder
```
Then
```
xz -z folder.tar
unxz folder.tar.xz
tar -xvf folder.tar
```



- pkill and pgrep
```
pkill psname
pkill -u username psname
pgrep -l -u username
pgrep -n -l -u username //-n: most recent process
pgrep -v -l -u username //does not belong the this user
pkill -t pts/2 //kill all ps associated with TTY 
```

- dmesg
```
dmesg | tail
```


- Grub-install and Grub-mkconfig (centos 7)
```
cd /etc/grub.d
cd /boot/grub
vim grub.cfg
```
change default boot configuration:
```
cd /etc/default
vim grub
```
Then regenerate configuration file
```
grub2-mkconfig > /boot/grub/grub.cfg
cd /boot/grub
```
reinstall boot loader:
```
cat device.map
grub2-install /dev/sda
reboot
```
