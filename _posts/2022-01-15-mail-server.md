---
title: Getting to know the Mail Server How it Works and Its Benefits
author: Eno
date: 2022-01-15 00:00:00 +0700
image: /assets/img/blogging/mail_server.png
categories: [Blogging, 0x3n0, Mail Server]
tags: [Mail, Mail User Agent, Mail Transport Agent, Mail Delivery Agent, Mail Server Protocol, Postfix, Qmail, SMTP, POP3, IMAP]
---

With just one click, you can send emails to other people who are far away. However, how does the email actually get to the recipient? The answer is thanks to the role of the mail server.

In this article, you will learn and know more about mail servers. And how it works and its benefits.

![img-description](/assets/img/blogging/mail_server.png)_Mail Server_

## What is a Mail Server?

Mail server is a server in charge of sending and receiving email. Although it looks simple, the actual process of sending an email is quite complex. The email you send goes through a series of complicated processes on the mail server to get to the recipient.

In simple terms, a mail server functions the same as a post office. It saves incoming mail, then sends it to the recipient.

## Mail Server Components
In general, all email servers consist of three components namely MTA, MDA, and MUA. Each component has a specific role in the process of moving and managing email. Let's see what roles each component has.

### MUA (Mail User Agent)

MUA is an application used to compose, send and receive emails. Examples of MUA for example are Yahoo, Gmail, Outlook, and other email services.

Some MUAs can appear more graphical, such as Evolution, Thunderbird, and Outlook, or have a simple text-based interface such as Mutt.

### MTA (Mail Transport Agent)

MTA is one of the components of the mail server in charge of receiving and sending email from one computer to another. MTA plays an important role in internet message handling system. Some of the tasks of the MTA include:

- Receive emails
- Request-mail exchange records and select an email server to transfer emails to.
- Sends an automatic response message, if the message fails to reach its destination.
    
### MDA (Mail Delivery Agent)

MDA is a computer software that is responsible for delivering email from the MTA server. MDA is also known as LDA or Local Delivery Agent. Some MTAs can fill the MDA role when they add a new email message to the on-premises user message file.

## Mail Server Protocol

As for protocols, there are two categories in email servers: outgoing mail protocols (SMTP) and incoming mail protocols (IMAP and POP3).

### SMTP or Simple Mail Transfer Protocol

SMTP is a standard protocol for transmitting or sending email. This protocol is in charge of communicating with the server to send email from local email to the email server.

In the process of working, SMTP is controlled by the MTA on your email server.

### POP3 or Post Office Protocol

POP 3 is the third version of the email receiving method. POP3 receives and stores email for someone until they retrieve it. POP3 is a server/client protocol where email is sent from the server to the local email.

POP3 works by contacting your e-mail server, then downloading all new messages from local e-mails. Once you download them, they will disappear from the server.

So, if you decide to check your email with a different gadget, the messages you downloaded earlier will no longer exist. That's why, it's good to do a back up.

POP3 is suitable for those of you who usually open email with only one gadget.

### IMAP or Internet Message Access.

IMAP allows you to access your email wherever you are, usually via the internet. When you read email using IMAP, you are not actually downloading, or saving it to your computer, but reading it through the server.

For those of you who travel a lot and often use various gadgets to access email, we recommend using an IMAP-based email service.

## Types of Mail Server

There are several types of mail servers that are distinguished based on the operating system and program. Here's the list:

### Sendmail

Are you using a Linux operating system? Well, you must be familiar with the Sendmail mail server type. Already in existence since 1982, Sendmail is a standard Linux mail server type. As a result, Sendmail is the most widely used in the world.

In addition, Sendmail is very easy to set up with decent performance. Unfortunately, in terms of security, Sendmail still needs a lot of improvement compared to other newer types of mail servers.

### Postfix
Postfix is a type of MTA mail server which is an improved version of Sendmail. As a result, Postfix is not limited to the Linux operating system but can also be used on Mac OS X.

Postfix also has a much better level of security than Sendmail because that's what it's all about. In addition, Postfix also has a very high performance. So, Postfix is predicted to replace Sendmail in the future.

### Qmail

Of the three types of mail servers in this article, Qmail is the MTA which is considered the safest mail server today. Why is that?

Because, Qmail does not have a security hole that has a negative effect or damage its overall performance. Therefore, there are several giant email providers that use Qmail such as Yahoo and Hotmail.

## How Mail Server Works

Basically, the main way the mail server works is sending email (sending email) and receiving email (receiving email) which will go through five stages to find out how the mail server actually works in sending and receiving messages. Below we outline each stage of the process:

### Stage 1: Sending a Message

After composing the message and clicking the send button, MUA will send the email. Then, the recipient/client email will connect to your domain's SMTP server. This server can be named anything, for example smtp.eg.com.

### Stage 2: Recipient Email Communicating with SMTP Server

The recipient/client email communicates with the MTA server using SMTP. Then provide it your email address, recipient email address, message body, and attachments.

### Stage 3: SMTP Server Processing Recipient's Email Address

After communicating with the recipient's email, the MDA component via SMTP will process the recipient's email address (specifically its domain). If the domain name is the same as the message sender, the message will be routed directly to the POP3 or IMAP domain server.

However, if the domains are different, the SMTP server will communicate with the domain server first.

### Stage 4: Sending SMTP Server Communicating with DNS

In order to find the receiving server, the MTA via SMTP must communicate with DNS. Or, Domain Name Servers. Later DNS will take the recipient's email domain name, then translate it into an IP address.

Why does it have to be an IP address? Because the sender's SMTP server can't properly channel mail with just a domain name. So, it takes an IP address, which is an identity number for each computer connected to the internet.

By knowing the IP address information, the mail server can work more efficiently.

### Stage 5: Email Connected with SMTP Server

After the SMTP server has the recipient's IP address, the email forwarded by the MDA/MTA can be connected to the SMTP server. This process does not just happen. Because, actually the message sent earlier must go through a series of SMTP processes, until it finally arrives at its destination.

### Stage 6: Recipient SMTP Server Scans Incoming Messages

At this stage the MUA scans for incoming messages. If it recognizes the domain and username, the message is forwarded to the domain's POP3 or IMAP server. From there, the message will be placed in the sendmail queue. The message will be in the sendmail queue until the recipient's email allows it to be downloaded.

## What are the advantages of having your own mail server?

Basically, the mail servers in free and paid email services have the same process and way of working. The biggest difference lies in the freedom of setting, security, and the amount of disk space you get.

Here are some of the benefits of a dedicated mail server for paid email services:

- Gaining Trust from Customers

By using paid email, you are not only using a dedicated mail server, but also your own domain. Of course, it can show the professionalism of your company. So, that later the trust of your customers continues to increase.

- Create a Business Email for All Team Members

Paid email allows you to have your own mail server with more disk space than free email. This means that you and your team will find it easier to transfer data and communicate with clients.

- Have a Safe Email from Viruses and Malware

By having your own mail server, later you will have additional security features. So, you will avoid attacks by viruses, malware, spam, and so on.

- Improve the Quality of Data Privacy

Having your own mail server keeps your company's important data protected. Don't worry that your email data will be used by other parties to place advertisements in your inbox.

## Want to Have Your Own Mail Server?

That's a complete explanation of the mail server. The mail server is one of the important things to be able to make the business communication process through email run well.

To increase business, a paid email subscription with a dedicated mail server is the best recommendation. Because, you can enjoy the various benefits and advantages above.
