useradd - create a new user or update default new user information
------------------------------------------------------------------
<li>Create a user and verify, the user creation </li>
<pre>
linux-jbz9:~ # useradd john
linux-jbz9:~ # ls /home/
blrk
linux-jbz9:~ # cat /etc/passwd | grep john
john:x:1001:100::/home/john:/bin/bash
</pre>
