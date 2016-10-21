# recinstall

## Description
A bash script that will create an uninstall shell script for locally installed programs from source code.
This script will work for local installed application that you build from source code. It will not work if in the same installation directory multiple users install programs with make install the same time.

## Usage
Use this script instead of `make install` command.
For example you want the [GNU awk](http://ftp.gnu.org/gnu/gawk/gawk-4.1.4.tar.gz) program and install it local in a folder of your home directory.
```
 xigpadi  edeacts0702  ~  $ wget http://ftp.gnu.org/gnu/gawk/gawk-4.1.4.tar.gz
--2016-10-21 14:43:14--  http://ftp.gnu.org/gnu/gawk/gawk-4.1.4.tar.gz
Resolving ftp.gnu.org... 208.118.235.20
Connecting to ftp.gnu.org|208.118.235.20|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 4582398 (4.4M) [application/x-gzip]
Saving to: `gawk-4.1.4.tar.gz'

100%[==================================================================================================>] 4,582,398    330K/s   in 11s

2016-10-21 14:43:26 (401 KB/s) - `gawk-4.1.4.tar.gz' saved [4582398/4582398]

 xigpadi  edeacts0702  ~  $ tar -zxvf gawk-4.1.4.tar.gz
 xigpadi  edeacts0702  ~/gawk-4.1.4  $ ./configure --prefix=/home/xigpadi/local
checking for a BSD-compatible install... ./install-sh -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /home/xigpadi/opt/bin/mkdir -p
checking for gawk... gawk
checking whether make sets $(MAKE)... yes
checking whether make supports nested variables... yes
...
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating Makefile
config.status: creating config.h
config.status: executing depfiles commands
config.status: executing libtool commands
 xigpadi  edeacts0702  ~/gawk-4.1.4  $ make -j 4
...
make[2]: Entering directory '/home/xigpadi/gawk-4.1.4/po'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/home/xigpadi/gawk-4.1.4/po'
Making all in test
make[2]: Entering directory '/home/xigpadi/gawk-4.1.4/test'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/home/xigpadi/gawk-4.1.4/test'
make[1]: Leaving directory '/home/xigpadi/gawk-4.1.4'
 xigpadi  edeacts0702  ~/gawk-4.1.4  $ recinstall
Getting current timestamp
Making install in .
make[1]: Entering directory '/home/xigpadi/gawk-4.1.4'
make[2]: Entering directory '/home/xigpadi/gawk-4.1.4'
 /home/xigpadi/opt/bin/mkdir -p '/home/xigpadi/local/bin'
  ./install-sh -c gawk '/home/xigpadi/local/bin'
make 'CFLAGS=-g -O2 -DNDEBUG' 'LDFLAGS=' install-exec-hook
make[3]: Entering directory '/home/xigpadi/gawk-4.1.4'
(cd /home/xigpadi/local/bin; \
name=`echo gawk | sed 's,x,x,'` ; \
ln ${name} gawk-4.1.4 2>/dev/null ; \
if [ ! -f awk ]; \
then    ln -s ${name} awk; \
fi; exit 0)
make[3]: Leaving directory '/home/xigpadi/gawk-4.1.4'
...
make[1]: Leaving directory '/home/xigpadi/gawk-4.1.4/po'
Making install in test
make[1]: Entering directory '/home/xigpadi/gawk-4.1.4/test'
make[2]: Entering directory '/home/xigpadi/gawk-4.1.4/test'
make[2]: Nothing to be done for 'install-exec-am'.
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/home/xigpadi/gawk-4.1.4/test'
make[1]: Leaving directory '/home/xigpadi/gawk-4.1.4/test'
Find files changed after make install
Uninstall script saved in '/home/xigpadi/uninstall_scripts' as 'gawk-4.1.4.sh'
 xigpadi  edeacts0702  ~/gawk-4.1.4  $
```
Now under your home directory and in folder *uninstall_scripts* there is a shell script *gawk-4.1.4.sh* that will remove
the local install gawk when you run it.

