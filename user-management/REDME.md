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

