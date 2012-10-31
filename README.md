pfind
=====

## ABOUT

`pfind` is a process finder and manupulation tool with command line syntax
like that of `find`. **It is not finished yet**, but stay tuned.

## WORKING EXAMPLES

	pfind -exe bash
	pfind -exe apache -and -cwd /var/www		# -and is optional
	pfind [ -exe rm -or -cwd /etc ] -printf '%exe (pid=%pid) in %{cwd}\n'

## NOT YET IMPLEMENTED EXAMPLES

	pfind -pidfile /var/run/apache.pid -exe /usr/sbin/apache -hup
	pfind -user mike -exec ps j {} +
	pfind -user mike -ps-j				# same as previous
	pfind -user mike -ok kill {} ';'		# interactive kill

## REQUIREMENTS

* `linux` with `procfs` mounted
* `perl`
* `Parse::Yapp`

