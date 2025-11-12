### Level14-> Level15


You don't need to ssh this time, just continue from where you left last time. 


To get to the next level I need to send the password for the current level to port `30000` on `localhost`.


Here's the password of the current level. 


```bash
cat /etc/bandit_pass/bandit14
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```


Use the `netcat(nc)` command to connect to ip ports. 


When using netcat you can pass the port number after the ip address. 


You then need to send the password to `localhost`. 


What exactly is `localhost`?


We usually communicate with other computers like Google's server, or Disney ... etc , but sometime we don't want to communicate to other computers. 


For example, when you open a web server you want the results to show on your computer. 


In cases like this, instead of sending a request to otehr cmoputers you want to test your local development results we use an ip.address (127.0.0.1) aka localhost. 


It's a loopback address that points to your computer instead of sending it to other ip addresses. 



```
nc localhost 30000 
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
Correct!
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

For more information read this post. 

https://www.reddit.com/r/learnpython/comments/3bgffc/meaning_of_localhost/ 
