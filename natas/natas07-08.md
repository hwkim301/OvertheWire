## Level7 -> Level8


The design of the website looks exactly the same as the level before. 


There's a submit button for the secret, a link to view the source code. 


Here's the source code, you can see that the source code has gotten much more complex. 


```php
<?

$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}

if(array_key_exists("submit", $_POST)) {
    if(encodeSecret($_POST['secret']) == $encodedSecret) {
    print "Access granted. The password for natas9 is <censored>";
    } else {
    print "Wrong secret";
    }
}
?>
```


There's a `encodeSecret` function that base64 encodes `$secret` strrevs it and bin2hexs it. 


So we need to pass the correct `$secret` and it has to be equal to `$encodedSecret` after passing it to the `encodeSecret` function.


Since We only know the `$encodedSecret` and not the `$secret` we'll have to reverse the `encodeSecret` function to get `$secret`.


The `encodeSecret` does 3 things when `$secret` is taken as an argument. 


### 1. base64_encode 


https://www.php.net/manual/en/function.base64-encode.php


### 2. strrev


https://www.php.net/manual/en/function.strrev.php


### 3. bin2hex 

https://www.php.net/manual/en/function.bin2hex.php



We can take the exact opposite measures to get the `$secret` value.


An important thing is to start from reversing `bin2hex` because that was the last step in the `encodeSecret` function.


### 1. hex2bin 


To reverse the result of `bin2hex` you have to use the `hex2bin` function. 


https://www.php.net/manual/en/function.hex2bin.php


### 2. strrev 


You can reverse a same string twice to get the original non reversed string 


### 3. base64_decode 


The opposite of encoding is decoding. 


https://www.php.net/manual/en/function.base64-decode.php



Here's the php script I wrote. 


```php
$encodedSecret = "3d3d516343746d4d6d6c315669563362";

echo hex2bin($encodedSecret); # ==QcCtmMml1ViV3b 
echo "\n";
echo strrev(hex2bin($encodedSecret)); # b3V1iV1lmMmtCq==
echo "\n";
echo base64_decode(strrev(hex2bin($encodedSecret))); # oubWYf2kBq
```


Submitting the base64_decode final output will show you the password. 


```
Access granted. The password for natas9 is ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t
```


You can also use python instead of php, but I think it's a good idea to use php because natas is written in php.


```python
from base64 import b64decode 

encodedsecret="3d3d516343746d4d6d6c315669563362"
bytes.fromhex(encodedsecret) # b'==QcCtmMml1ViV3b'
b64decode(bytes.fromhex(encodedsecret)[::-1]) # b'oubWYf2kBq'
```