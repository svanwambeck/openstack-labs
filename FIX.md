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

### A fix to avoid slow yum mirror in anisble lab when a mirror is down and yum slows to a craw or completely fails.

1. Why are YUM updates taking so long!!
  - Here is the YUM mirror status: http://mirror-status.centos.org/
  - Here is yum.conf file info: https://docs.fedoraproject.org/en-US/Fedora/15/html/Deployment_Guide/sec-Configuring_Yum_and_Yum_Repositories.html
  - The default retries before YUM advances to the next mirror is **10 (TEN!!!)** retries, let's make that 1:
Copy this text into the files directory and name the file "yum.conf"

2. In your home directory, make a new directory called "files"

3. copy /etc/yum.conf to /~/files

4. Edit your new yum.conmf file by adding **retries=1** to the bottom of the config as shown below. 

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

5. Save the file

6. After you have downloaded sl.yml file, modify it to look like this:

<pre> 
  - hosts: openstack
    remote_user: root
    tasks:
    - name: Look at me adding my first line of devops code! The next line of code updates yum.conf on all my hosts, this is really cool.
      copy: src=/home/centos/files/yum.conf dest=/etc/yum.conf owner=root group=root mode=0644
    - name: Install sl even though I have no idea what sl does... yet.
      yum: name=sl state=installed
</pre>

Now run the sl.yml playbook and it should go a lot faster.

## How to save files from my Openstack Lab to view later

1. First do lab 13 which will set up an account with github

2. Then SSH into your controller and issue these commands

    `mkdir ~/myopenstack``

    `cd myopenstack`

    `yum install git`

    `git config --global user.name "---Your Name Here---"`

    `git config --global user.email "---your_email@example.com---"`

    `git config --list`

    `git init`

    `touch readme.txt`

    `vim readme.txt`

    > This is my test file to see if I can push a file up to gut hub.

    `git status`

    `git add readme.txt`

    `git commit -m 'This is supposed to add Readme.txt to my repository'`

    `git add`

    > CREATE REPOSITORY on github called 'myopenstack'

    `git remote add origin https://github.com/YOUR-ACCOUNT-NAME-HERE/myopenstack.git`

    `git push origin master`

    ` # respond to login`  
    ` # respond to password`

## Out of sync? Do this

  `git remove origin`

  `remote add origin https://github.com/YOUR-ACCOUNT-NAME-HERE/myopenstack.git`

  `git pull origin master`

  > This will sync github with your current directly

  `git push origin master`

  > Now that you are synced with github, this should work


