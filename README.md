xtBackup
========

Development of this project was sponsored by [xtmotion.com](http://www.xtmotion.com).

Requirements
------------

* PHP 5.3 and above
  * with SQLite support

Features
--------

* ready to be used as command line tool (provided by xtbackup.php tool)
* no installation needed, works everywhere where PHP 5.3 and above is installed
  * [DreamHost](http://www.dreamhost.com/) tested
* designed as re-usable PHP code library
* configurable with single/multiple INI file(s) and command line options
* efficient compare algorithm
  * works with huge amount of files
  * minimize traffic and CPU
  * use time and md5 for change detection
  * sqlite3 implementation
* backup from Linux/Windows file system
  * support for UTF8 file names
  * support for case-sensitive file names
  * symlink handling
* backup to Amazon S3 storage
  * parallel upload multiple parts of huge files
  * multiple backups into the same bucket
  * on 32bit architecture, current implementation of the PHP-AWS library doesn't support files over 2GB
* configurable independent output drivers
  * output to console
  * log into sqlite database
* extendable with PHP code
  * file filters
  * new storage drivers
  * backup preparation processes (DB, subversion, etc.)
  * improved compare algorithm

Installation
------------

* get code from <http://github.com/k2s/xtbackup>
  * git clone git://github.com/k2s/xtbackup.git
  * cd xtbackup
  * git submodule update --init
* copy examples/minimal.ini and examples/s3access.ini to own folder
* modify this files (see Configuration section)
* test environment for Amazon S3 backups (read the output): `php -f xtbackup.php ini[]=/path_to/minimal.ini storage.s3.compatibility-test=true`
* dry run with : `php -f xtbackup.php ini[]=/path_to/s3access.ini ini[]=/path_to/minimal.ini`
* to really upload files: `php -f xtbackup.php ini[]=/path_to/s3access.ini ini[]=/path_to/minimal.ini storage.s3.update=true`

### Docker

There is Docker image in [Doicker registry](https://registry.hub.docker.com/u/bigm/xtbackup/) . 

Configuration
-------------

### Quick

* run: `php -f xtbackup.php -- --init > myconfig.ini`
* edit myconfig.ini
* run: `php -f xtbackup.php -- ini[]=myconfig.ini`

### Configuration explained

`xtbackup` is build as library which may be included into different programs.
The controll programm `xtbackup.php` is provided to make backup task functionality available and it makes it possible to execute backup tasks.

`xtbackup.php` by itself interprets following command line options:

* --help : will output basic information how to use the programm
* --init : generate documented INI skeleton
* --quiet-start : it is possible to suppress output to console in start phase of engine

All other command line parameters passed to `xtbackup.php` are forwarded to `xtbackup engine` as configuration options.

Most of configuration is done in INI file(s), but command line passed options have precedence over INI definitions.
Special case is the `ini[]` options which can't be used in INI files.
It is possible to define multiple `ini[]` options on command line, they precedence is given in order they are listed.
The purpose of multiple `ini[]` options and precedence of command line options over INI is:
* sharing of configuration
* security, credentials may be stored in private INI files

To start with backup follow:

* run: `xtbackup.php --init > myconfig.ini`
* edit myconfig.ini
* run: `xtbackup.php ini[]=myconfig.ini`

### Configuration reference

Read output of `xtbackup.php --init`, that is all we have and yes, you are welcome to contribute with more and better documentation.

### Program output

xtbackup.php
------------

### Return codes

### Creating PHAR package

Support
-------

Submit issues or support requests to <http://github.com/k2s/xtbackup/issues>.

Warranty
--------

USE ON YOUR OWN RISK. WITHOUT ANY EXPRESS OR IMPLIED WARRANTIES.
This project is used in production environment to backup data and MySQL databases to local and S3 storage.
The Authors will not be responsible for any damage users may suffer, including but not limited to, loss of data.

Resources
---------

* working with Amazon S3:
  * <http://www.dragondisk.com>
* writing with Markup
  * <http://daringfireball.net/projects/markdown/syntax>
  * <http://daringfireball.net/projects/markdown/dingus>
  * <http://github.github.com/github-flavored-markdown>

Contributors
------------

* work donated by [xtmotion.com](http://www.xtmotion.com)
* Martin Minka
* Alex Melnyk
* Artem Komarov

Credits
-------

xtBackup uses following libraries:

* [SQLite](http://www.sqlite.org/)
* [AWS SDK for PHP](https://github.com/amazonwebservices/aws-sdk-for-php)
* [PHP-GetOpts](https://github.com/hash-bang/PHP-GetOpts)

License
-------

xtBackup is free and unencumbered public domain software. For more information, see http://unlicense.org/ or the accompanying UNLICENSE file.