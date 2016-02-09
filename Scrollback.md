+++
date = "2016-2-09"
draft = false
weight = 20
title = "Using Screen to Scroll Back"
+++

#### Objective
Use screen to scroll back to view information that scrolled off the top of the machine.

When you use your browser to perform CLI changes, you are using HTTP to connect to Shell In a Box, which connects you to a screen session, which in turn uses SSH to connect to your lab environment.


## [What is screen?](https://en.wikipedia.org/wiki/GNU_Screen)

1. Activate screen: 

    `[root@controller ~]$` `control-a`

    > You now have screen's attention!
    > Further commands will intercepted by screen
   
2. Enter COPY mode (Left square bracket)
    `[root@controller ~]$` `[`
    > You now have screen's attention!
    > Further commands will intercepted by screen
3. Scroll up and down one line at a time with the **arrow** keys

4. Scroll the display up and down by 1/2 screen with **control-u** and **control-d**

5. Scroll the display up and down by a full with **control-b** and **control-f**

2. Exit with the **Escape** key
