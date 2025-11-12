
### Level20->Level21


Like last time another setuid ELF file is given.


```bash 
file suconnect 
suconnect: setuid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, BuildID[sha1]=a95f034b2749e585fbeed4f260f85a4b150934c2, for GNU/Linux 3.2.0, not stripped
```


Here's the usage of the setuid binary. 


```
./suconnect 
Usage: ./suconnect <portnumber>
This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted bac
```


In order to pass the level you need to connect to `localhost` on a port and send the password of `bandit20`. 


We can pass the `bandit19` password with a pipe and use `nc -l` (listen option) to listen to a certain port. 


Here's the man page for `nc -l`.


```
-l  Listen for an incoming connection rather than initiating a connection to a remote host.  The destination and port to listen on can be specified either as non-optional arguments, or with  options  -s and -p respectively.  Cannot be used together with -x or -z.  Additionally, any timeouts specified with the -w option are ignored.
```


One important fact is that you need to run the `nc` command in the background using `&` because, without `nc` will wait for an incoming connection which will block you from using your terminal. 


In effect won't let you run the setuid binary, although we need to run it to make a `TCP` connection to `localhost`.


```bash   
echo 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO | nc -lp 1234 &
```


```bash 
./suconnect 1234
Read: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
Password matches, sending next password
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```