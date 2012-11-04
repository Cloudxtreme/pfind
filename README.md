pfind
=====

## ABOUT

`pfind` is a process finder and manupulation tool with command line syntax
like that of `find`. **It is not finished yet**, but stay tuned.

## WORKING EXAMPLES

	pfind -exe /bin/bash -or -exe /bin/csh

	pfind -exe apache -and -cwd /var/www
	# -and is optional, the following command line does the same thing:
	pfind -exe apache -cwd /var/www
	
	# print something more than just a list of PIDs:
	pfind [ -exe rm -or -cwd /etc ] -printf '%exe (pid=%pid) in %{cwd}\n'

## NOT YET IMPLEMENTED EXAMPLES

	# send SIGHUP to process with pid in /var/run/apache.pid,
	# but only if it is really /usr/bin/apache:
	pfind -pidfile /var/run/apache.pid -exe /usr/sbin/apache -hup

	# kill the whole process tree:
	pfind [ -pidfile /var/run/apache.pid -exe /usr/sbin/apache \
		-or -descendants ] -kill

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

