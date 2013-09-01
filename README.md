TuxLite Quick-start Guide
=============
[TuxLite](http://tuxlite.com) is a free collection of shell scripts for rapid deployment of LAMP and LNMP stacks (Linux, Apache/Nginx, MySQL and PHP) for Debian and Ubuntu.

This guide will explore it's use and deployment, as well as steps to bring into full production. Portions of this guide are excerpts from the [TuxLite](http://tuxlite.com) website. For a better understanding of the script, it is **highly* * that you visit the [TuxLite](http://tuxlite.com) website before proceeding.

Base Installation[1](http://tuxlite.com/installation/)
_________________
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


