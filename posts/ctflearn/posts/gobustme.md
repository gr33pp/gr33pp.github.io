## Gobustme ?
### Difficulty: easy

![Imgur](https://i.imgur.com/35E42aM.png)

After checking the site and reading through the contents, only clue was the wordlist and repetitive mention of gobuster, I will enumerate even if it wasn't there. There was no link on the main page and nothing useful in the page source, nothing in the page response. Next I did directory brute with Gobuster.

![Imgur](https://i.imgur.com/XZVVpku.png)

![Imgur](https://i.imgur.com/KuALsIf.png)
```
┌──(gr33pp㉿machine)-[~/Documents/ctflearn/gobustme]
└─$ gobuster dir -u https://gobustme.ctflearn.com -w /seclists/Discovery/Web-Content/common.txt
===============================================================
Gobuster v3.5
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     https://gobustme.ctflearn.com
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.5
[+] Timeout:                 10s
===============================================================
2023/07/15 13:08:26 Starting gobuster in directory enumeration mode
===============================================================
/.well-known/http-opportunistic (Status: 200) [Size: 32]
/call                 (Status: 301) [Size: 169] [--> http://gobustme.ctflearn.com/call/]
/carpet               (Status: 301) [Size: 169] [--> http://gobustme.ctflearn.com/carpet/]
/flag                 (Status: 301) [Size: 169] [--> http://gobustme.ctflearn.com/flag/]
/hide                 (Status: 301) [Size: 169] [--> http://gobustme.ctflearn.com/hide/]
/index.html           (Status: 200) [Size: 2713]
/sex                  (Status: 301) [Size: 169] [--> http://gobustme.ctflearn.com/sex/]
/shadow               (Status: 301) [Size: 169] [--> http://gobustme.ctflearn.com/shadow/]
/skin                 (Status: 301) [Size: 169] [--> http://gobustme.ctflearn.com/skin/]
Progress: 4712 / 4716 (99.92%)
===============================================================
2023/07/15 13:10:31 Finished
===============================================================                          
```

/flag directory looked more like it could be but /hide gave the flag

![Imgur](https://i.imgur.com/rrHdYSL.png)

![Imgur](https://i.imgur.com/pHknpCi.png)
flag ```CTFlearn{gh0sbu5t3rs_4ever}```
