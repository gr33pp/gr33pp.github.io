## Compromised Account
### Category: Networking

![Image of challenge](https://i.imgur.com/VyAbhI7.png)

We were told to find the account that was compromised as a result of the attack. Going through the packets, I found multiple HTTP POST request trying to bruteforce the login page.

![Image of clue](https://i.imgur.com/S6LJupc.png)

In the picture, packet 7025 was the last bruteforce attempt and the response, packet 7027 gave a login successful reponse and a 302 redirect to the dashboard.

![Image of solution](https://i.imgur.com/5Ot4HO9.png)

Here we can see the email and password as `tareq@gmail.com` and `tareq@nanomate` respectively. On the dashboard response packet, we could see the username as tareq.

Flag: `BDSEC{tareq_tareq@nanomate}`