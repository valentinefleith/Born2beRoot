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
- change port :
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
  
