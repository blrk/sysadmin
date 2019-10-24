Managing Packages using RPM
-----------------------------------
<li>List all the repositary</li>
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
16 | vlc-new                             | vlc-new                                | Yes     | (r ) Yes  | Yes 
</pre>


