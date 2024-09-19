# Basic commands and tools

### Merge PDF files
```
gs -dBATCH -dNOPAUSE -q -sDEVICE=pdfwrite -dAutoRotatePages=/None -sOutputFile=finished.pdf  rg2020.pdf rg2020-ver.pdf 
```


### How to print a total of register from a table? Total COUNT in postgreSQL.
To create a file with the follow content:
```
echo "SELECT COUNT(*) FROM client_client WHERE confirmed=1;"  > /tmp/command.sql
```
Print date time and total of occurences 5 to 5 minutes, sleep command work's in seconds,
crtl+c to out. Execute the command as postgres user.
```
su - postgres 
while [ -z ]; do date && psql -d mydatabase < command.sql; sleep 300; done
```


### The best traffic monitoring
```
iptraf-ng
```


### My current IP address via line command
```
curl checkip.amazonaws.com
curl ifconfig.me
curl icanhazip.com
curl ipecho.net/plain
curl ifconfig.co
```


### Show resume of process and use memory for each service
```
https://github.com/pixelb/ps_mem
git clone https://github.com/pixelb/ps_mem.git
```
