# [Creating Your Own Server - without a credit card](https://www.reddit.com/r/linuxupskillchallenge/comments/nmfo4o/day_0_creating_your_own_server_without_a_credit/)

## INTRO

Linux has a rich set of features for running scheduled tasks. One of the key attributes of a good sysadmin is getting the computer to do your work for you (sometimes misrepresented as laziness!) - and a well configured set of scheduled tasks is key to keeping your server running well.

## CRON

Each user potentially has their own set of scheduled task which can be listed with the `crontab` command (list out your user crontab entry with `crontab -l` and then that for _root_ with `sudo crontab -l` ).

However, there’s also a system-wide crontab defined in `/etc/crontab` - use `less` to look at this. Here's example, along with an explanation:

```
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow user  command
17 *	* * *   root	cd / && run-parts --report /etc/cron.hourly
25 6	* * *   root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6	* * 7   root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6	1 * *   root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
```
Lines beginning with "#" are comments, so `# m h dom mon dow user command` defines the meanings of the columns.

Although the detail is a bit complex, it's pretty clear what this does. The _first line_ says that __at 17mins after every hour, on every day__, the credential for "root" will be used to run any scripts in the `/etc/cron.hourly` folder - and similar logic kicks off __daily__, __weekly__ and __monthly__ scripts. This is a tidy way to organise things, and many Linux distributions use this approach. It does mean we have to look in those `/etc/cron.*` folders to see what’s actually scheduled.

On your system type: `ls /etc/cron.daily` - you'll see something like this:
```
$ ls /etc/cron.daily
apache2  apt  aptitude  bsdmainutils  locate  logrotate  man-db  mlocate  standard  sysklog
```
Each of these files is a script or a shortcut to a script to do some regular task, and they're run in __alphabetic__ order by `run-parts`. So in this case _apache2_ will run first. Use `less` to view some of the scripts on your system - many will look very complex and are best left well alone, but others may be just a few lines of simple commands.

Look at the articles in the resources section below - you should be aware of `at` and `anacron` but are _not likely to use them in a server_.

Google for "logrotate", and then look at the logs in your own server to see how they've been "rotated".

## SYSTEMD TIMERS

All major Linux distributions now include "systemd". As well as starting and stopping services, this can also be used to run tasks at specific times via "timers". See which ones are already configured on your server with:

`systemctl list-timers`

Use the links in the RESOURCES section to read up about how these timers work.

## RESOURCES

- [A good overview of systemd/Timers](https://wiki.archlinux.org/index.php/Systemd/Timers)

- ["How to Use Systemd Timers as a Cron Replacement"](https://www.maketecheasier.com/use-systemd-timers-as-cron-replacement/)
