---
title: Bitlab Writeup
author: Eno
date: 2019-12-22 11:30am
categories: [hackthebox]
tags: [hackthebox, writeup, bitlab]
math: true
image: /assets/img/htb/Bitlab/bitlab_infocard.PNG
---





first we do the usual nmap scan

![desktop](/assets/img/htb/Bitlab/1_nmap.PNG)

We find that ports 22 and 80 are open. Let's browse to port 80 and see what we find.

![desktop](/assets/img/htb/Bitlab/2_login.PNG)

A GitLab installation! We need a username and password to login though but we don't have one! 


After some browsing through the site we see that we can click on help at the bottom of the page which takes us to 

![desktop](/assets/img/htb/Bitlab/3_help.PNG)

and then when clicking on bookmarks.html to this

![desktop](/assets/img/htb/Bitlab/4_gitlab_login.PNG)


When we hover the mouse on "Gitlab Login" you can notice this piece of code at the bottom of the browser


![desktop](/assets/img/htb/Bitlab/5_auto_login_code.PNG)

![desktop](/assets/img/htb/Bitlab/6_code.PNG)



We need the bits between the [ and ]. It looks a lot like hex but we first need to strip away the \x and now we can put that into a hexdecoder and then we are left with the following.


![desktop](/assets/img/htb/Bitlab/8_decode2.PNG)



You will notice a username and password. clave:d11des0081x




We can now use this to login to GitLab.


![desktop](/assets/img/htb/Bitlab/9_gitlab_page.PNG)



After browsing around for a while I found the following under the snippets tab on top.


![desktop](/assets/img/htb/Bitlab/10_snippet.PNG)

![desktop](/assets/img/htb/Bitlab/11_snippet_postgres.PNG)



Connect details to the Postgres database. We cannot access it directly and only within the machine. We need to try find a way into the machine with a shell.




Being able to upload files to the repository we can try upload a reverse shell with PHP. I created a PHP file with the following code.


![desktop](/assets/img/htb/Bitlab/12_reverse_shell.PNG)



Just remember to use your IP otherwise you will not get a reverse shell back to your machine as I have done on a couple of occasions.


![desktop](/assets/img/htb/Bitlab/13_check_ip.PNG)



In the profile repository, click on the + icon and select upload file and upload your file, in my case it was cake.php.


![desktop](/assets/img/htb/Bitlab/14_upload_reverse.PNG)



Then click Submit merge request and then Merge on the next screens.


![desktop](/assets/img/htb/Bitlab/15_merge_request.PNG)

![desktop](/assets/img/htb/Bitlab/16_merge_final.PNG)



Once that is done, we now have to listen for connections coming into our box with the nc command.


![desktop](/assets/img/htb/Bitlab/18_nc_listen.PNG)



We can now browse to our reverse shell PHP file to initiate the reverse connection by browsing to http://10.10.10.114/profile/cake.php




You should now see a reverse shell on your nc window


![desktop](/assets/img/htb/Bitlab/19_nc_connected.PNG)



We are connected BUT we kinda have a useless terminal which is not interactive meaning you cannot create or edit files easily. We can fix this though with the following steps:


<ol><li>python -c 'import pty; pty.spawn("/bin/bash")'</li><li>ctrl + z (put's the nc into the background)</li><li>echo $TERM (this gets what your term is set as)</li><li>stty -a (this gets your windows size)</li><li>stty raw -echo (NOTE: you will not see any output after this)</li><li>fg (go back to the nc)</li><li>reset (this resets the terminal settings on the remote machine</li><li>In the Terminal type, type in the $TERM output you got, in my case it was xterm-256color. </li></ol>

![desktop](/assets/img/htb/Bitlab/20_terminal_buff.PNG)




then enter the following: 


<ol><li>export SHELL=bash</li><li>stty rows 29 columns 147 (this matches what yours is upbove)</li></ol>






![desktop](/assets/img/htb/Bitlab/21_terminal_buff_2.PNG)




I then created a new file under /tmp/cake


![desktop](/assets/img/htb/Bitlab/22_php_code_postgres.PNG)




and then ran it


![desktop](/assets/img/htb/Bitlab/23_clave_details.PNG)




Oh look, could that be clave's SSH details?


![desktop](/assets/img/htb/Bitlab/24_user_flag.PNG)




yes it was!




Now for root.




Copy RemoteConnection.exe to your machine. I just scp'd it to my machine.




We now have to reverse engineer (debug more like it). I use a tool called OllyDBG.




Once opened we can try run the program but we get a "Access Denied !!"




We have to debug it and see how we can bypass that. Right click on the left and search for all text strings.


![desktop](/assets/img/htb/Bitlab/25_ollydbg_text_strings.PNG)




We actually see the "Access Denied !!" part.


![desktop](/assets/img/htb/Bitlab/26_ollydbg_denied.PNG)




Double click it and you will be take to the portion of the program where it executes. Right click and then select fill with NOPs. This will cause the program to bypass that function.


![desktop](/assets/img/htb/Bitlab/27_NOPS.PNG)




Now run the program again.




Focus on the bottom right window.


![desktop](/assets/img/htb/Bitlab/29_bottom_right.PNG)




Scroll down and you will see the following


![desktop](/assets/img/htb/Bitlab/31_root_password.PNG)




Could that be???


![desktop](/assets/img/htb/Bitlab/30_root_flag.PNG)




Indeed!

