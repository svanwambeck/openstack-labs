+++
date = "2015-09-30"
draft = false
weight = 20
title = "FIX"
+++

### Fixes

1. Reset aliceanderson password example  
   `keystone user-password-update aliceanderson --pass fa5tpa55w0rd`


2. How to "unsource" your bash session  
   `source .bashrc`

## A fix to avoid slow yum mirror in anisble lab when a mirror is down and yum slows to a craw or completely fails.

1. In your home directory, make a new directory called "files"

2. S-L-O-W YUM Mirrors
  - Why is YUM updates taking so long!!
  - Here is the mirror status: http://mirror-status.centos.org/
  - Here is yum.conf file info: https://docs.fedoraproject.org/en-US/Fedora/15/html/Deployment_Guide/sec-Configuring_Yum_and_Yum_Repositories.html
  - The default retries before YUM advances to the next mirror is 10 (TEN!!!) retries, let's make that 1:
Copy this text into the files directory and name the file "yum.conf"

<pre>
    [main]
    cachedir=/var/cache/yum/$basearch/$releasever
    keepcache=0
    debuglevel=2
    logfile=/var/log/yum.log
    exactarch=1
    obsoletes=1
    gpgcheck=1
    plugins=1
    installonly_limit=5
    bugtracker_url=http://bugs.centos.org/set_project.php?project_id=23&ref=http://bugs.centos.org/bug_report_page.php?category=yum
    distroverpkg=centos-release
    retries=1
</pre>

3. Modify the sl.yml file to this:

<pre> 
  - hosts: openstack
    remote_user: root
    tasks:
    - copy: src=/home/centos/files/yum.conf dest=/etc/yum.conf owner=root group=root mode=0644
    - name: Install sl
      yum: name=sl state=installed
</pre>

Now run the sl.yml playbook and it should go a lot faster.

