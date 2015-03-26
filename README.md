TuxLite Quick-start Guide
=============
[TuxLite](http://tuxlite.com) is a free collection of shell scripts for rapid deployment of LAMP and LNMP stacks (Linux, Apache/Nginx, MySQL and PHP) for Debian and Ubuntu.

This guide will explore it's use and deployment, as well as steps to bring into full production. Portions of this guide are excerpts from the [TuxLite](http://tuxlite.com) website. For a better understanding of the script, it is **highly** that you visit the [TuxLite](http://tuxlite.com) website before proceeding.

Base Installation[1](http://tuxlite.com/installation/)
--------------------------
The initial installation entails downloading, configuring, and executing the TuxLite script.

To get started, you need to SSH into your server a become root by executing `$ sudo su`

Then, proceed with following steps to obtain and configure the script:

- `$ mkdir tuxlite`
- `$ cd tuxlite`
- ` $ wget http://tuxlite.com/scripts/tuxlite.tar.gz`
- ` $ tar xzf tuxlite.tar.gz`
- ` $ nano options.conf`

Before proceeding, it is recommended that you fully explore `options.conf`.

Of the available options, I recommend setting:

`CONFIGURE_APT=no` as apt mirrors are not necessarily reliable sources.

`USE_NGINX_ORG_REPO=yes` for faster updates.

Once `options.conf` is configured to your liking.

- `$ chmod 700 *.sh && chmod 700 options.conf`

To execute the script, execute:

- `$ ./install.sh`

SysAdmin
-----------------
Following the TuxLite tutorial you need to add a user:

`$ adduser johndoe`

However, the script disables root login, so you need to grant at least one user with sudo rights for system administration.

`$  sudo usermod -a -G sudo johndoe`

As this user is the sysadmin, forward all system email, normally sent to `root@localhost` to this user

`$ echo "root: john@doe.com" >> /etc/aliases && newaliases`

Finalizing the base
----------------------
Add a domain to the server

`$ ./domain.sh add johndoe yourdomain.com`

Optionally, install  database GUI

`$ ./setup.sh dbgui`

Once again, please consult the [TuxLite installation guide](http://tuxlite.com/installation/)

Server Hardening
-------------------
###fail2ban

`$ aptitude install fail2ban`

Configure fail2ban to whitelist your IP address and to send you ban notification emails:

`$ cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local`
   
`$ nano /etc/fail2ban/jail.local`

- ignoreip = 127.0.0.1 [yourIP]
- action = %(action_mw)

###[ConfigServer Security & Firewall](http://configserver.com/free/csf/install.txt)

`$ wget http://www.configserver.com/free/csf.tgz`

`$ tar -xzf csf.tgz`

`$ cd csf`

`$ sh install.sh`

Next, test whether you have the required iptables modules:

`$ perl /usr/local/csf/bin/csftest.pl`

### Install  apticron
Generates email listing packages  which are pending an upgrade

`$ sudo apt-get install apticron`
