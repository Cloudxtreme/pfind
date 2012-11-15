pfind
=====

## ABOUT

`pfind` is a process finder and manupulation tool with command line syntax
like that of `find`. **It is not finished yet**, but stay tuned.

## WORKING EXAMPLES

	pfind -exe /bin/bash -or -exe /bin/csh

	pfind -exe /usr/sbin/apache -and -cwd '/var/www*'
	# -and is optional, the following command line does the same thing:
	pfind -exe /usr/sbin/apache -cwd '/var/www*'
	
	# print something more than just a list of PIDs:
	pfind [ -exe /bin/rm -or -cwd /etc ] -printf '%exe (pid=%pid) in %{cwd}\n'

	# send SIGHUP to process with pid in /var/run/apache.pid,
	# but only if it is really /usr/bin/apache:
	pfind -pidfile /var/run/apache.pid -exe /usr/sbin/apache -hup

	# show process tree:
	pfind [ -pidfile /var/run/apache.pid -exe /usr/sbin/apache \
		-or -descendants ] -ps jf

	# kill the whole process tree:
	pfind [ -pidfile /var/run/apache.pid -exe /usr/sbin/apache \
		-or -descendants ] -kill

	# pretty print list of processes with big utime, sorted by utime:
	pfind %stat::utime -gt 100 -sort -%stat::utime \
		-print1 'UTIME \tPID \tCOMM\n' \
		-printf '%stat::utime \t%pid \t%comm\n'

## NOT YET IMPLEMENTED EXAMPLES

	# "+" is to run `ps` command with all pids, not one by one:
	pfind -user mike -exec ps j {} +		

	# same as previous
	pfind -user mike -ps-j

	# interactive kill, ';' is to run `kill` for each PID one by one
	pfind -user mike -ok kill {} ';'

## REQUIREMENTS

* `linux` with `procfs` mounted
* `perl`
* `Parse::Yapp`

