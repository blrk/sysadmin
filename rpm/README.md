Managing repositary using Zypper
-------------------------------------------
<div align=right>
<a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/sec-managing_yum_repositories">Manage repositary using yum </a>
</div
-----------------------------------
<li>List all the repository </li>
<pre>
 rk-lpc:~ # zypper lr 
Repository priorities in effect:                                                                       (See 'zypper lr -P' for details)
      90 (raised priority)  :  1 repository  
      99 (default priority) :  9 repositories
#  | Alias                               | Name                                   | Enabled | GPG Check | Refresh
---+-------------------------------------+----------------------------------------+---------+-----------+--------
 1 | google-chrome                       | google-chrome                          | Yes     | (r ) Yes  | Yes    
 2 | http-download.opensuse.org-7af3c51b | openSUSE.org:openSUSE:Leap:15.0:Update | Yes     | (r ) Yes  | Yes    
 3 | http-download.videolan.org-c90ca15a | SuSE                                   | Yes     | (r ) Yes  | Yes    
 4 | openSUSE-Leap-15.1-1                | openSUSE-Leap-15.1-1                   | Yes     | (r ) Yes  | No     
 5 | packman-manual                      | packman-manual                         | Yes     | (r ) Yes  | Yes    
 6 | repo-debug                          | Debug Repository                       | No      | ----      | ----   
 7 | repo-debug-non-oss                  | Debug Repository (Non-OSS)             | No      | ----      | ----   
 8 | repo-debug-update                   | Update Repository (Debug)              | No      | ----      | ----   
 9 | repo-debug-update-non-oss           | Update Repository (Debug, Non-OSS)     | No      | ----      | ----   
10 | repo-non-oss                        | Non-OSS Repository                     | Yes     | (r ) Yes  | Yes    
11 | repo-oss                            | Main Repository                        | Yes     | (r ) Yes  | Yes    
12 | repo-source                         | Source Repository                      | No      | ----      | ----   
13 | repo-source-non-oss                 | Source Repository (Non-OSS)            | No      | ----      | ----   
14 | repo-update                         | Main Update Repository                 | Yes     | (r ) Yes  | Yes    
15 | repo-update-non-oss                 | Update Repository (Non-Oss)            | Yes     | (r ) Yes  | Yes    
</pre>

<li> adding a repository  </li>
<pre>
rk-lpc:~ # zypper ar https://download.videolan.org/pub/vlc/SuSE/Leap_15.2/ vlc
Adding repository 'vlc' .........................................................................................................[done]
Repository 'vlc' successfully added

URI         : https://download.videolan.org/pub/vlc/SuSE/Leap_15.2/
Enabled     : Yes                                                  
GPG Check   : Yes                                                  
Autorefresh : No                                                   
Priority    : 99 (default priority)                                

Repository priorities in effect:                                                                       (See 'zypper lr -P' for details)
      90 (raised priority)  :  1 repository  
      99 (default priority) : 10 repositories
</pre>

<li>List the repositary after addinf a repo</li>
<pre>
rk-lpc:~ # zypper lr 
Repository priorities in effect:                                                                       (See 'zypper lr -P' for details)
      90 (raised priority)  :  1 repository  
      99 (default priority) : 10 repositories
#  | Alias                               | Name                                   | Enabled | GPG Check | Refresh
---+-------------------------------------+----------------------------------------+---------+-----------+--------
 1 | google-chrome                       | google-chrome                          | Yes     | (r ) Yes  | Yes    
 2 | http-download.opensuse.org-7af3c51b | openSUSE.org:openSUSE:Leap:15.0:Update | Yes     | (r ) Yes  | Yes    
 3 | http-download.videolan.org-c90ca15a | SuSE                                   | Yes     | (r ) Yes  | Yes    
 4 | openSUSE-Leap-15.1-1                | openSUSE-Leap-15.1-1                   | Yes     | (r ) Yes  | No     
 5 | packman-manual                      | packman-manual                         | Yes     | (r ) Yes  | Yes    
 6 | repo-debug                          | Debug Repository                       | No      | ----      | ----   
 7 | repo-debug-non-oss                  | Debug Repository (Non-OSS)             | No      | ----      | ----   
 8 | repo-debug-update                   | Update Repository (Debug)              | No      | ----      | ----   
 9 | repo-debug-update-non-oss           | Update Repository (Debug, Non-OSS)     | No      | ----      | ----   
10 | repo-non-oss                        | Non-OSS Repository                     | Yes     | (r ) Yes  | Yes    
11 | repo-oss                            | Main Repository                        | Yes     | (r ) Yes  | Yes    
12 | repo-source                         | Source Repository                      | No      | ----      | ----   
13 | repo-source-non-oss                 | Source Repository (Non-OSS)            | No      | ----      | ----   
14 | repo-update                         | Main Update Repository                 | Yes     | (r ) Yes  | Yes    
15 | repo-update-non-oss                 | Update Repository (Non-Oss)            | Yes     | (r ) Yes  | Yes    
16 | vlc                                 | vlc                                    | Yes     | ( p) Yes  | No   
</pre>
 
<li>Remove a repository </li>
<pre>
rk-lpc:~ # zypper rr vlc
Removing repository 'vlc' .......................................................................................................[done]
Repository 'vlc' has been removed.
</pre>

Manage packages using RPM
--------------------------------

<li>Downalod a rpm file</li>
<pre>
rk-lpc:~ # wget -P /tmp/ https://rpmfind.net/linux/fedora/linux/development/rawhide/Everything/x86_64/os/Packages/l/lynx-2.8.9-6.fc31.x86_64.rpm
--2019-10-24 11:47:38--  https://rpmfind.net/linux/fedora/linux/development/rawhide/Everything/x86_64/os/Packages/l/lynx-2.8.9-6.fc31.x86_64.rpm
Resolving rpmfind.net (rpmfind.net)... 195.220.108.108
Connecting to rpmfind.net (rpmfind.net)|195.220.108.108|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1651752 (1.6M) [application/x-rpm]
Saving to: ‘/tmp/lynx-2.8.9-6.fc31.x86_64.rpm’

lynx-2.8.9-6.fc31.x86_64.rpm      100%[============================================================>]   1.58M   492KB/s    in 3.3s    

2019-10-24 11:47:42 (492 KB/s) - ‘/tmp/lynx-2.8.9-6.fc31.x86_64.rpm’ saved [1651752/1651752]

rk-lpc:~ # ls /tmp/
lynx-2.8.9-6.fc31.x86_64.rpm
</pre>

<li>Find out information on a package</li>
<pre>
rk-lpc:~ # rpm -qf wget
error: file /root/wget: No such file or directory
rk-lpc:~ # rpm -qf /usr/bin/wget 
wget-1.19.5-lp151.4.1.x86_64
</pre>

<li>Find out information about an installed package</li>
<pre>
rk-lpc:~ # rpm -qi wget
Name        : wget
Version     : 1.19.5
Release     : lp151.4.1
Architecture: x86_64
Install Date: Mon Oct  7 12:35:51 2019
Group       : Productivity/Networking/Web/Utilities
Size        : 2881903
License     : GPL-3.0+
Signature   : RSA/SHA256, Thu Apr 11 14:53:42 2019, Key ID b88b2fd43dbdc284
Source RPM  : wget-1.19.5-lp151.4.1.src.rpm
Build Date  : Thu Apr 11 14:53:27 2019
Build Host  : cloud114
Relocations : (not relocatable)
Packager    : https://bugs.opensuse.org
Vendor      : openSUSE
URL         : https://www.gnu.org/software/wget/
Summary     : A Tool for Mirroring FTP and HTTP Servers
Description :
Wget enables you to retrieve WWW documents or FTP files from a server.
This can be done in script files or via the command line.
Distribution: openSUSE Leap 15.1

rk-lpc:~ # rpm -qi lynx
package lynx is not installed
</pre>

<li>show all the files installed by the wget package</li>
<pre>
rk-lpc:~ # rpm -ql wget
/etc/wgetrc
/usr/bin/wget
/usr/share/doc/packages/wget
/usr/share/doc/packages/wget/AUTHORS
/usr/share/doc/packages/wget/COPYING
/usr/share/doc/packages/wget/MAILING-LIST
/usr/share/doc/packages/wget/NEWS
/usr/share/doc/packages/wget/README
/usr/share/doc/packages/wget/rmold.pl
/usr/share/doc/packages/wget/sample.wgetrc
/usr/share/info/wget.info.gz
/usr/share/locale/be/LC_MESSAGES/wget.mo
/usr/share/locale/bg/LC_MESSAGES/wget.mo
/usr/share/locale/ca/LC_MESSAGES/wget.mo
/usr/share/locale/cs/LC_MESSAGES/wget.mo
/usr/share/locale/da/LC_MESSAGES/wget.mo
/usr/share/locale/de/LC_MESSAGES/wget.mo
/usr/share/locale/el/LC_MESSAGES/wget.mo
/usr/share/locale/en_GB/LC_MESSAGES/wget.mo
/usr/share/locale/eo/LC_MESSAGES/wget.mo
/usr/share/locale/es/LC_MESSAGES/wget.mo
/usr/share/locale/et/LC_MESSAGES/wget.mo
/usr/share/locale/eu/LC_MESSAGES/wget.mo
/usr/share/locale/fi/LC_MESSAGES/wget.mo
/usr/share/locale/fr/LC_MESSAGES/wget.mo
/usr/share/locale/ga/LC_MESSAGES/wget.mo
/usr/share/locale/gl/LC_MESSAGES/wget.mo
/usr/share/locale/he/LC_MESSAGES/wget.mo
/usr/share/locale/hr/LC_MESSAGES/wget.mo
/usr/share/locale/hu/LC_MESSAGES/wget.mo
/usr/share/locale/id/LC_MESSAGES/wget.mo
/usr/share/locale/it/LC_MESSAGES/wget.mo
/usr/share/locale/ja/LC_MESSAGES/wget.mo
/usr/share/locale/lt/LC_MESSAGES/wget.mo
/usr/share/locale/nb/LC_MESSAGES/wget.mo
/usr/share/locale/nl/LC_MESSAGES/wget.mo
/usr/share/locale/pl/LC_MESSAGES/wget.mo
/usr/share/locale/pt/LC_MESSAGES/wget.mo
/usr/share/locale/pt_BR/LC_MESSAGES/wget.mo
/usr/share/locale/ro/LC_MESSAGES/wget.mo
/usr/share/locale/ru/LC_MESSAGES/wget.mo
/usr/share/locale/sk/LC_MESSAGES/wget.mo
/usr/share/locale/sl/LC_MESSAGES/wget.mo
/usr/share/locale/sr/LC_MESSAGES/wget.mo
/usr/share/locale/sv/LC_MESSAGES/wget.mo
/usr/share/locale/tr/LC_MESSAGES/wget.mo
/usr/share/locale/uk/LC_MESSAGES/wget.mo
/usr/share/locale/vi/LC_MESSAGES/wget.mo
/usr/share/locale/zh_CN/LC_MESSAGES/wget.mo
/usr/share/locale/zh_TW/LC_MESSAGES/wget.mo
/usr/share/man/man1/wget.1.gz

rk-lpc:~ # rpm -ql lynx
package lynx is not installed
</pre>

<li>To see what has changed in the files on your hard drive since the wget RPM was originally installed </li>
<pre>
rk-lpc:~ # rpm -V wget
rk-lpc:~ # 
#no output if no files were changed

rk-lpc:~ # vi /etc/wgetrc 

Note: press i then enter the text in quote "#this is rpm test" and save by entering Esc wq. Then run the previous command

rk-lpc:~ # rpm -V wget
S.5....T.  c /etc/wgetrc

</pre>

<li>View the documnetation files of wget</li>
<pre>
rk-lpc:~ # rpm -qd wget
/usr/share/doc/packages/wget/AUTHORS
/usr/share/doc/packages/wget/COPYING
/usr/share/doc/packages/wget/MAILING-LIST
/usr/share/doc/packages/wget/NEWS
/usr/share/doc/packages/wget/README
/usr/share/doc/packages/wget/rmold.pl
/usr/share/doc/packages/wget/sample.wgetrc
/usr/share/info/wget.info.gz
/usr/share/man/man1/wget.1.gz
</pre>

<li>query all the installed packages</li>
<pre>
rk-lpc:~ # rpm -qa | less
diffutils-lang-3.6-lp151.3.3.noarch
intlfonts-arabic-bitmap-fonts-1.2.1-lp151.2.1.noarch
libopenjpeg1-32bit-1.5.2-lp151.3.3.x86_64
libmwaw-0_3-3-0.3.14-lp151.1.3.x86_64
brasero-nautilus-3.12.2+20171213.567326a7-lp151.3.5.x86_64
libX11-xcb1-1.6.5-lp151.3.3.x86_64
sysvinit-tools-2.88+-lp151.2.3.x86_64
</pre>

<li>Install an rpm file</li>
<pre>
rk-lpc:~ # rpm -i /tmp/lynx-2.8.9-6.fc31.x86_64.rpm 
</pre>

<li>Uninstall an rpm file</li>
<pre>
rk-lpc:~ # rpm -e lynx
</pre>

<li>upgrades or installs the package currently installed to a newer version</li>

<pre>
rk-lpc:~ # rpm -U lynx-2.8.9-6.fc31.x86_64.rpm 
</pre>
 
