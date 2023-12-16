# Born2beRoot

## Commands I need to remember

### general VM

- see the partitions : ```lsblk```
- log in as the root user : ```su -```

### sudo

- add a new user in sudo group : ```usermod -aG sudo username```
- to verify if it worked : ```getent group sudo```

NB : can work with other groups

- `visudo` emplacement = `/etc/sudoers.d` but `visudo` is an alias that works itself
