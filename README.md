Tool usage:  
------------  
USAGE:  quickRCP -f \<file name\> [-h \<remote host\>]  
		[-u \<remote login\>] [-d \<remote dir\>]  
		[-c \<remote login\>@\<remote host\>:\<remote dir\>]  
		[-m \<method\>] [-t \<time\>] [-M \<split mode\>]  
		[-N \<split number\>] [-S \<split size\>]  
		[-T] [-H]  
  
Regular options:  
	-f 	file name for shipping,required option  
	-h	remote host name or IP  
	-u	remote login  
	-d	remote directory  
	-c	if this option is used, option -h,-u,-d should not be used  
	-T	test mode, only used by tool adminstrator for quick debugging   
	-H	print usage message  
  
Alternative options:  
	-m	shipping mothod, valid value is [rcp|scp]  
	-t	seconds for periodical checks for shipping completion  
	-M	split mode, valid value is [NUMBER|SIZE]  
	-N	split number, when -s0 specify num, split input file with this number, example 10  
	-S	byte of split size, when -s0 specify size, split input file with this size, example 100m   
  
Note: 	All alternative options have default value in Config file, and can be used to   
	overwrite the default value by command line. However, to update Config file   
	with new default value may be a simpler way to achieve the same.  
  
Examples:  
	 quickRCP -f file1.cpio -h 192.168.1.90 -u username -d /usr/tmp -m scp  
	 quickRCP -f file1.cpio -c username@192.168.1.90:/usr/tmp  
  
Dependent packages & tools:  
----------------------  
- Korn Shell - /bin/ksh93  
- rsh or ssh  
- tools: split, awk  
  
Test environment:  
-------------------  
- ubuntu server -> ubuntu server, yes  
- Solaris server -> Solaris server, to-do  
- ubuntu server to Solaris server not tested  
	- One difference between the two system is the result of "sum -r", this can be handled by the tool.  
	- Not sure whether there are other diferences for the commands.  
