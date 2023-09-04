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
![Imgur](https://i.imgur.com/r1S2B4B.png)

flag: `UCTF{W3lc0m3_t0_URMIA}`

### Appelations
![Imgur](https://i.imgur.com/rPfjNAA.png)

> Situated between East and West Azarbaijan  provinces, Lake Urmia was renowned as the largest saltwater lake across  the Middle East. Throughout the past century, it garnered various  significant designations. However, within this challenge, the focus lies  on unearthing one of its most splendid titles. Your task: decipher the  contemporary identity that adorns Lake Urmia today. Note that the flag  should be in this format: UCTF{flag}

Attachments: Information.mp3, Message.wav

I played Message.wav and I heard beeps, it was morse code. I used morsecode.world for this. It translated into `7U2QU01535011741230F4242841J4N`

flag: UCTF{7U2QU01535011741230F4242841J4N}

### Any Questions
![Imgur](https://i.imgur.com/h76LtiK.png)

> Play the famous "20 Questions" with many  questions, game with an AI bot, and try to guess the secret key! The  flag is the md5 of the key and is in this format UCTF{MD5(key)}.
 https://que.uctf.ir/
                                                                                       
I asked the bot if the key contains numbers and it replied "no", then I began to ask the alphabets one by one if they are characters in the key . It replied yes for a, e, i, o, l, s, and t.

I asked "aeiolst" as the key then it gave a response:

>aeiolst :  Based on the given question "aeiolst", I cannot determine if the secret key "salt" is related to it. Therefore, my response is "No".

The secret key is "salt". I inputted salt to confirm if it's correct or not.

> Congrats! The key is "salt". You found the key!The flag is the md5 encryption of this Key!

![Imgur](https://i.imgur.com/ORWIqKf.png)

Next, I did the md5 of “salt”, which is , `ceb20772e0c9d240c75eb26b0e37abee`

flag: UCTF{ceb20772e0c9d240c75eb26b0e37abee}

### HTTPS Decryption
![Imgur](https://i.imgur.com/ZSsMol0.png)
> In this challenge, you are provided with a  file containing captured network packets and a file containing master  keys. Your task is to decrypt the HTTPS traffic and find the flag hidden  within the decrypted data. The target domain for this challenge is mrgray.xyz. Good luck!

Attachments: captured_packets.pcapng, master_keys.log

It took a bit before I discovered that the master_keys.log file is the TLS or SSL key to decrypting this captured HTTPS traffic, next I fired up my wireshark and imported the log file as TLS key as preference. Boom, the traffic was decrypted.

The flag can be found in packet 72 

![Imgur](https://i.imgur.com/16QTZEi.png)

flag: `uctf{St. _Sarkis_Church}`

### Hidden Streams
![Imgur](https://i.imgur.com/mOdRo9g.png)

> Explore the available streams and consider the different types of data that can be associated with a single filename. Good luck!

Attached file: stream-ctf.zip

The zip file unzipped gave `stream-ctf.vhd` file which was `Microsoft Disk Image, Virtual Server or Virtual PC, Creator win  a.0 (W2k) Tue Aug 15 07:26:30 2023, 33554432 bytes, CHS 963/4/17` (file command).

I loaded Autopsy to see if I can find files in it. I found 2 files related to the flag; flag.zip and flag.zip:look-behind.

Since files are arranged alphabetically on autopsy, I indeed looked behind. Flag.zip was a text file containing `password:Atoosa` while `flag.zip:look-behind` was an actual zip file. I extracted the content with the provided password and I got `uctf_flag.txt` file which contains the flag.

flag: `uctf{St. Mary Church}`

### Deleted Message
![Imgur](https://i.imgur.com/5EPHNME.png)
> Cyber Police have seized a computer containing illegal content, but the data stored is secured with a password.
 A member of the criminal organization owning the computer was  arrested. Police suspect that the password was sent to the criminal via  SMS, but the message was deleted right before the arrest.
> You're given a dump of the data partition of the phone (running  Android 6.0). Your job as the forensic specialist is to recover the  deleted password.
 
 Attachment: data.tar.gz
 
 I extracted the tar gzip file which contains the data partition of the phone. App data is normally stored in the data directory, so I went for it first. I found com.android.messaging
 
For messsages, there was a `databases` directory and we have `bugle_db-journal` and `bugle_db` which contains the database of messages. I found the flag in table `parts` and column `texts`

flag: `uctf{l057_1n_urm14}`

### Network Punk
![Imgur](https://i.imgur.com/ogvzT7C.png)
> Some cyberpunk hide the flag inside a  network traffic. We have dumped the traffic. Your task is to find the  flag to save the city.

Attachment: traffic.pcap

I didn't bother to open it. I ran strings and found junks in the output, I ran strings again in full screen and I saw that it did formed the text of the flag

![Imgur](https://i.imgur.com/jgntomo.png)

flag: `uctf{urm14_n3tw0rk}`

### Cryptic Mansion
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
 
 I started by doing a reverse image search using Tineye.com. I got the name of the building through an article then I searched on google maps for the building coordinates. Coordinates: 37.496805716848954, 45.63767444207702 .

(Check the name of the building for yourself : )
 
 flag: `UCTF{37.496805716848954, 45.63767444207702}`

