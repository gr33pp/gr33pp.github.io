## Old Client Area
### Category: OSINT

[image of challenge](https://i.imgur.com/xjIubVC.png)

> Our sponsor NS TechValley recently changed their billing system and moved the billing/client area to a new domain/sub-domain. Can you fnd the old billing area domain/sub-domain?

Here I just need to list the subdomains or find a domain link on the site's page. I did a passive recon with crt.sh . I found this..

[Image of crt.sh](https://i.imgur.com/NL8xDVn.png)
 
On visiting clients.nstechvalley.com, it was redirected to the new subdomain. The new page contained the billing area. So the flag

flag: `BDSEC{clients.nstechvalley.com}`
