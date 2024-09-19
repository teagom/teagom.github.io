# PFSense commands
## Easy and direct commands for PFSense and FreeBSD

The following command adds a firewall rule, allowing tcp traffic in on port 443 from remote IP XX.XX.XX.XX: to the WAN IP on YY.YY.YY.YY:
```sh
easyrule pass wan tcp XX.XX.XX.XX YY.YY.YY.YY 443
```
You can also allow SSH access and set up a remote port forward (ssh -L localport:remoteip:remoteport remoteip):
```sh
easyrule pass wan tcp XX.XX.XX.XX YY.YY.YY.YY 22
```

Traffic network
```
iftop -i re0 -F -P -o 2s
```

## Nginx don't start, service nginx one restart
**erro**
```
Performing sanity check on nginx configuration:
nginx: [emerg] cannot load certificate key "/usr/local/etc/nginx/cert.key": BIO_new_file() failed (SSL: error:02001002:system library:fopen:No such file or directory:fopen('/usr/local/etc/nginx/cert.key','r') error:2006D080:BIO routines:BIO_new_file:no such file)
nginx: configuration file /usr/local/etc/nginx/nginx.conf test failed
```
**to fix**
```
cd /usr/local/etc/nginx
openssl req -x509 -newkey rsa:4096 -sha256 -nodes -keyout cert.key -out cert.pem -days 3650
```
