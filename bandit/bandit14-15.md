### Level15-> Level16


```bash
ssh -p 2220 bandit15@bandit.labs.overthewire.org
```


In this level you need to send the current password to `localhost` on port `30001` using `SSL/TLS` encryption. 


The `openssl` command  allows you to connect to `localhost` using `SSL/TLS`. 


```
openssl s_client -connect localhost:30001
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN = SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = SnakeOil
verify return:1
---
Certificate chain
 0 s:CN = SnakeOil
   i:CN = SnakeOil
   a:PKEY: rsaEncryption, 4096 (bit); sigalg: RSA-SHA256
   v:NotBefore: Jun 10 03:59:50 2024 GMT; NotAfter: Jun  8 03:59:50 2034 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIFBzCCAu+gAwIBAgIUBLz7DBxA0IfojaL/WaJzE6Sbz7cwDQYJKoZIhvcNAQEL
BQAwEzERMA8GA1UEAwwIU25ha2VPaWwwHhcNMjQwNjEwMDM1OTUwWhcNMzQwNjA4
MDM1OTUwWjATMREwDwYDVQQDDAhTbmFrZU9pbDCCAiIwDQYJKoZIhvcNAQEBBQAD
ggIPADCCAgoCggIBANI+P5QXm9Bj21FIPsQqbqZRb5XmSZZJYaam7EIJ16Fxedf+
jXAv4d/FVqiEM4BuSNsNMeBMx2Gq0lAfN33h+RMTjRoMb8yBsZsC063MLfXCk4p+
09gtGP7BS6Iy5XdmfY/fPHvA3JDEScdlDDmd6Lsbdwhv93Q8M6POVO9sv4HuS4t/
jEjr+NhE+Bjr/wDbyg7GL71BP1WPZpQnRE4OzoSrt5+bZVLvODWUFwinB0fLaGRk
GmI0r5EUOUd7HpYyoIQbiNlePGfPpHRKnmdXTTEZEoxeWWAaM1VhPGqfrB/Pnca+
vAJX7iBOb3kHinmfVOScsG/YAUR94wSELeY+UlEWJaELVUntrJ5HeRDiTChiVQ++
wnnjNbepaW6shopybUF3XXfhIb4NvwLWpvoKFXVtcVjlOujF0snVvpE+MRT0wacy
tHtjZs7Ao7GYxDz6H8AdBLKJW67uQon37a4MI260ADFMS+2vEAbNSFP+f6ii5mrB
18cY64ZaF6oU8bjGK7BArDx56bRc3WFyuBIGWAFHEuB948BcshXY7baf5jjzPmgz
mq1zdRthQB31MOM2ii6vuTkheAvKfFf+llH4M9SnES4NSF2hj9NnHga9V08wfhYc
x0W6qu+S8HUdVF+V23yTvUNgz4Q+UoGs4sHSDEsIBFqNvInnpUmtNgcR2L5PAgMB
AAGjUzBRMB0GA1UdDgQWBBTPo8kfze4P9EgxNuyk7+xDGFtAYzAfBgNVHSMEGDAW
gBTPo8kfze4P9EgxNuyk7+xDGFtAYzAPBgNVHRMBAf8EBTADAQH/MA0GCSqGSIb3
DQEBCwUAA4ICAQAKHomtmcGqyiLnhziLe97Mq2+Sul5QgYVwfx/KYOXxv2T8ZmcR
Ae9XFhZT4jsAOUDK1OXx9aZgDGJHJLNEVTe9zWv1ONFfNxEBxQgP7hhmDBWdtj6d
taqEW/Jp06X+08BtnYK9NZsvDg2YRcvOHConeMjwvEL7tQK0m+GVyQfLYg6jnrhx
egH+abucTKxabFcWSE+Vk0uJYMqcbXvB4WNKz9vj4V5Hn7/DN4xIjFko+nREw6Oa
/AUFjNnO/FPjap+d68H1LdzMH3PSs+yjGid+6Zx9FCnt9qZydW13Miqg3nDnODXw
+Z682mQFjVlGPCA5ZOQbyMKY4tNazG2n8qy2famQT3+jF8Lb6a4NGbnpeWnLMkIu
jWLWIkA9MlbdNXuajiPNVyYIK9gdoBzbfaKwoOfSsLxEqlf8rio1GGcEV5Hlz5S2
txwI0xdW9MWeGWoiLbZSbRJH4TIBFFtoBG0LoEJi0C+UPwS8CDngJB4TyrZqEld3
rH87W+Et1t/Nepoc/Eoaux9PFp5VPXP+qwQGmhir/hv7OsgBhrkYuhkjxZ8+1uk7
tUWC/XM0mpLoxsq6vVl3AJaJe1ivdA9xLytsuG4iv02Juc593HXYR8yOpow0Eq2T
U5EyeuFg5RXYwAPi7ykw1PW7zAPL4MlonEVz+QXOSx6eyhimp1VZC11SCg==
-----END CERTIFICATE-----
subject=CN = SnakeOil
issuer=CN = SnakeOil
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 2103 bytes and written 373 bytes
Verification error: self-signed certificate
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Server public key is 4096 bit
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 18 (self-signed certificate)
---
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: C4EFDF313C8AC016458C8EFC521F4475BEE6E58DFDCA63BD975042626B476713
    Session-ID-ctx: 
    Resumption PSK: A7509F0A8559D3F2EADA317C78B63B44BDF16DF9E7271E8FB954291C0CAF0F97EA692EB751DE4F88294AC82B50DF6B42
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - 2a 06 c5 62 9a 2e e0 07-e1 99 e9 19 e0 c6 d4 e8   *..b............
    0010 - 4e 35 30 ef bf ec 9b 3a-c9 54 ae 7d 34 a4 33 0f   N50....:.T.}4.3.
    0020 - 3a d0 ea 4b 47 cb e9 87-92 e9 3f 36 af cc 07 48   :..KG.....?6...H
    0030 - 79 d1 87 c2 45 9d 4b 1b-c3 69 a6 cf 97 23 c7 f0   y...E.K..i...#..
    0040 - 40 fa 47 e2 21 21 43 8c-64 a4 90 de cb 76 b0 e7   @.G.!!C.d....v..
    0050 - 83 e0 83 5b 6e cd b8 6c-df 0e e4 90 27 1a 9e a4   ...[n..l....'...
    0060 - cc 4d 0b df b9 83 b3 4f-41 d8 bc 94 12 06 ab 2a   .M.....OA......*
    0070 - 1b 70 bf c6 a0 6c df a4-60 b6 49 42 7e 1a 8c 25   .p...l..`.IB~..%
    0080 - 21 c8 d5 59 e5 07 ca a4-63 3c a0 b2 31 03 1e 59   !..Y....c<..1..Y
    0090 - cd 31 b4 85 42 59 2b e9-35 78 0a 7a 62 29 45 a7   .1..BY+.5x.zb)E.
    00a0 - 01 55 80 c6 24 42 6c f6-9a 5e 11 f5 9d 1c 49 b0   .U..$Bl..^....I.
    00b0 - 66 b6 f4 2c 0a 24 7b 8e-f7 e1 e4 a6 1c 70 02 0a   f..,.${......p..
    00c0 - 2e fe 41 eb 9f d3 67 96-f0 02 09 61 ca cf 30 f8   ..A...g....a..0.
    00d0 - f8 4a 73 82 cf 7c 03 8a-75 ce 3e ab 03 cb 00 d9   .Js..|..u.>.....

    Start Time: 1761790790
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 8793B5DE04AA018A70022B5D61E758773404AF6D5FD227965486F6D04C673724
    Session-ID-ctx: 
    Resumption PSK: EDEA2C214681BCBDAC065B920E9CCFBA8A1A98F5B08BB3984FC8BA244F62F070C68CEE4D16E7E8CF18CF4B0BA5D68FAC
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - 2a 06 c5 62 9a 2e e0 07-e1 99 e9 19 e0 c6 d4 e8   *..b............
    0010 - 74 7d 51 e2 4f 10 0a c4-f1 d3 f4 ce 10 c1 97 56   t}Q.O..........V
    0020 - af ee c9 5b a0 12 9b 6f-5b 50 03 69 94 96 bc 0f   ...[...o[P.i....
    0030 - 05 c2 66 2d 0a a2 89 09-07 7c 42 1d ec 7a 6c 32   ..f-.....|B..zl2
    0040 - 09 31 5f 50 e8 6b b4 16-f8 ed a4 3f c1 e4 87 e4   .1_P.k.....?....
    0050 - d1 13 e4 cb ae 32 48 da-d5 40 ec e6 a2 27 78 3e   .....2H..@...'x>
    0060 - ae e9 7f 31 ab bc c5 8a-1f 31 3f 01 46 08 82 48   ...1.....1?.F..H
    0070 - 7b 40 a0 98 47 54 6f fe-6f 79 a5 09 34 46 ff 99   {@..GTo.oy..4F..
    0080 - cc 74 77 ab bb 6d 6b bb-42 6d 38 f6 f1 ad 81 b2   .tw..mk.Bm8.....
    0090 - c3 c1 00 60 50 79 58 33-f0 0d 54 ed 85 47 34 fe   ...`PyX3..T..G4.
    00a0 - 17 ab f5 bc 1b bd 8d ac-ec f5 2c a3 53 04 3d 17   ..........,.S.=.
    00b0 - cf 43 08 57 14 df d5 3c-eb 0e ef 5b 0d a0 4f e6   .C.W...<...[..O.
    00c0 - fe 38 3d d6 61 c4 a6 f7-97 98 35 e3 11 71 0f c1   .8=.a.....5..q..
    00d0 - a4 6e 54 ca 13 7a 54 dc-0b bb bd e3 c4 91 43 74   .nT..zT.......Ct

    Start Time: 1761790790
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

closed
```


I always like to use `nc` to connect to remote servers but apparently it doesn't support `TLS/SSL`. 


Here's an easy explanation of `TLS/SSL`. 


https://www.reddit.com/r/explainlikeimfive/comments/b0z43c/eli5_what_is_tlsssl/
