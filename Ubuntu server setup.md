**login**

ssh root@123.123.123.123

**install updates**

apt-get update && apt-get upgrade

**configure automatic updates**

https://help.ubuntu.com/lts/serverguide/automatic-updates.html

**create a sudo user**

```bash
adduser example_user
adduser example_user sudo
```

**install ssh keys**

On the server, as your new user:

```bash
mkdir ~/.ssh
chmod 700 ~/.ssh
```

On your Mac:

`scp ~/.ssh/id_rsa.pub example_user@203.0.113.0:~/.ssh/authorized_keys`

You should be able to `ssh` to this machine now, if you get prompted for the password for example_user you've probably not got teh correct permissions or ownership on the .ssh folder.

**disable root login**

`sudo vim /etc/ssh/sshd_config`

Update to:
>PermitRootLogin no
