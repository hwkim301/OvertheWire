## Level12-> Level13


```bash
ssh -p 2220 bandit12@bandit.labs.overthewire.org
```


We have a text file. 


```bash
file data.txt 
data.txt: ASCII text
```


Here's the content of the file. 


```
cat data.txt 
00000000: 1f8b 0808 2817 ee68 0203 6461 7461 322e  ....(..h..data2.
00000010: 6269 6e00 013c 02c3 fd42 5a68 3931 4159  bin..<...BZh91AY
00000020: 2653 59cc 46b5 2d00 0018 ffff da5f e6e3  &SY.F.-......_..
00000030: 9fcd f59d bc69 ddd7 f7ff a7e7 dbdd b59f  .....i..........
00000040: fff7 cfdd ffbf bbdf ffff ff5e b001 3b58  ...........^..;X
00000050: 2406 8000 00d0 6834 6234 d000 6869 9000  $.....h4b4..hi..
00000060: 1a7a 8003 40d0 01a1 a006 8188 340d 1a68  .z..@.......4..h
00000070: d340 d189 e906 8f41 0346 4d94 40d1 91a0  .@.....A.FM.@...
00000080: 681a 0681 a068 0680 c400 3207 a269 a189  h....h....2..i..
00000090: a326 8000 c800 c81a 1883 1000 00d0 c023  .&.............#
000000a0: 4311 a034 30ca 6800 0680 0681 a680 6868  C..40.h.......hh
000000b0: d068 6868 c04c d400 0003 4d06 87a8 d000  .hhh.L....M.....
000000c0: 3086 8c20 3268 068d 000c 9a64 0698 8d04  0.. 2h.....d....
000000d0: 0600 6860 3541 2c85 c8e1 7bc9 479e e369  ..h`5A,...{.G..i
000000e0: 30a1 0250 82e9 64ef 9d40 312f 4bc8 b00f  0..P..d..@1/K...
000000f0: 0c8f 026c d5ca 1008 d7aa 336a ed8f bb7b  ...l......3j...{
00000100: b43f d544 1658 824e a4af 9ce5 612e 8a27  .?.D.X.N....a..'
00000110: c303 0512 cbff dccd f42d 6866 ceec 8127  .........-hf...'
00000120: 5475 ed39 100b f897 7828 46e2 fdf3 efa7  Tu.9....x(F.....
00000130: 43b0 1701 a114 397a 1d81 8d1f 1f23 2ada  C.....9z.....#*.
00000140: 9b18 ee4d d05d 4ae3 d032 e494 ae98 27b0  ...M.]J..2....'.
00000150: 30a0 533c 6696 60ad c546 70c4 322b 7174  0.S<f.`..Fp.2+qt
00000160: 8bb1 52c6 ed0a 267b 7165 208b 77fe 1294  ..R...&{qe .w...
00000170: 2280 3311 354f c68e e004 93e3 abf4 5a0a  ".3.5O........Z.
00000180: a568 c894 27c2 9015 49bb 0147 c253 8e73  .h..'...I..G.S.s
00000190: 2fdd 90e1 6871 c692 1d67 5ebc a5f9 b8a1  /...hq...g^.....
000001a0: 3913 f073 1919 b628 9ae2 c1bf 15ee 493a  9..s...(......I:
000001b0: e375 4d23 71e0 4934 c7a2 15ff 985c a0ba  .uM#q.I4.....\..
000001c0: 9e65 d613 313d 7cef 512a 32bf 835e 50d6  .e..1=|.Q*2..^P.
000001d0: a54f 57ba bceb 6944 03c8 8a50 3542 9140  .OW...iD...P5B.@
000001e0: eb51 0f4c 8a23 9401 0246 0457 d1c0 c33e  .Q.L.#...F.W...>
000001f0: c328 2de7 3d1d 64be 4190 36b0 b803 4f80  .(-.=.d.A.6...O.
00000200: 40bc 3960 ac5e 13a9 3a77 0162 d662 7659  @.9`.^..:w.b.bvY
00000210: fdfd 9535 1188 8588 e8e5 a78d 9b24 c066  ...5.........$.f
00000220: 91c6 4212 fac6 4ed8 ce48 161f cc44 215f  ..B...N..H...D!_
00000230: 330c 5ed7 2709 e578 6efd 3775 c703 8aa1  3.^.'..xn.7u....
00000240: 10b6 2c5d 16bf f352 c7ff c5dc 914e 1424  ..,]...R.....N.$
00000250: 3311 ad4b 40d0 18b2 373c 0200 00         3..K@...7<...
```


I first thought it was a `bzip` file because the file header contains `bzip` file's signature (BZh91AY), but it wasn't.


Since we don't have permission to write or execute the file we need to make a temporary directory where we can. 


```bash
mktemp -d 
/tmp/tmp.cqLdafZpA8
```


`cd` into the directory we just made and copy `data.txt`. 


```bash
cd /tmp/tmp.cqLdafZpA8
cp ~/data.txt .
```


If you Google the first `8` characters of `data.txt`(1f8b 0808), it tells us that it's the `gzip` file header. 


So we're dealing with a `gzip` file, but we simply can't just change the file name from `data.txt` to `data.gz` because the contents of a `gzip` file needs to be binary and right now `data.txt` is just ASCII text. 


In order to change the content from ASCII text to binary we can use the `xxd` command. 


Here's the man page of `xxd -r`.   


```
-r | -revert
Reverse operation: convert (or patch) hex dump into binary.  If not writing to stdout, xxd writes into its output file without truncating it. Use the combina‐
tion  -r  -p to read plain hexadecimal dumps without line number information and without a particular column layout. Additional whitespace and line breaks are
allowed anywhere. Use the combination -r -b to read a bits dump instead of a hex dump.
```


```bash
xxd -r data.txt data
```


Now we've changed the format from ASCII text to binary and correctly saved it in a `gzip` file. 


```bash 
file data
data: gzip compressed data, was "data2.bin", last modified: Tue Oct 14 09:26:00 2025, max compression, from Unix, original size modulo 2^32 572
```


If you change the extension of the file to `.gz(gzip)` the name of the file will become red, which means your Linux system knows that the file is a `gzip` file.



```bash
mv data data.gz
```


You can deflate the file using the `-d` from the `gzip` command. 


```bash 
gzip -d data.gz
```


Here's the man page for `-d`. 


```
-d --decompress --uncompress
    Decompress.
```


Now it's a `bzip` file. 


```bash
file data
data: bzip2 compressed data, block size = 900k
```


Let's change the file extension to a `bzip` file(.bz2). 


Again the color of the file name will be red, if your computer recognizes the bzip file. 


```bash
mv data data.bz2
```


You can decompress the flag with the `-d` flag, below is the man page. 


```bash
 -d --decompress
              Force  decompression.   bzip2,  bunzip2  and bzcat are really the same program, and the decision about what actions to take is done on the basis of which name is used.  This flag overrides that
              mechanism, and forces bzip2 to decompress.
```


You can also use `gunzip` to deflate gzip files and `bunzip` for bzip files but I always use the `-d` option instead because a lot of other commands use it to decode or deflate stuff as well for example `base64`, etc... 


```bash
bzip2 -d data.bz2
```


Now we can repeat the process above, since it's another `gzip` file. 


```bash
file data
data: gzip compressed data, was "data4.bin", last modified: Tue Oct 14 09:26:00 2025, max compression, from Unix, original size modulo 2^32 20480
```


After unzipping the `gzip` file these you'll get a `tar` archive. 


```bash
file data
data: POSIX tar archive (GNU)
```


Read the wikiepdia page below to understand what a `tar` archive is 
https://en.wikipedia.org/wiki/Tar_(computing). 



The `tar` archive uses the `.tar` extension. 


```bash
mv data data.tar
```


If you run `ls` on the `data.tar` file you can see the file name has changed red again. 


To extract `tar` files I always use `-xvf`. 


```bash
tar -xvf data.tar
```


Here's the man page for each tack used in the `tar`. 


```
 -x, --extract, --get
  Extract files from an archive.  Arguments are optional.  When given, they specify names of the archive members to be extracted.

 -v, --verbose
  Verbosely list files processed.  Each instance of this option on the command line increases the verbosity level by one.  The maximum verbosity level is 3.  For a detailed discussion of how var‐
  ious verbosity levels affect tar's output, please refer to GNU Tar Manual, subsection 2.5.2 "The '--verbose' Option".

 -f, --file=ARCHIVE
  Use archive file or device ARCHIVE.  If this option is not given, tar will first examine the environment variable `TAPE'.  If it is set, its value will be used as the archive name.   Otherwise,
  tar will assume the compiled-in default.  The default value can be inspected either using the --show-defaults option, or at the end of the tar --help output.
```


For your information you pretty much always have to use the `-f` option. 


```bash
file data5.bin 
data5.bin: POSIX tar archive (GNU)
```


Now we can repeat, after doing the same stuff over and over again you get the password. 


```bash
cat data8
The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```