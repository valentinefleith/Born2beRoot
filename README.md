# Born2beRoot

## Useful commands

### general VM

- view partitions :
```
lsblk
```
- log in as the root user :
```
su -
```

### sudo

- add a new user in sudo group :
```
usermod -aG sudo username
```
- to verify if it worked :
```
getent group sudo
```
*(NB : can work with other groups)*

- `visudo` is an alias that leads to `/etc/sudoers.d`. Useful for managing groups and rights

### ssh (secure shell host)
- view ssh server status :
```
sudo systemctl status ssh
```
- change Port :
```shell
sudo vim /etc/ssh/sshd_config
# check if it worked after changing in file :
sudo grep Port /etc/ssh/sshd_config
```
- restart ssh server :
```
sudo systemctl restart ssh
```
- access my VM from my terminal :
```shell
ssh user@localhost -p port_nb #general
ssh vafleith@localhost -p 4142 #for my own VM
ssh vafleith@127.0.0.1 -p 4142 #alternative command
```
### ufw

- check ufw status :
```
sudo ufw status
```

- add a new Port rule for 8080 :
```
sudo ufw allow 8080
sudo ufw status
```
- delete a Port rule :
``` shell
sudo ufw delete allow 8080
#can work with sudo ufw delete + nb of line (-> sudo ufw status numbered to get the nb)
```

### password policy
2 files related to password policy :
- `/etc/pam.d/common-password` which handles nb of characters requirements, types etc. Requirements are :
```
password  requisite     pam_pwquality.so  retry=3 minlen=10 ucredit=-1 lcredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root
```
- `/etc/login.defs` which handles password changing + warning messages frequencies :
```
PASS_MAX_DAYS 30
PASS_MIN_DAYS 2
PASS_WARN_AGE 7
```
Then type `sudo reboot` to apply changes.

### Create a group / create a new user and assing them to a group

- create a new group :
```
sudo groupadd user42
sudo groupadd evaluating
```
- check if the groups have been created :
```
getent group
```
- create a new user :
```
sudo adduser username
```
- add a user to a specific group :
```
usermod -aG evaluating username
```
- check if user has been added to the group :
```
getent group evaluating
```
- or more generally, type `groups` to see which groups the user account belongs to

- check if the password rules are working for users :
```
sudo chage -l username
```

### Crontab
- `monitoring.sh` is saved in `/usr/local/bin`
- to change rules for crontab :
```
sudo crontab -e
```
- to start / stop / restart crontab :
```
sudo systemctl stop cron
sudo systemctl start cron
sudo systemctl restart cron
```

### Hostname
- verify hostname of the machine :
```
hostname
```
- change hostname :
```shell
sudo vim /etc/hostname #change to new_user42
sudo reboot
```

## Evaluation

### What is a virtual machine ?
A virtual machine is a program on a computer that works like it is a separate computer inside the main computer. It is a simple way to run more than one operating system on the same computer. A very powerful server can be split into several smaller virtual machines to use its resources better. The main purpose of VMs is to operate multiple operating systems at the same time, from the same piece of hardware. Without virtualization, operating multiple systems — like Windows and Linux — would require two separate physical units.

### Operating System choice

Setting up Rocky is quite complex. Debian is more user-friendly and supports many libraries, filesystems and architecture. It also has more options for customisation

### What is the difference between APT and Aptitude ?

- Aptitude is a high-level package manager while APT is lower level which can be used by other higher level package managers
- Aptitude is smarter and will automatically remove unused packages or suggest installation of dependent packages
- Apt will only do explicitly what it is told to do in the command line

### What is AppArmor ? What is SELinux ?

- **AppArmor** is a Linux security system that provides Mandatory Access Control (MAC) security. It allows the system admin to restrict the actions that processes can perform. It is included by default with Debian. Run `aa-status` to check if it is running.
- **SELinux** is 

### How does SSH works?



### What is a firewall and how does it work ?

### What is LVM ?
Logical Volume Manager – allows us to easily manipulate the partitions or logical volume on a storage device.

