User Management in SLES 12 / 15
--------------------------------
useradd - create a new user or update default new user information
------------------------------------------------------------------
<li>Create a user and verify, the user creation </li>
<pre>
linux-jbz9:~ # useradd john
linux-jbz9:~ # ls /home/
blrk
linux-jbz9:~ # cat /etc/passwd | grep john
john:x:1001:100::/home/john:/bin/bash
linux-jbz9:~ # cat /etc/group | grep users
users:x:100:
</pre>
<li> Note: loo at the previous output home directory not created for the user, also you understand that the user is added to the default group users this differs in other distro </li>
<li>For example if you create a user in radhat / Centos machine</li>
<pre>
~]# useradd robert
~]# cat /etc/passwd| grep robert 
robert:x:502:502::/home/robert:/bin/bash
</pre>
<li> Note: robert has been assigned a UID of 502, and group ID of User Private Group, equals to UID </li>

Create user with a default home directory 
----------------------------------------------
<pre>
linux-jbz9:~ # useradd -c "Administrator" -m kevin
linux-jbz9:~ # ls /home/
blrk  kevin
linux-jbz9:~ # cat /etc/passwd | grep kevin
kevin:x:1002:100:Administrator:/home/kevin:/bin/bash
</pre>
<li>Note: Look at the above example user's home directory create because of option -m</li>

create a user with home directory in a non default location
-----------------------------------------------------------
<pre>
linux-jbz9:~ # mkdir /admins
linux-jbz9:~ # ls /admins/
linux-jbz9:~ # useradd -d /admins/belvin -c "DB administrator" -m belvin
linux-jbz9:~ # ls /admins/
belvin
linux-jbz9:~ # cat /etc/passwd | grep belvin
belvin:x:1003:100:DB administrator:/admins/belvin:/bin/bash
</pre>

Creating Groups
--------------------
<pre>
linux-jbz9:~ # groupadd webadmin
linux-jbz9:~ # cat /etc/group | grep webadmin
webadmin:x:1001:
</pre>
<li>Create user alternate default group </li>
<pre>
linux-jbz9:~ # useradd -m -d /admins/joe -c "Website admin" -g webadmin joe
linux-jbz9:~ # cat /etc/passwd | grep joe
joe:x:1004:1001:Website admin:/admins/joe:/bin/bash
linux-jbz9:~ # ls /admins/
belvin  joe
</pre>

Modify the existing users
-----------------------------
<li>adding a secondary group to a existing user</li>
<pre>
linux-jbz9:~ # groupadd storageadmin
linux-jbz9:~ # cat /etc/group | grep storage
storageadmin:x:1002:
linux-jbz9:~ # usermod -G storageadmin joe 
linux-jbz9:~ # id joe
uid=1004(joe) gid=1001(webadmin) groups=1002(storageadmin),1001(webadmin)
linux-jbz9:~ # cat /etc/group | grep storage
storageadmin:x:1002:joe
</pre>

setting password for a user
-----------------------------
<li>Note: We have not set password to any of the created users</li>
<li>try to login as user joe</li>
<li>exit from the super user mode using the command exit </li>
<pre>
blrk@linux-jbz9:~> su - joe
Password: 
su: Authentication failure
</pre>

<li>Login as super user su - </li>
<pre>
linux-jbz9:~ # passwd joe
New password: 
BAD PASSWORD: it is too short
BAD PASSWORD: is too simple
Retype new password: 
passwd: password updated successfully
</pre>
<li>Note: setting less secure password gives a warning</li>
<li>exit from the super user mode and login as joe</li>
<pre>
linux-jbz9:~ # exit
logout
blrk@linux-jbz9:~> su - joe
Password: 
joe@linux-jbz9:~> pwd
/admins/joe
joe@linux-jbz9:~> 
</pre>
<li>Note: See the previous output the home directory of the user is the not the default one </li>
<li>login as kevin </li>
<pre>
linux-jbz9:~ # passwd kevin
New password: 
BAD PASSWORD: it is too short
BAD PASSWORD: is too simple
Retype new password: 
passwd: password updated successfully
linux-jbz9:~ # exit
logout
joe@linux-jbz9:~> su - kevin
Password: 
kevin@linux-jbz9:~> pwd
/home/kevin
kevin@linux-jbz9:~> 
</pre>
<li>Note: the home directory of the user kevin is the default </li>

Delete a user
--------------------
<li>delete the user belvin and kevin using different options</li>
<pre>
linux-jbz9:~ # ls /home/
blrk  kevin
linux-jbz9:~ # ls /admins/
belvin  joe
linux-jbz9:~ # userdel belvin 
no crontab for belvin
linux-jbz9:~ # man userdel 
linux-jbz9:~ # userdel -r kevin
userdel: user kevin is currently used by process 2009
linux-jbz9:~ # userdel -r -f  kevin
userdel: user kevin is currently used by process 2009
no crontab for kevin
</pre>




