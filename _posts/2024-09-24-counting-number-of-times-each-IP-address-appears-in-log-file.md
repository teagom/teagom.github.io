# Counting number of times each IP address appears in log file.
## How to print a total of hits per IP?

I will use the common log of apache2
```
/var/log/apache2/access.log
```

This is the format of access.log, I want to print total of hits per IP.
```
192.168.0.x - - [24/Sep/2024:02:03:55 -0300] "GET / HTTP/1.1" 200
```

To explain parts of last command line
1 print only IP column
```
cd /var/log/apache2
more access.log | awk '{print $1}'
# output
89.208.11.10
45.148.10.242
95.214.55.138
45.148.10.242
```

2 sort IP list
```
more access.log | awk '{print $1}' | sort
# output
89.208.11.y
89.208.11.y
89.208.11.y
95.214.55.x
95.214.55.x
95.214.55.x
95.214.55.x
```

3 counter total of hits per IP
```
more access.log | awk '{print $1}' | sort | uniq -c
# output
 1 141.98.11.122
 1 178.211.139.188
 2 185.16.39.118
 1 185.224.128.47
 1 35.177.209.183
98 45.148.10.242
 1 45.84.89.2
 1 46.174.191.30
 1 52.228.160.228
 2 5.8.11.202
 3 65.49.20.67
 1 79.124.59.226
 1 79.124.8.107
 1 81.17.22.122
 1 82.157.247.165
 2 89.190.156.137
10 89.208.11.10
30 95.214.55.138
 2 95.214.55.43
 ```

## Custom filter
Filter 40x apache2 error, counter total of hits per IP.
```
more access.log | grep '\" 40[0|1|2|3|4]' | awk '{print $1}' | sort | uniq -c
```

Filter 200 apache2 success, counter total of hits per IP.
```
more access.log | grep '\" 200' | awk '{print $1}' | sort | uniq -c
```
