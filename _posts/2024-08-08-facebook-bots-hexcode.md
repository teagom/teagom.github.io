## Facebook Bots flooding a web server, how to block?

A excessive / massive requests from facebook are flooding a web (apache2) server and freeze it for each 30 minutes.

Doubts
1.  Why hexa code found in the URL? Exploit memory address?
2.  Why massive and excessive requests?
3.  Are facebook-bots or attacker are using the game/app dev environment of facebook to do this?
4.  Bad robot?

/va/log/apache2/access.log

`173.252.107.x - - [01/Aug/2024:10:20:45 -0300] "GET
index?q=\xe7\xbb\x8d\xe5\x85\xb4\xe5\x93\xaa\xe9\x87\x8c\xe6\x9c\x89\xe6\x9c HTTP/1.1" 200 3847 "-" "facebookexternalhit/1.1
(+http://www.facebook.com/externalhit_uatext.php)"`

Count hits daily of apache access log
```
10.491 28/Jul/2024 without rule
 8.859 29/Jul/2024 without rule
 9.340 30/Jul/2024 without rule
 3.573 31/Jul/2024 without rule
 1.238 01/Aug/2024 with rule, 237 blocked IPs from 12h00 until 17h25.
```

To block, add this rule in the fail2ban service,
*/etc/fail2ban/filter.d/apache-facebook-hexcode.conf*
```
# Generic configuration items (to be used as interpolations) in other
# apache filters.
[Definition]
datepattern = ^[^\[]*\[({DATE})
failregex = ^<HOST> -.*(GET|POST|HEAD).*\\x[a-zA-Z0-9].*$
            ^<HOST> -.*facebookexternalhit.*$

ignoreregex =
```
