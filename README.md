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
