# User

scan

nmap -sS -T4 -A 10.10.10.222

22/tcp open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)

80/tcp open  http    nginx 1.14.2


#open the web page

#add ip to the hosts file

nano /etc/hosts


#first I tried to signup and add email

#then I realized that the machine wasn't on the internet

#open new ticket

#if you have any error then change the email address beacuse someone else used it

#save the ticket id and the email we will use those

ticket id: 4701529

4701529@delivery.htb


#now we go to Check Ticket Status

#type the email and tickt id

#now,we go to Mattermost server and create an account with the ticket number email then refresh the ticket

#if the server didn't open add the server ip o the hosts

#You have to use ticket number email it gives you when you create the ticket

8113433@delivery.htb.

now what happened that you taked the email that was supposed to be the support email and creat the Mattermost server with it

# the verfing email goes to the ticket view page

#It’s kind of a hack, instead of going to an email it went to the ticket page instead

That should have went to an email address, not the details of the ticket

So you just tricked the application into creating an account when before it wouldn’t let you

#copy/paste that huge link


#the root saied

@developers Please update theme to the OSTicket before we go live.  Credentials to the server are maildeliverer:Youve_G0t_Mail!

Also please create a program to help us stop re-using the same passwords everywhere.... Especially those that are a variant of "PleaseSubscribe!"

#now we have the credintials to access the server

username:maildeliverer

password:Youve_G0t_Mail!

#using ssh to enter

Bingo now you own the user
