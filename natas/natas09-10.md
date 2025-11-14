## Level9 -> Level10


Now for security reasons `natas` filters certain characters. 


Here's the source code.


```php
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    if(preg_match('/[;|&]/',$key)) {
        print "Input contains an illegal character!";
    } else {
        passthru("grep -i $key dictionary.txt");
    }
}
?>
```


It's almost identical to the level before, but there's an `if` statement that uses the `preg_match` function to check whether characters `;`, `|`, `&` are used.


This means that we won't be able to chain commands like we did in the last level.


However, instead of chaining commands you can pass a single character that's in the password. 


It that character is in the password the webpage will show it because it uses `grep -i` to show any matches. 


For me I tried entering `a /etc/natas_webpass/natas11` because, `a` is a vowel and is one of the most used characters in English. 


At the very top of the output you could see the password did have an `a` or `A` in it. 


```bash 
/etc/natas_webpass/natas11:UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk
```


If your password is different try other characters and start with the vowels first. 


Vowels are more prevalent in English than consonants. 


### 1. What does the preg_match function in php do? 


https://www.php.net/manual/en/function.preg-match.php


https://stackoverflow.com/questions/5382401/can-anyone-explain-to-me-what-this-preg-match-function-does


