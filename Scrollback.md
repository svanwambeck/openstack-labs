+++
date = "2016-2-09"
draft = false
weight = 20
title = "Using GNU Screen to Scroll Back"
+++

You can use GNU screen (commonly called "screen") to scroll back to view information that scrolled off the top of the machine. When you logged into the SSH proxy, a screen session was automatically started for you and normally just runs silently in the background. You can take advantage of your screen session to scroll back to view stuff that scrolled off the top of your browser window.  


## [What is GNU screen?](https://en.wikipedia.org/wiki/GNU_Screen)

1. Activate screen: 

    `[root@controller ~]$` `control-a`

    > You now have screen's attention!
    > Further commands will intercepted by screen
   
2. Enter COPY mode which will allow you to scroll back (Left square bracket)

    `[root@controller ~]$` `[`

    > You now have screen's attention!
    > Further commands will intercepted by screen
    > You won't actually use the copy feature, just scrollback

3. Scroll up and down one line at a time with the **arrow** keys

4. Scroll the display up and down by 1/2 screen with **control-u** and **control-d**

5. Scroll the display up and down by a full screen with **control-b** and **control-f**

6. Exit with the **Escape** key
