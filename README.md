pfind
=====

## ABOUT

`pfind` is a process finder and manupulation tool with command line syntax
like that of `find`.

## USAGE EXAMPLES

	pfind %exe == /bin/bash -or %exe == /bin/csh

Pattern matching with `-m`:

	pfind %exe == /usr/sbin/apache -and %cwd -m '/var/www*'

Print something more than just a list of PIDs:

	pfind [ %exe == /bin/rm -or %cwd == /etc ] -printf '%exe (pid=%pid) in %{cwd}\n'

Send `SIGHUP` to process with PID in `/var/run/apache.pid`,
but only if it is really `/usr/bin/apache`:

	pfind -pidfile /var/run/apache.pid -and %exe == /usr/sbin/apache -hup

Show process tree:

	pfind [ -pidfile /var/run/apache.pid -and %exe == /usr/sbin/apache \
		-or -descendants ] -ps jf

Kill the whole process tree:

	pfind [ -pidfile /var/run/apache.pid -and %exe == /usr/sbin/apache \
		-or -descendants ] -kill

Pretty print list of processes with big `utime`, sorted by `utime`:

	pfind %stat::utime -gt 100 -sort -%stat::utime \
		-print1 'UTIME \tPID \tCOMM\n' \
		-printf '%stat::utime \t%pid \t%comm\n'

`+` is to run `ps` command with all PIDs, not one by one:

	pfind %user == mike -exec ps j {} +		

Same as previous:

	pfind %user == mike -ps j

## NOT YET IMPLEMENTED EXAMPLES

Interactive kill, `;` is to run `kill` for each PID one by one:

	pfind %user == mike -ok kill {} ';'

## REQUIREMENTS

* `linux` with `procfs` mounted
* `perl`
* `Parse::Yapp`

