What do I need?
===============

In this tutorial we assume that your server has activated support for PHP and that all files ending in .php are handled by PHP. On most servers, this is the default extension for PHP files, but ask your server administrator to be sure. If your server supports PHP, then you do not need to do anything. Just create your .php files, put them in your web directory and the server will automatically parse them for you. There is no need to compile anything nor do you need to install any extra tools.

> **Note:**  
> If you want to use PHP locally you would need to install a webserver (e.g. [Apache][apache] or [nginx][nginx]) and of course [PHP][php-downloads]. For more information about installing a webserver and PHP please refer to [the installation manual][installation]. 

> **Note:**  
> Although not mandatory you may also want to install a database (e.g. [MySQL][mysql] or [PostgreSQL][postgresql]).

If you have problems with installing PHP yourself, we would suggest you ask your questions on our [installation mailing list][installation-mailinglist].

There are also some [pre-configured packages][pre-configured] for different operating systems, which will automatically install a webserver with PHP and a database with just a few mouse clicks.

> **Note:**  
> It is discouraged to use pre-configured packages on production systems, because the default settings of these packages are often not secure enough to be used on production server. They are however an easy way to get a test server up and running.

PHP can be installed on any operating system, including MacOSX, Linux and Windows. On Linux, you may find [rpmfind][rpmfind] and [PBone][pbone] helpful for locating RPMs. You may also want to visit [apt-get][aptget] to find packages for Debian.

[links]:http://php.net/links.php
[apache]:http://httpd.apache.org/
[nginx]:http://nginx.com/
[php-downloads]:http://www.php.net/downloads.php
[installation]:http://php.net/manual/en/install.php
[mysql]:http://www.mysql.com/downloads/
[postgresql]:http://www.postgresql.org/
[installation-mailinglist]:http://www.php.net/mailing-lists.php
[pre-configured]:http://wikipedia.org/wiki/List_of_AMP_packages
[rpmfind]:http://www.rpmfind.net/
[pbone]:http://rpm.pbone.net/
[aptget]:http://www.apt-get.org/