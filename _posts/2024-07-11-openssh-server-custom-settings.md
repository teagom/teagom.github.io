### OpenSSH - Custom settings for more security.

For more security change ssh port for a custom port, but a risk to sshd broken and you can lost server ssh access.
To test a custom settings before to the production

1.  How to do this in safe mode?
2.  How to avoid to lost ssh connection?

Enviromment
```
Linux Ubuntu Server 20.04 64
Required root access / sudo
```

Make backup of sshd_config file
```
cp /etc/ssh/sshd_config /etc/ssh/sshd_config.port22
cp /etc/ssh/sshd_config /etc/ssh/sshd_config.port5000
```

You can run a second instance of openssh-server using a custom configuration, make all change you need.
```
vim /etc/ssh/sshd_config.port5000
change port to 5000
Port 5000
```

To test the synta of custom config file
```
sshd -t -f /etc/ssh/sshd_config.port5000
```

Run a new server using new sshd_config
```
-4d: Ipv4 + debug
-f : config file
```
```
/usr/sbin/sshd -4d -f /etc/ssh/sshd_config.port5000
```
ctrl+c to stop
