---
title: Resolute Writeup
author: Eno
date: 2019-12-24 11:30am
categories: [hackthebox]
tags: [hackthebox, writeup, resolute]
math: true
image: /assets/img/htb/Resolute/resolute_infocard.PNG
---
let's start with a nmap

![desktop](/assets/img/htb/Resolute/1_nmap.PNG)

No port 80 or 443. This is going to be interesting. It looks like it has samba and LDAP running.

Let us run a tool called enum4linux and see if we can get any information out.

![desktop](/assets/img/htb/Resolute/2_enum4linux_1.PNG)

We get the domain and also a bunch of domain users

![desktop](/assets/img/htb/Resolute/3_enum4linux_2_domain.PNG)

![desktop](/assets/img/htb/Resolute/4_enum4linux_3_users.PNG)

What do we have here?

![desktop](/assets/img/htb/Resolute/5_enum4linux_3_user_pass.PNG)

Looks like a username and password. 

Let's use a tool called "evil-winrm" to login

![desktop](/assets/img/htb/Resolute/6_evilwinrm_marko.PNG)

No luck. What if the administrator used that password to create the rest of the users and we have a user who has not changed their password?

After going through all the users we actually found one! Naughty Melanie.

![desktop](/assets/img/htb/Resolute/7_evilwinrm_melanie.PNG)

After I log in to a user my first instinct, on a windows machine, is to check the user's desktop directory first to see if there is any flag or note. This time it seems like this user was the intended user! 

![desktop](/assets/img/htb/Resolute/8_userflag.PNG)

User flag done!

Now to get root flag.

Usually one also looks at what other users are on the box so you can get an idea of if you can get a privilege escalation out of them.

![desktop](/assets/img/htb/Resolute/9_list_of_users.PNG)

We find another user called ryan but we don't have a password or access to that user's home directory.

Let's enumerate some more. 

After enumerating quite a bit I finally found the following. To look for hidden directories on windows, you simpy just use dir -force. 

![desktop](/assets/img/htb/Resolute/10_hidden_file.PNG)

I am not gonna post the whole file here because it's a bit big but I will show you the juicy info.

![desktop](/assets/img/htb/Resolute/11_powershell_script.PNG)

![desktop](/assets/img/htb/Resolute/12_ryan_password.PNG)

Could this be ryan's password? Let's see. I use Evil-WinRM once again.

![desktop](/assets/img/htb/Resolute/13_ryan_logged_in.PNG)

Success! But it's not the Administrator. Let's browse around his user space and see what we can find.

![desktop](/assets/img/htb/Resolute/14_ryan_note.PNG)

A note. Drats. This could prove to be interesting as any changes we make to the system will be reverted in a minute.

Let's see what groups ryan is in. Maybe we can leverage off a group?

![desktop](/assets/img/htb/Resolute/15_ryan_groups.PNG)

Seems like ryan is part of the DNSAdmin group. The DNSAdmin is a full privileged administrator of a server. Let's try exploit this!

I got a bit of a nudge and stumbled across the following article:

<a href="https://ired.team/offensive-security-experiments/active-directory-kerberos-abuse/from-dnsadmins-to-system-to-domain-compromise">https://ired.team/offensive-security-experiments/active-directory-kerberos-abuse/from-dnsadmins-to-system-to-domain-compromise</a>

We need to create a reverse shell payload. I tried to create many payloads but the Anti Virus or Windows Defender kept on destroying my payload. Especially .exe files would be thrown off a cliff. I also tried with .DLL files but also to no avail. It was frustrating me.

Eventually someone showed me the one from Mimikatz which was altered a bit and eventually used that one.

Now we need to create a Samba share to be able to get the reverse shell and it seems that anything we copy to the server would just get blocked from running locally.

![desktop](/assets/img/htb/Resolute/16_smb_server.PNG)

First let's start a nc listener

![desktop](/assets/img/htb/Resolute/21_listener.PNG)

Once that is started we can go to the server and run the following

![desktop](/assets/img/htb/Resolute/17_dnscmd.PNG)

This injects the .dll into the regkey. We now have to stop and start the DNS Service to activate it.

![desktop](/assets/img/htb/Resolute/18_dns_service.PNG)

To check to see if it was inserted into the key

![desktop](/assets/img/htb/Resolute/20_check_regkey.PNG)

If this was successful, the following should happen on your nc listener window. I did have some issues doing this multiple of times as I was doing this in the free tier I was fighting with people injecting their payloads. Just keep trying.

![desktop](/assets/img/htb/Resolute/22_nc_connected.PNG)

Connected!

![desktop](/assets/img/htb/Resolute/23_root_flag.PNG)

Root flag achieved!
