# You've got mail

I recently began using cronjobs to manage and schedule different type of analytics scripts on a dev VM at work. When the jobs occaisionally fail to execute, crontab may also fail to send me a notificaiton mesage. These mesasges get spooled on my VM and I wanted to access them

###  Where is that mail
Well its likely to live in /var/mail/$USER. Access it with the below command

```
$ nano /var/mail/$USER
```

Most often the messages contain output of cron jobs, or a system security report by logwatch, or similar junk. Read it and find out.

Occaisionally, you may run into IPv6 sending guideline errors depending on your configuration. Check out [ipv6-support-is-disabled-warnings](http://unix.stackexchange.com/questions/64414/ipv6-support-is-disabled-warnings) and [reload postfix](http://www.cyberciti.biz/faq/linux-unix-start-stop-restart-postfix/) for handling guidance