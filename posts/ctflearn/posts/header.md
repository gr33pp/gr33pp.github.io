## Don't Bump Your Head(er)
### Difficulty : Medium

![Image of challenge](https://i.imgur.com/RXKGY7b.png)

http://165.227.106.113/header.php

On opening the site this messsage shows up

![Image of site](https://i.imgur.com/x2r0Z6i.png)

Checking the site's source... 

![source](https://i.imgur.com/dEvRgHB.png)

We get the obvious user agent. ```Sup3rS3cr3tAg3nt```. Next, I used curl

```                                                                                        
┌──(gr33pp㉿kali)
└─$ curl -A Sup3rS3cr3tAg3nt http://165.227.106.113/header.php 
Sorry, it seems as if you did not just come from the site, "awesomesauce.com".
<!-- Sup3rS3cr3tAg3nt  -->
```

Setting my user agent as Sup3rS3cr3tAg3nt gave the next clue. This is requiring a referrer header of ```awesomsauce.com``` to proceed

```                                                                                                                         
┌──(gr33pp㉿kali)
└─$ curl -A Sup3rS3cr3tAg3nt -e awesomesauce.com http://165.227.106.113/header.php 
Here is your flag: flag{did_this_m3ss_with_y0ur_h34d}
<!-- Sup3rS3cr3tAg3nt  -->
```

And, done.. More like easy challenge
flag : ```flag{did_this_m3ss_with_y0ur_h34d}```
