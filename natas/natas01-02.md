## Level1 -> Level2


It says there's nothing on the page, but to check if it's really true you have to inspect the page source. 


Use the methods explained in [natas0](https://github.com/hwkim301/OvertheWire/blob/master/natas/natas00-00.md) to view the page source. 


When checking the page source you can see that there is a link to an image file.


```html
<img src="files/pixel.png">
```


The image(pixel.png) looks like a black picture without any important information, however when you move a directory up to the `files` directory(http://natas2.natas.labs.overthewire.org/files/) there's another file named `users.txt`.


Let's check the `users.txt` file.


```
# username:password
alice:BYNdCesZqW
bob:jw2ueICLvT
charlie:G5vCxkVV3m
natas3:3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH
eve:zo4mJWyNj2
mallory:9urtcpzBmH
```


It looks like it stores password using a key,value like structure, and the password for the next level is in it. 