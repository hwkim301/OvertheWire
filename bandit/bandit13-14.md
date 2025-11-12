### Level13-> Level14


```bash
ssh -p 2220 bandit13@bandit.labs.overthewire.org
```


```bash
file sshkey.private 
sshkey.private: PEM RSA private key
```


This time a ssh private key is given and it looks like it's `base64` encoded. 


```
cat sshkey.private
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----
```


If you've never used an ssh key file this is going to be pretty hard so I'll just give the solution right away. 


You can `ssh` into another machine using the ssh key with the `ssh -i` tack, below is the man page of it. 


```
-i identity_file
    Selects  a  file  from  which  the  identity (private key) for public key authentication is read.  You can also specify a public key file to use the corresponding private key that is loaded in
    ssh-agent(1) when the private key file is not present locally.  The default is ~/.ssh/id_rsa, ~/.ssh/id_ecdsa, ~/.ssh/id_ecdsa_sk, ~/.ssh/id_ed25519,  ~/.ssh/id_ed25519_sk  and  ~/.ssh/id_dsa.
    Identity  files may also be specified on a per-host basis in the configuration file.  It is possible to have multiple -i options (and multiple identities specified in configuration files).  If
    no certificates have been explicitly specified by the CertificateFile directive, ssh will also try to load certificate information from the filename obtained by appending -cert.pub to identity
    filenames.
```

But a problem arises when you try to `ssh` inside the remote server. 


```
bandit13@bandit:~$ ssh -p 2220  -i sshkey.private bandit14@bandit.labs.overthewire.org
The authenticity of host '[bandit.labs.overthewire.org]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit13/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit13/.ssh/known_hosts).
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

!!! You are trying to log into this SSH server with a password on port 2220 from localhost.
!!! Connecting from localhost is blocked to conserve resources.
!!! Please log out and log in again.

backend: gibson-0
Received disconnect from 127.0.0.1 port 2220:2: no authentication methods enabled
Disconnected from 127.0.0.1 port 2220
```


Not a lot of writeups explained this error. 


The solution is to copy the sshkey to your local machine. 


You then might get an error regarding permissions.


```
ssh -p 2220 -i sshkey.private bandit14@bandit.labs.overthewire.org
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0644 for 'sshkey.private' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "sshkey.private": bad permissions
```


Bandit is complaining that the sshkey.priavte has more permissions that it's supposed to have. 


Changing the permission to owner-readonly then sshing will take you to the next level. 


```bash 
chmod 400 sshkey.private
```


We solved `bandit13` but here are some questions I had after solving the level. 



1. Why is the sshkey.private base64 encoded? 


It's because most of the times `base64` is used to transport binary data. 


base64 encodes binary data to `64` characters 0~9(10) + A~Z,a-z(52), and '+','/'(2) and will occasionally use '=' for paddings. 

Since binary characters include characters that aren't printable we need it to transfer it to format like `UTF-8` or ASCII which a lot of systems can handle.


By the way base64 decoding the RSA key won't print any meaningful text because the data itself is binary. 


I've actually tried decoding it, but it wasn't meaningful at all. 


2. Why does it use a RSA key? 


**[RSA](https://en.wikipedia.org/wiki/RSA_cryptosystem)** is one of the oldest assymetric encryption algorithms. 


In short it uses a pair of keys. 


The pair of keys are consisted of a private key and a public key. 


The private key as the name suggets is private and should be kept to yourself. 


It allows you to sign data, proving that you are the owner.


The private key is usually in `~/.ssh/id_rsa`.


The public is given to any server you want to login.


It goes to the server's `~/.ssh/authorized_keys` to verify you own the private key. 


The public key is usually in `~/.ssh/id_rsa.pub`. 


If you go inside your  `~/.ssh`  folder there are other files such as the `known_hosts` files but I think this is all I can explain.


I'm not good at crypo or math if you want to learn more have a look at **[cryptopals](https://cryptopals.com/)**


I found even the first few problems required a lot of Python and was pretty difficult LOL.