---
title: Traverxec Writeup
author: Eno
date: 2019-12-24 18:30am
categories: [hackthebox]
tags: [hackthebox, writeup, traverxec]
math: true
image: /assets/img/htb/Traverxec/traverxec_infocard.PNG
---

<p>Let's do the nmap scan</p>

![desktop](/assets/img/htb/Traverxec/1_nmap.PNG)

<p>Ports 22 and 80 are open.</p>

<p>Browsing to the webpage I found nothing of interest and running GoBuster brought back no results.</p>

<p>Noticing the webserver that is running Nostromo I checked for any exploits.</p>

![desktop](/assets/img/htb/Traverxec/2_nostromo_metasploit.PNG)

<p>Found one, let's see what happens!</p>

![desktop](/assets/img/htb/Traverxec/2_nostromo_metasploit_options.PNG)

![desktop](/assets/img/htb/Traverxec/4_nostromo_metasploit_exploit.PNG)

<p>Reverse shell given!</p>

<p>First thing to do is find the webserver config and see what we can get.</p>

![desktop](/assets/img/htb/Traverxec/5_nostromo_config.PNG)

<p>Browsing htdocs brought nothing useful. Now we check .htpasswd and see.</p>

![desktop](/assets/img/htb/Traverxec/6_nostromo_htpasswd.PNG)

<p>Let's crack it!</p>

![desktop](/assets/img/htb/Traverxec/7_nostromo_htpasswd_crack.PNG)

<p>I used another box of mine that cracks passwords quicker and found the following.</p>

![desktop](/assets/img/htb/Traverxec/8_nostromo_htpasswd_cracked.PNG)

<p>Let us try our luck with ssh login.</p>

![desktop](/assets/img/htb/Traverxec/9_david_ssh_noluck.PNG)

<p>Thought as much.</p>

<p> In the Nostromo config we see that user home directories are setup.</p>

![desktop](/assets/img/htb/Traverxec/10_user_space.PNG)

<p>Drats.</p>

<p>After trying and understanding what the homedir setting does, we managed to get into the user's public_www directory. Nice file permissions.</p>

<p>Wait, what do we have here? He backed up his ssh keys where?</p>

![desktop](/assets/img/htb/Traverxec/11_user_directory.PNG)

<p>Let's browse to the folder on the webpage.</p>

![desktop](/assets/img/htb/Traverxec/12_login_page.PNG)

<p>Use the credentials from above for david.</p>

![desktop](/assets/img/htb/Traverxec/13_ssh_keys.PNG)

<p>Download the file and untar it.</p>

![desktop](/assets/img/htb/Traverxec/14_downloaded_ssh_keys.PNG)

<p>Now we need to convert the private key to push it through John to crack the password.</p>

![desktop](/assets/img/htb/Traverxec/15_sshkey_cracked.PNG)

<p>Password cracked and now we have the user flag!</p>

![desktop](/assets/img/htb/Traverxec/16_user_flag.PNG)>

<p>There is a file in the bin directory which we need to have a look at.</p>

<p>Running this script just outputs a couple of things and doesn't do anything special on output.</p>

![desktop](/assets/img/htb/Traverxec/17_server_stats_script.PNG)

<p> I hit a bit of a wall at this stage and then I saw a clue when someone mentioned GTFOBins - <a href="https://gtfobins.github.io/">https://gtfobins.github.io/</a> </p>

![desktop](/assets/img/htb/Traverxec/18_gtfobins_jounalctl.PNG)

<p>This is where things get weird. Bare with me.</p>

<p>If your terminal is full screen and you run the command then the following happens.</p>

![desktop](/assets/img/htb/Traverxec/19_gtfobins_fullscreen.PNG)

<p>But now if you make your terminal smaller and run the command again, then the following happens</p>

![desktop](/assets/img/htb/Traverxec/19_gtfobins_small.PNG)

<p>When the above screen shows, enter !/bin/bash and you will be given a root prompt, wtf?</p>

![desktop](/assets/img/htb/Traverxec/19_gtfobins_wtf.PNG)

![desktop](/assets/img/htb/Traverxec/20_root_flag.PNG)>

<p>root flag :)</p>
