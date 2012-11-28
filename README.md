pfind
=====

## ABOUT

`pfind` is a process finder and manupulation tool with command line syntax
like that of `find` or `tcpdump`.

## USAGE EXAMPLES

Print all shell processes:

	pfind -exe /bin/bash -or -exe /bin/csh

Same as previous:

	pfind %exe == /bin/bash -o %exe == /bin/csh

Pattern matching with `-m`:

	pfind -exe /usr/sbin/apache -and %cwd -m '/var/www*'

Print something more than just a list of PIDs:

	pfind [ -exe /bin/rm -or -cwd /etc ] -printf '%exe (pid=%pid) in %cwd\n'

Send `SIGHUP` to process with PID in `/var/run/apache.pid`,
but only if it is really `/usr/bin/apache`:

	pfind -pidfile /var/run/apache.pid -and %exe == /usr/sbin/apache -hup

Show process tree:

	pfind [ -pidfile /var/run/apache.pid -and -exe /usr/sbin/apache -or -descendants ] -ps

Kill the whole process tree:

	pfind [ -pidfile /var/run/apache.pid -and -exe /usr/sbin/apache -or -descendants ] -kill

Pretty print list of processes with big `utime`, sorted by `utime`:

	pfind %utime := %stat::utime %utime -gt 100 -sort -%utime -echo1 'UTIME \tPID \tCOMM' -echo '%utime \t%pid \t%comm'

## NOT YET IMPLEMENTED EXAMPLES

Show all processes of user `mike`:

	pfind -user mike -ps

Same as previous (`+` is to run the command with all PIDs, not one by one):

	pfind %user == mike -exec ps uf {} +

Interactive kill, `;` is to run `kill` for each PID one by one:

	pfind %user == mike -ok kill {} ';'

## REQUIREMENTS

* `linux` with `procfs` mounted
* `perl`
* `Parse::Yapp`

