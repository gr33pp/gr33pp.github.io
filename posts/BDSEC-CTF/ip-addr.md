## IP Addr
### Category: Networking

![image of challenge](https://i.imgur.com/NGeL5Vq.png)

On opening the challenge.pcapng file, it was a pretty big file. Well, the challenge was asking what the attacker and server ip was.

![image proof](https://i.imgur.com/mmJBoXe.png)

We can see that 192.168.1.7 was sending SYN packets but recieved RST packets in repeatedly. One could say that 192.168.1.7 was scanning because it was reapeated several times.

Attacker IP : `192.168.1.7`
Server IP : `192.168.1.5`

flag: `BDSEC{192.168.1.5_192.168.1.7}`
