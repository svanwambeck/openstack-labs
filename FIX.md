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

#### A fix to avoid slow yum mirror in anisble lab when a mirror is down and yum slows to a craw or completely fails.

1. In your home directory, make a new directory called "files"

2. Copy this text into the files directory and name the file "yum.conf"

    ```
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

    #  This is the default, if you make this bigger yum won't see if the metadata
    # is newer on the remote and so you'll "gain" the bandwidth of not having to
    # download the new metadata and "pay" for it by yum not having correct
    # information.
    #  It is esp. important, to have correct metadata, for distributions like
    # Fedora which don't keep old packages around. If you don't like this checking
    # interupting your command line usage, it's much better to have something
    # manually check the metadata once an hour (yum-updatesd will do this).
    # metadata_expire=90m

    # PUT YOUR REPOS HERE OR IN separate files named file.repo
    # in /etc/yum.repos.d    
    ```

3. Modify the sl.yml file to this:

<pre> 
- hosts: openstack  
  remote_user: root  
  tasks:  
  - copy: src=/home/centos/files/yum.conf dest=/etc/yum.conf owner=root group=root mode=0644  
  - name: Install sl  
    yum: name=sl state=installed  
</pre>    

4. Now run the sl.yml playbook and it should go a lot faster.
