Current usage:

quickRCP <filename> <remote hostname or IP> <remote ogin> <remote path>

To-do:
quickRCP  options:
	-f:
	-h:
	-u:
	-p:
        -c: <remote ogin>@<remote hostname or IP>:<remote path>
	-T: test mode, for debugging purpose
Following option has default value in config file, but can be overwritten by command lines. If such parameter has no change every time, suggest to update config file as one time effort.
	-m: scp or rcp, default defined in config
	-t: Seconds for periodical checks on if shipping complete
	-s0: splitmode,[num|size]
	-s1: splitnumber, example 10
	-s2: splitsize, example 100m

Example:
quickRCP -f <filename> -c  <remote ogin>@<remote hostname or IP>:<remote path>
quickRCP -f <filename> -h <remote hostname or IP> -u <remote ogin> -p <remote path>

