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
copy to home dic:
```
cp /etc/hosts ~/;
```

- Logs & More File Management Tools
```
tail -f secure
```

cat multiple files:
```
cat cron secure > all.log
```
less command. e->one line down y->one line up b->one page up f->one page down

- File Permissions

show user belongs group
```
groups username
```
- Cron Jobs

```
cd /etc
vim crontab
```
should remember the sequence:
min, hour, day of month, month, day of week

OR create own cron
```
cd /var/spool/cron
crontab -e
```
- Introduction To Linux Package Managers
```
apt-cache search apache2
```
- top
many shortcuts.
For example.k = kill
- Finding Files
locate( rarely used)
```
updatedb
yum install locate
locate filename
```
find
```
find . -name 'filename*'
```

- Exercise: Using FIND to Find and Manipulate Files

Using the find command, change the permissions on the /etc/myTesT.txt file so that it is universal read/write/execute. This should be done in one line using the find command options only.
```
sudo find / -name myTesT.txt -exec chmod 777 {} \;
```

With the find command, using root or sudo privileges, display all executable files in /usr directory.

```
sudo find /usr -perm /a=x
```

- wc, split, cat, and diff commands
```
split -l 2 filename
```
- grep, egrep, and fgrep
```
grep ^beginwith file
grep -c ^beginwith file (return count)
grep [z] file
grep -f formatfile testtargetfile
grep -lr cron /etc (search file name)
```
```
egrep -i 'hello.*world' filename (-i,insensitive)
egrep -i 'hello|world' filename (or)
egrep -i 'hello|world' filename | grep -v donotwant
```
fgrep(all literal,no escape)
```
fgrep ^hello filename
```

- Using ps To Manage Processes
```
ps -w
ps -U username
ps -U username --forest (show hiarachy)
ps -i
ps -e (all running process)
```
- Using TOP
```
top -d 1 (update every 1 second)
top -p numbers (assignprocess to moniter) Ex: top -p 1,2,3
top -n 5 (Execute 5 times)

```
press 's' to change delay

- Using nice To Change Linux Process Priorities
-20 is highest level. 19 is lowest
```
default is 10.
To assign,
nice -n 10 progname
nice -10 progname
```
renice:
```
renice -n -20 -p 1234 (pid)
renice -n -20 -u username
```
- Killing Processes In Linux
```
kill -9 pid(force kill)
kill -1 pid(restart)
kill -15 pid(normal shutdown)
nohup (commands) execute after shutdown(immune)
```
- Using The uname Command To Query System Information
```
uname -o (os name)
uname -s (kernel name)
uname -n (network host name)
uname -m (cpu/arch)
uname -v (kernel version)
uname -r (kernel release)
uname -i (hardware)
uname -a (all)
```

- Background VS Foreground processes
for example
```
nano
```
press ctrl z turn to background
fg to return

To see all jobs,
```
jobs
fg 1
```
to launch in background, append &
```
command &
```
- The nohup Command
- The free Command
```
free -b/-m
free -s 2 (set interval) similar to top -d 2
```
- Find Command
```
find . -type f/d -name 'cron*'
find /home -perm 777 -exec chmod 555 {} \;
find / -group name
find / -size +1M
```

- Creating And Mounting A Disk Partition
```
mkfs -t ext4 /dev/xvdf
```

- Using fdisk, Creating A File System, and Configuring Mount Entry With /etc/fstab
```
cd dev/
fdisk 
n
p

```
- Working With Linux Swap
```
dd if=/dev/zero of=~/swap.swp bs=1024 count=800k
mkswap swap.swp
swapon swap.swp
free -m
```

release swap:
```
swapoff -a
```

- du, df and mount
- fsck and e2fsck
- mke2fs and debugfs
```
mke2fs -t ext4 /dev/xvdf
```
- dumpe2fs and tune2fs
```
dumpe2fs /dev/sda1
```
- xfs tools
- Exercise: File System Integrity and Maintenance
Display both the volume name and UUID of the root drive on your server and capture the results in your output file.
```
ls -al /dev/disk/by-uuid >> file.out && ls -al /dev/disk/by-partlabel >> file.out 
lsblk -o partlabel,uuid >> file.out
blkid >> file.out
```
Set the root partition of your server to the following:
i. Volume Name: SysUtilLab4
ii. Maximum Number of Mounts Before Check: 50
iii. Current Number of Mounts: 55
iv. Interval Between Checks: 2 Days
```
sudo tune2fs -L SysUtilLab4 -c 50 -C 55 -i 2d /dev/xvda1
```


- Simple Commands & Shortcuts For The Linux Shell
time command
```
time ls
```
ctrl x backspace (clear current line)

-  Environment Variables, Redirection Operators & Data Pipes
```
export VAR="new"
echo $VAR
```
To remove environ var:
```
unset VAR
```
check env:
```
env
```
standard output:
```
tac < x.txt
```
- Manipulating Files
```
touch test1
sort test1 >> test1.txt
touch test2
sort test2 >> test2.txt
join test1 test2
```
paste a file's content to another file:
```
paste oldfile newfile
```
'translate', substitute
```
tr worda wordb < text.txt (substitute a to b)
```
count line numbers:
```
nl file.txt
cat -n file.txt
```
count unique:
```
cat -n file.txt |uniq
```
format:
```
fmt file.txt
```
- File Viewing Commands For The Linux Bash Shell
Only moniter specific words
```
tail -f xx.txt | grep word
```
sed (substitute)
```
sed 's/old/new/g' filename
```
- Disk Quotas
```
apt-get install quota quotatool
```
Check:
```
sudo quotacheck -avugm
```
Edit:
```
edquota username
```
repquota
```
repquota /
repquota -s (human readable format)
```
-  Upstart Overview
```
runlevel
initctl list
```
```
init-ckeckconf xx.conf
telinit 4
```
- SysVinit Vs Systemd
```
systemctl -t help
systemd.unit
```
- Using Systemd With Services And Service Unit Files
```
yum install httpd
locate httpd.service
cat /usr/lib/systemd/system/httpd.service
systemctl status httpd.service
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
