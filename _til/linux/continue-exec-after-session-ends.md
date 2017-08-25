---
title: Continue a Program after Ending an SSH Session
category: linux 
---


Assuming that you have a program running in the foreground, press ```ctrl-Z```, then:
```
[1]+  Stopped                 myprogram
$ disown -h %1
$ bg 1
[1]+ myprogram &
$ logout
```

If there is only one job, then you don't need to specify the job number. Just use ```disown -h``` and ```bg```.
Explanation of the above steps:

You press ```ctrl-Z```. The system suspends the running program, displays a job number and a "Stopped" message and returns you to a bash prompt.

You type the ```disown -h %1``` command (here, I've used a 1, but you'd use the job number that was displayed in the Stopped message) which marks the job so it ignores the SIGHUP signal (it will not be stopped by logging out).

Next, type the ```bg``` command using the same job number; this resumes the running of the program in the background and a message is displayed confirming that.

You can now log out and it will continue running..
