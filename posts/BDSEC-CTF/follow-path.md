## Follow The Path
### Category: Networking

![image of challenge](https://i.imgur.com/vjfEeM8.png)

The task was to find the path of the Admin endpoint.
From the log, the attacker was fuzzing for directories and he/she found the admin endpoint and login page. 

![Image of solution](https://i.imgur.com/zE58TRe.png)

The endpoint is /app/admin_panel.

Flag: `BDSEC{/app/admin_panel}`
