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

Next, i found the md5 of “salt”, which is , `ceb20772e0c9d240c75eb26b0e37abee`

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

SInce files are arranged alphabetically on autopsy, I indeed looked behind. Flag.zip was a text file containing `password:Atoosa` while `flag.zip:look-behind` was an actual zip file. I extracted the content with the provided password and I got `uctf_flag.txt` file which contains the flag.

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

I didn't bother to open it. I ran strings and found junks in the output, I ran strings again in full screm and I saw that it formed the text of the flag


flag: `uctf{urm14_n3tw0rk}`
