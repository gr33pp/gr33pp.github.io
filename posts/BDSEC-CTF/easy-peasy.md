## E4sy Pe4sy OSINT
### Category: OSINT

![challenge image](https://i.imgur.com/bd4USGN.png)

> A few days ago I went to meet a friend of mine. I took a picture while we were talking. Can you tell me where we met?

![picture](https://i.imgur.com/efFdGE6.jpg)

My first attempt is to do EXIF check with exiftool to see if the gps loaction was added to the metadata, it didn't prove much of help as there was no gps data. Next is to do a reverse image search, I tried google and bing and I did't get much. Next I tried to look into the photo for clues for where it could be. I saw a logo showing "STAR". I found the exact logo online and it belongs to a Bangladesh tech company called STAR Tech. I thought Star tech was the location but I was wrong.

I began to look for star tech on the map and check photos of it but no avail. Next, i found Star Cineplex, it had the same logo as Star Tech. On more attention on the map, I found Sony Square, it has a STAR Cineplex section and I found a similar photo too.

![similar photo](https://i.imgur.com/wAefV3w.png)

It was it!

Flag:`BDSEC{Sony_Square}`
