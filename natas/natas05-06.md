## Level5 -> Level6


Now the web page as a submit button for secrets. 


It also has a link when clicking will show the source-code.


Here's the source code. 


```php
<?

include "includes/secret.inc";

    if(array_key_exists("submit", $_POST)) {
        if($secret == $_POST['secret']) {
        print "Access granted. The password for natas7 is <censored>";
    } else {
        print "Wrong secret";
    }
    }
?>
```


The web page is written in [PHP](https://en.wikipedia.org/wiki/PHP).


The source code tells us that if we submit `$secret` it will print the password. 


Since the php code includes `includes/secret.inc` it would be a good idea to check that file.


After changing the url to [includes/secret.inc](http://natas6.natas.labs.overthewire.org/includes/secret.inc).


It shows you the value of secret.  


```php 
<?
$secret = "FOEIUWGHFEEUHOFUOIU";
?>
```


Copy the `$secret` value without the `""` and submit it as the secret. 


The web page changes and you'll get the password for the next level.


```html 
Access granted. The password for natas7 is B1szg95UcTnrzwnF3i3TzYHlyYh8iBV0
```

Here are some links helpful to solving the challenge.


### 1. [What is a .inc in php?](https://stackoverflow.com/questions/7129842/what-is-an-inc-and-why-use-it
)


### 2. [Why does php use $ in variables?](https://stackoverflow.com/questions/3073812/why-php-variables-start-with-a-sign-symbol
) 


### 3. [What is $_POST in php?](https://stackoverflow.com/questions/1039797/what-is-the-purpose-of-post 
) 


### 4.[Why does php start with a <?](https://www.reddit.com/r/PHP/comments/1mprxiw/why_should_a_php_file_always_start_with_that_ugly/ 
) 

You can still solve the challenge without understanding PHP, I think it's a good chance to learn a little bit. 

Doing so will deepen your knowledge on web in general. 