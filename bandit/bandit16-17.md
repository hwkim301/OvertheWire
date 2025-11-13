## Level16-> Level17


```bash
ssh -p 2220 bandit16@bandit.labs.overthewire.org
```

It's almost the same as level16 but the only difference is that it accepts only one port from `31000~32000` accepts the password. 


To find out which port number to use we will use **[nmap]**(https://en.wikipedia.org/wiki/Nmap) Network Mapper. 


Here's the man page for `nmap` and the `-p` tack. 


```DESCRIPTION
       Nmap (“Network Mapper”) is an open source tool for network exploration and security auditing. It was designed to rapidly scan large networks, although it works fine against single hosts. Nmap uses raw
       IP packets in novel ways to determine what hosts are available on the network, what services (application name and version) those hosts are offering, what operating systems (and OS versions) they are
       running, what type of packet filters/firewalls are in use, and dozens of other characteristics. While Nmap is commonly used for security audits, many systems and network administrators find it useful
       for routine tasks such as network inventory, managing service upgrade schedules, and monitoring host or service uptime.

       The output from Nmap is a list of scanned targets, with supplemental information on each depending on the options used. Key among that information is the “interesting ports table”.  That table lists
       the port number and protocol, service name, and state. The state is either open, filtered, closed, or unfiltered.  Open means that an application on the target machine is listening for
       connections/packets on that port.  Filtered means that a firewall, filter, or other network obstacle is blocking the port so that Nmap cannot tell whether it is open or closed.  Closed ports have no
       application listening on them, though they could open up at any time. Ports are classified as unfiltered when they are responsive to Nmap's probes, but Nmap cannot determine whether they are open or
       closed. Nmap reports the state combinations open|filtered and closed|filtered when it cannot determine which of the two states describe a port. The port table may also include software version details
       when version detection has been requested. When an IP protocol scan is requested (-sO), Nmap provides information on supported IP protocols rather than listening ports.

       In addition to the interesting ports table, Nmap can provide further information on targets, including reverse DNS names, operating system guesses, device types, and MAC addresses.

       A typical Nmap scan is shown in Example 1. The only Nmap arguments used in this example are -A, to enable OS and version detection, script scanning, and traceroute; -T4 for faster execution; and then
       the hostname.

-p <port ranges>: Only scan specified ports
```


```
nmap -p 31000-32000 localhost
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-10-30 02:30 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00017s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 0.11 seconds
```


If you try port by port the only port that speaks `SSL/TLS` is `31790`.


When trying to connect to `localhost` via port `31790` you'll get a `KEYUPDATE` alert and fail.


```
openssl s_client -connect localhost:31790
...
read R BLOCK
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
KEYUPDATE

Wrong! Please enter the correct current password.
closed
```


However by adding the `-ign_eof` flag at the end of the ssl command fixes the job.


```bash 
openssl s_client -connect localhost:31790 -ign_eof
...
read R BLOCK
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
Correct!
```


Unlike the previous levels you won't get a password instead you get an RSA Key.


Copy your RSA key, save it on your local computer and change the permissions like we did before.