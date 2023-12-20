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
AppArmor and SELinux are security systems that provide Mandatory Access Control (MAC) :  refers to a type of access control by which the operating system or database constrains the ability of a subject or initiator to access or generally perform some sort of operation on an object or target. With mandatory access control, this security policy is centrally controlled by a security policy administrator; users do not have the ability to override the policy and, for example, grant access to files that would otherwise be restricted. By contrast, discretionary access control (DAC), which also governs the ability of subjects to access objects, allows users the ability to make policy decisions and/or assign security attributes. 
- **AppArmor** is included by default with Debian. Run `aa-status` to check if it is running. It is designed to be simpler than SELinux because it uses the same semantics used for DAC.
- **SELinux**, however, reinvents some concepts and leaves more liberty in security policy choices.

### How does SSH works?
SSH or Secure Shell is an authentication mechanism between a client and a host. It uses encryption techniques so that all communication between clients and hosts is done in encrypted form. User on Mac or Linux can use SSH the terminal to work on their server via SSH. SSH provides password or public-key based authentication and encrypts connections between two network endpoints. SSH is widely used by network administrators to manage systems and applications remotely, deliver software patches, or execute commands and move files.


### What is a firewall and how does it work ?

### UFW (Uncomplicated FireWall)

UFW is a interface to modify the firewall of the device without compromising security. You use it to configure which ports to allow connections to and which ports to close. This is useful in conjunction with SSH, can set a specific port for it to work with.

### What is LVM ?
Logical Volume Manager – allows us to easily manipulate the partitions or logical volume on a storage device.

### What is Cron ?

Cron or cron job is a command line utility to schedule commands or scripts to happen at specific intervals or a specific time each day. Useful if you want to set your server to restart at a specific time each day.

- `cd /usr/local/bin` – to show monitoring.sh
- `sudo crontab -u root -e` – to edit the cron job
- change script to `*/1 * * * * sleep 30s && script path` – to run it every 30 seconds, delete the line to stop the job from running.

