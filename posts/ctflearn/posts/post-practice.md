## POST practice
### Difficulty: Medium

![image-of-challenge](https://i.imgur.com/myNibjN.png)

http://165.227.106.113/post.php

![image-of-site](https://i.imgur.com/WV2I5iY.png)

Checking the site's source code, I found the credentials. ```username: admin | password: 71urlkufpsdnlkadsf```. 

![image-source](https://i.imgur.com/l9PF8wv.png)

To authenticate and get the flag, I sent post request using burp to the url.

![image-of-burp](https://i.imgur.com/XT8oRyv.png)

Easiest way is to use curl or wget. Here, I used curl.

```
┌──(gr33pp㉿machine)
└─$ curl -d "username=admin&password=71urlkufpsdnlkadsf" -X POST http://165.227.106.113/post.php
<h1>flag{p0st_d4t4_4ll_d4y}</h1>                                                                                               
                      
```
This looks more like ```easy```

flag ```flag{p0st_d4t4_4ll_d4y}```
