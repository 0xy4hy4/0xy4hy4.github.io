---
layout: post
title:  RITSEC CTF 2019 CHALLENGES [WRITEUPS]
---
<h3><strong>RITSEC CTF 2019 </strong></h3>

<hr>


<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>CHALLENGE</strong></p>
<p><img src="https://github.com/0xy4hy4/0xy4hy4.github.io/blob/master/_posts/RITSEC_img/Screenshot%20from%202019-11-18%2023-26-48.png?raw=true" alt="" /></p>
<p>&nbsp;</p>
<p>SOLUTION</p>
<p>they given an image by this hint "Artist" i took look at EXIF DATA :</p>
<p><img src="https://github.com/0xy4hy4/0xy4hy4.github.io/blob/master/_posts/RITSEC_img/Screenshot%20from%202019-11-18%2023-37-34.png?raw=true" /></p>
<p>the " user comment " contain base64 , after decryption :</p>
<p>EVGFRP{SBERAFVPF_SNVYF_JBAG_URYC_LBH_URER}</p>
<p>&nbsp;the flag encoded with caesar cipher&nbsp;</p>
<p>, so&nbsp;</p>
<p>FLAG :&nbsp;RITSEC{FORENSICS_FAILS_WONT_HELP_YOU_HERE}</p>
<p>&nbsp;</p>
<hr />
<p>&nbsp;CHALLENGE</p>
<p><img src="https://github.com/0xy4hy4/0xy4hy4.github.io/blob/master/_posts/RITSEC_img/Screenshot%20from%202019-11-18%2023-59-23.png?raw=true" alt="" /></p>
<p>&nbsp;SOLUTION</p>
<p>&nbsp;</p>
<p>the seconde challenge there's two methods to solve it , let's take the easy one</p>
<p>after downloading the pcapc i opened it with wireshark&nbsp; :</p>
<p>&nbsp;</p>
<p><img src="https://github.com/0xy4hy4/0xy4hy4.github.io/blob/master/_posts/RITSEC_img/Screenshot%20from%202019-11-18%2018-32-10.png?raw=true" /></p>
<p>the packet contain 2 base64 encoded i decrypt it&nbsp; , the decryption has a gz archive so let's&nbsp; compile the archive:</p>
<p><a href="https://base64.guru/converter/decode/file">https://base64.guru/converter/decode/file</a></p>
<p>&nbsp;</p>
<p><img src="https://github.com/0xy4hy4/0xy4hy4.github.io/blob/master/_posts/RITSEC_img/Screenshot%20from%202019-11-18%2018-45-09.png?raw=true" alt="" /></p>
<hr />
<p>&nbsp;</p>
<p><img src="https://github.com/0xy4hy4/0xy4hy4.github.io/blob/master/_posts/RITSEC_img/Screenshot%20from%202019-11-18%2018-54-10.png?raw=true" /></p>
<p>file name chromebin by using binwalk tool for extracting the embedded files , given chrome folder and 0.tar file after seeing these i assumed that's google chrome backup , in the description they want us to check the history , so the path is : /Chrome/User Data/Default/history</p>
<p>using some databases reader&nbsp;</p>
<p><img src="https://github.com/0xy4hy4/0xy4hy4.github.io/blob/master/_posts/RITSEC_img/Screenshot%20from%202019-11-18%2019-07-53.png?raw=true" alt="" /></p>
<p>&nbsp;</p>
<p>RITSEC{SP00KY_BR0WS3R_H1ST0RY}</p>
<hr />
<p><img src="https://github.com/0xy4hy4/0xy4hy4.github.io/blob/master/_posts/RITSEC_img/Screenshot%20from%202019-11-18%2019-09-42.png?raw=true" alt="" /></p>
<p>they said "Favorite" so opened Bookmarks file and when i look at names values it's contain familiar words , so using this command&nbsp;</p>
<p>cat Bookmarks | grep 'name"' | cut -d':' -f 2 | tr -d '^ *,"\n\r'</p>
<p>i got</p>
<h2>RITSEC{CHR0M3_BM_FTW}</h2>
<p>&nbsp;</p>
<h2>----------------------------------------------</h2>
<p>&nbsp;</p>
<p>CHALLENGE</p>
<p><img src="https://github.com/0xy4hy4/0xy4hy4.github.io/blob/master/_posts/RITSEC_img/Screenshot%20from%202019-11-18%2021-02-21.png?raw=true" alt="" /></p>
<p>&nbsp;</p>
<p>SOLUTION&nbsp;</p>
<p>they given a large file with multiple base encoded ciphertext : base64/base16/base32 encoded a lot of times , i wrote this script :</p>
<p>```</p>
<p>#!/usr/bin/env</p>
<p>python import sys</p>
<p>import base64</p>
<p>def base64randomde():</p>
<p>flag = open('onionlayerencoding', 'r').read()</p>
<p>while "RITSEC" not in str(flag):</p>
<p>try: flag = base64.b16decode(flag)</p>
<p>except TypeError: try:</p>
<p>flag = base64.b32decode(flag)</p>
<p>except TypeError: try:</p>
<p>flag = base64.b64decode(flag)</p>
<p>except TypeError: break</p>
<p>print(flag)</p>
<p>print(base64randomde())&nbsp;</p>
<p>```</p>
<p>&nbsp;flag : RITSEC{0n1On_L4y3R}</p>
<hr />
<p>&nbsp;</p>
<p>CHALLENGE</p>
<p><img src="https://github.com/0xy4hy4/0xy4hy4.github.io/blob/master/_posts/RITSEC_img/Screenshot%20from%202019-11-19%2000-18-34.png?raw=true" /></p>
<p>&nbsp;</p>
<p>SOLUTION</p>
<p>&nbsp;</p>
<p>by&nbsp;just removing &lt;region&gt;&nbsp; part :</p>
<p>http://bucketsoffun-ctf.s3.amazonaws.com/</p>
<p>i got error page contained "youfoundme-asd897kjm.txt"</p>
<p>FLAG : RITSEC{LIST_HIDDEN_FILES}</p>
<hr />
<p>i wanted to complete the CTF but i was busy and my team also</p>
<p>#0v3n_Sh3ll ❤</p>
