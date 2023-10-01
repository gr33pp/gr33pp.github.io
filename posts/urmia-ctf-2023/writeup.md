# Urmia CTF 2023

Solved Challenges:

### Misc
-  Warm Up
-  Appellations
-  Any Questions?

### Forensics
-  HTTPS Decryption
-  Hidden Streams
-  Deleted Message
-  Network Punk


### OSINT
-  Cryptic Mansion

### Steganography
-  Dorna
-  Deb File The Old Systems
  
### Cryptography
-  Insider's Secret
  
### Web
-   captcha2 the Missing Lake 2

  
### Warm Up
Category: Warmup

![Imgur](https://i.imgur.com/r1S2B4B.png)

flag: `UCTF{W3lc0m3_t0_URMIA}`

### Appellations
Category: MISC

![Imgur](https://i.imgur.com/rPfjNAA.png)

> Situated between East and West Azarbaijan  provinces, Lake Urmia was renowned as the largest saltwater lake across  the Middle East. Throughout the past century, it garnered various  significant designations. However, within this challenge, the focus lies  on unearthing one of its most splendid titles. Your task: decipher the  contemporary identity that adorns Lake Urmia today. Note that the flag  should be in this format: UCTF{flag}

Attachments: Information.mp3, Message.wav

I played Message.wav and I heard short and long beeps, it was Morse code.
Morse code is a method used in telecommunication to encode text characters using two different signal duration, called dots and dashes. It can be transmitted in many ways; written, light and sound, in this case etc. You can read more about Morse Code and its history on [Wikipedia](https://en.wikipedia.org/wiki/Morse_code).
I used [morsecode.world](https://morsecode.world) for this as the site can convert audio Morse code to readable text. It translated into `7U2QU01535011741230F4242841J4N`.

flag: UCTF{7U2QU01535011741230F4242841J4N}

### Any Questions
Category: MISC

![Imgur](https://i.imgur.com/h76LtiK.png)

> Play the famous "20 Questions" with many  questions, game with an AI bot, and try to guess the secret key! The  flag is the md5 of the key and is in this format UCTF{MD5(key)}.
 https://que.uctf.ir/

Summary: It's a fun game with an AI powered bot where you trick it to reveal information and construct flag from the responses. 

I asked the bot if the key contains numbers and it replied "no", then I began to ask the alphabets one by one if they are characters in the key . It replied yes for a, e, i, o, l, s, and t.

I asked "aeiolst" as the key then it gave a response:

>aeiolst :  Based on the given question "aeiolst", I cannot determine if the secret key "salt" is related to it. Therefore, my response is "No".

The secret key is "salt". I inputted salt to confirm if it's correct or not.

> Congrats! The key is "salt". You found the key!The flag is the md5 encryption of this Key!

![Imgur](https://i.imgur.com/ORWIqKf.png)

As requested by the challenge, we are required to submit the MD5 hash of the key, which is, `ceb20772e0c9d240c75eb26b0e37abee`.

flag: UCTF{ceb20772e0c9d240c75eb26b0e37abee}

### HTTPS Decryption
Category: Forensics

![Imgur](https://i.imgur.com/ZSsMol0.png)

> In this challenge, you are provided with a  file containing captured network packets and a file containing master  keys. Your task is to decrypt the HTTPS traffic and find the flag hidden  within the decrypted data. The target domain for this challenge is mrgray.xyz. Good luck!

Attachments: captured_packets.pcapng, master_keys.log

Summary: We are given a network capture file which contains secured HTTP traffic (HTTPS) and the key to do the decryption of the encrypted traffic. Using the key, flag can be retrieved in plaintext.

It took a bit before I discovered that the master_keys.log file is the TLS or SSL key to decrypting this captured HTTPS traffic, next I fired up my wireshark and imported the .log file as TLS key as preference, as of writing can be replicated by going through the following steps. 

- Open wireshark and open **captured_packets.pcapng**.
- Go to **Edit** > **Preferences** > **Protocols** > **TLS** 
- In the **(Pre)-Master-Secret log filename** section, browse and import **master_keys.log**.

By following the steps, the traffic will be decrypted and flag can be found in packet 72. Remember to click on the **Decrypted TLS** tab.

![Imgur](https://i.imgur.com/16QTZEi.png)

flag: `uctf{St. _Sarkis_Church}`

### Hidden Streams
Category: Forensics

![Imgur](https://i.imgur.com/mOdRo9g.png)

> Explore the available streams and consider the different types of data that can be associated with a single filename. Good luck!

Attached file: stream-ctf.zip
Summary: You have to open a Microsoft Disk Image and retrieve the flag

#### Unzipping the ZIP
The zip file unzipped gave `stream-ctf.vhd` file which was a `Microsoft Disk Image, Virtual Server or Virtual PC, Creator win  a.0 (W2k) Tue Aug 15 07:26:30 2023, 33554432 bytes, CHS 963/4/17` (file command).

#### Digging for files
I loaded Autopsy to see if I can find files in it. I found 2 files related to the flag; flag.zip and flag.zip:look-behind.
Since files are arranged alphabetically on autopsy, I indeed looked behind. Flag.zip was a text file containing `password:Atoosa` while `flag.zip:look-behind` was an actual zip file. I extracted the content with the provided password and I got `uctf_flag.txt` file which contains the flag.

flag: `uctf{St. Mary Church}`

### Deleted Message
Category: Forensics

![Imgur](https://i.imgur.com/5EPHNME.png)

> Cyber Police have seized a computer containing illegal content, but the data stored is secured with a password. A member of the criminal organization owning the computer was  arrested. Police suspect that the password was sent to the criminal via  SMS, but the message was deleted right before the arrest. You're given a dump of the data partition of the phone (running  Android 6.0). Your job as the forensic specialist is to recover the  deleted password.
 
 Attachment: data.tar.gz
#### Data extraction
I extracted the tar gzip file which contains the data partition of the phone. App data is normally stored in the data directory, so I went for it first. I found com.android.messaging.
 
For messsages, there was a `databases` directory and we have `bugle_db-journal` and `bugle_db` which contains the database of messages. I found the flag in table `parts` and column `texts`

flag: `uctf{l057_1n_urm14}`

### Network Punk
Category: Forensics

![Imgur](https://i.imgur.com/ogvzT7C.png)

> Some cyberpunk hide the flag inside a  network traffic. We have dumped the traffic. Your task is to find the  flag to save the city.

Attachment: traffic.pcap

I didn't bother to open it. I ran strings and found junks in the output, I ran strings again in full screen and I saw that it did formed the text of the flag

![Imgur](https://i.imgur.com/jgntomo.png)

flag: `uctf{urm14_n3tw0rk}`

### Cryptic Mansion
Category: OSINT
> 🏰 Cryptic Mansion
> 🕵️‍♂️ Welcome, intrepid digital detectives, to the "Cryptic Mansion"  challenge! Are you ready to put your OSINT skills to the ultimate test?  Get ready to embark on a virtual journey that will lead you through  twists and turns, all while unveiling the secrets hidden within a single  image.
 
> Challenge Description:
> Nestled within the pixels of a single image lies the enigmatic  "Cryptic Mansion." Your mission, should you choose to accept it, is to  reveal the well-guarded location of this elusive villa. You might be  thinking, "How hard could it be to find a villa?" But this isn't just  any villa—it's cloaked in mystery, designed to challenge even the most  seasoned OSINT adventurers.
 
> The Image:
> Before you stands a captivating image of a luxurious villa. The  details are alluring, but don't be fooled by appearances. This image  holds the key to a virtual realm that conceals the villa's true  whereabouts. A single image, they say, can contain a thousand secrets,  and it's your task to extract them.
 
> The Quest:
>  Your first step is to deploy reverse image search tools, carefully  analyzing each pixel for traces that will lead you on this thrilling  journey. You'll delve into the depths of the web, employing your skills  to uncover the origin, the history, and the real-world counterpart of  this captivating mansion.
 
> Unveiling the Flag:
> 🏆 Victory awaits those who successfully unveil the Cryptic Mansion's  exact location. As you navigate the labyrinth of data, keep an eye out  for the golden key—a distinctive link that opens the gates to Google  Maps. Within this link, you'll discover the latitude and longitude  coordinates that pinpoint the villa's precise location.

> When you find the Google Maps link, it will have a structure like this:
> https://goo.gl/maps/VMdjyjA7xs8E2E5s6
> Extract the latitude and longitude from the link. For example, latitude is 37.123456789012345, and longitude is 45.987654321098765.
> Then, use these coordinates to construct the flag in the following format:
> UCTF{37.123456789012345, 45.987654321098765}
> This challenge not only tests your OSINT prowess but also your  geolocation skills. Are you ready to showcase your expertise in  pinpointing the exact location of the Cryptic Mansion?
> Now, the example flag contains random values with the exact numbers after the decimal point.
> This is more than just a challenge; it's an opportunity to showcase  your OSINT prowess, outsmarting the virtual world's intricate puzzles to  emerge as the ultimate Cryptic Mansion conqueror.
> Are you ready to embark on a journey through pixels and  pathways? Will you unravel the hidden truths of the villa's location?  The Cryptic Mansion awaits your investigative finesse. Good luck,  digital detectives!
 
File attached: Mansion.jpg

![Imgur](https://i.imgur.com/zSVOewE.jpg)
 Mansion.jpg

#### Mansion, where are you??

I started by doing a reverse image search using tineye.com. I got the name of the building through an article by **asriran.com**. The site language was in Persian and I used google webpage translate to get it in English (I don't understand Persian :P). 

The article called this building **the Villa of Ashraf Pahlavi and Behrouz Vostoghi** which is located  in the middle of Lake Urmia.

![Article](https://i.imgur.com/BBWpoes.png)
Screenshot from Translated article

#### Give me your number o‿O
I searched on google maps for the villa, I ended up with this coordinates which can be gotten by right-clicking on the map pin. Coordinates: 37.496805716848954, 45.63767444207702 .

![Map](https://i.imgur.com/VTHwtbQ.png)
 Screenshot of map
 
flag: `UCTF{37.496805716848954, 45.63767444207702}`

References
1. Original asriran.com article [link](https://www.asriran.com/fa/news/298249/%D9%88%DB%8C%D9%84%D8%A7%DB%8C-%D8%A7%D8%B4%D8%B1%D9%81-%D9%BE%D9%87%D9%84%D9%88%DB%8C-%D9%88-%D8%A8%D9%87%D8%B1%D9%88%D8%B2-%D9%88%D8%AB%D9%88%D9%82%DB%8C-%D8%AF%D8%B1-%D9%88%D8%B3%D8%B7-%D8%AF%D8%B1%DB%8C%D8%A7%DA%86%D9%87-%D8%A7%D8%B1%D9%88%D9%85%DB%8C%D9%87)
2. Translated article [link](https://www-asriran-com.translate.goog/fa/news/298249/%D9%88%DB%8C%D9%84%D8%A7%DB%8C-%D8%A7%D8%B4%D8%B1%D9%81-%D9%BE%D9%87%D9%84%D9%88%DB%8C-%D9%88-%D8%A8%D9%87%D8%B1%D9%88%D8%B2-%D9%88%D8%AB%D9%88%D9%82%DB%8C-%D8%AF%D8%B1-%D9%88%D8%B3%D8%B7-%D8%AF%D8%B1%DB%8C%D8%A7%DA%86%D9%87-%D8%A7%D8%B1%D9%88%D9%85%DB%8C%D9%87?_x_tr_sl=auto&_x_tr_tl=en&_x_tr_hl=en&_x_tr_pto=wapp)
3. Google map [link](https://www.google.com/maps/place/37%C2%B029'48.5%22N+45%C2%B038'15.6%22E/@37.4968092,45.6355627,541m/data=!3m2!1e3!4b1!4m4!3m3!8m2!3d37.4968057!4d45.6376744?entry=ttu)
   
### Dorna
Category: Steganography

![Imgur](https://i.imgur.com/bJ7XTJF.png)

I'm hiding somewhere. Find me if you can!!  if you need a password anywhere use this "urumdorn4"

Attachment: Dorna.jpg 
 
Thinking of image steganography, Steghide is a popular method that requires password for decryption and supports JPG files.
Steghide is a steganography program that is able to hide data in various kinds of image- and audio-files. The color- respectivly sample-frequencies are not changed thus making the embedding resistant against first-order statistical tests.
Features of Steghide
- compression of embedded data
- encryption of embedded data
- embedding of a checksum to verify the integrity of the extraced data
- support for JPEG, BMP, WAV and AU files

So, I tried using Steghide and I got a txt file `dorn4.txt` as output.

```
$ steghide extract -sf Dorna.jpg
Password: 
Success, file extracted to dorn4.txt
```
 
Content of dorn4.txt:
 
```
Hello, wish you success in our event

'dorna lar yovasi' is the nickname of a stadium in Urmia where volleyball lovers gather together.
This place has hosted important competitions such as the VNL and the Asian Championship.

flag : uctf{ZG9ybmFfbGFyX3lvdmFzaQ==}    *base64-encoded
 ```
 
flag is given but the main text encoded in base64. Decryption gave the flag.
 
flag `uctf{dorna_lar_yovasi}`

### Deb File The Old Systems
Category: Steganography

![Imgur](https://i.imgur.com/2fLftLg.png)

> Can you believe it? people still use linux?  after the emerge of Evil E computers, nobody bothered to use linux  systems. anyways, we got this file from database gaurds' pc, can you  help us?

Attachment: uctfdeb-0.0.1.deb

This is a debian package installation file . To figure out what it contains, I extracted it as an archive.

It contains two directories DEBIAN and usr, usr contains the binary and the DEBIAN contains `postinst` binary and `control` text file. 

```
Package: uctfdeb
Version: 0.0.1
Homepage: https://uctf.ir
Maintainer: UCTF Support https://t.me/uctf_support_bot
Architecture: amd64
Description: You can find the flag in your tmp directory under UCTFDEB folder
    only after installation!

```
control

So I proceeded with the instructions. The binary generates a temporary file and saves it in the /tmp/UCTFDEB/dont-delete-me folder .

flag: `UCTF{c4n_p3n6u1n5_5urv1v3_1n_54l7_w473r}`

### Insider's Secret
Category: Cryptography

![Imgur](https://i.imgur.com/qYLJp47.png)

> "Craving a peek into my mysterious identity vault? Flex your decryption muscles and tackle this challenge:"

Summary: Base64 encoding

 ```
 Vm14V1QxWldTblZqTTJoWlpXeEtNRmRJY0VaTlIwWTJWRzFhYTFaRmNEQlVWbEpUVDFFOVBRPT0=
 ```
 
 Passing it through base64 four times brought the flag to life. Which can be easily done with the base64 command in the terminal
```
$ echo 'Vm14V1QxWldTblZqTTJoWlpXeEtNRmRJY0VaTlIwWTJWRzFhYTFaRmNEQlVWbEpUVDFFOVBRPT0=' | base64 -d | base64 -d | base64 -d | base64 -d

UCTF{1_4m_14k3_u2m14}
```
 
 flag: `UCTF{1_4m_14k3_u2m14}`

### captcha2 the Missing Lake 2

![Imgur](https://i.imgur.com/jgdGfnn.png)

> Sorry for bothering you again! We forgot to  retrieve some valuable assets the last time. They have changed their  captcha system, I think they know that we know about OCRs :)

#### OxManual 

From the first captcha challenge, I deduced the url https://captcha1.uctf.ir/  to captcha2*

I did the 100 captchas available manually!! Do not panic!!.  My teammate wrote a script to sort it :)  [LINK](https://github.com/SENSEIXENUS2/Ctf-writeupsScripts/blob/main/UctfWriteups/captcha2.py)

flag: UCTF{Arm3n1an_m0uflon}

And.. Check out the continuation on [HERE](https://github.com/SENSEIXENUS2/Ctf-writeupsScripts/blob/main/UctfWriteups/Writeup.md) and [HERE](https://h4ckyou.github.io/posts/ctf/uctf/writeup.html) . 
Thanks for reading.. 
