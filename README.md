Tool Usage:  
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
  
Development Environment:  
----------------------  
- Initial version developed on Solaris 10 server, support rsh/rcp and basic sun day scenarios,  
but the followings were not supported:  
	- ssh/scp,rainy day handling, Config file and related options, command line interface, etc.  
- Full version completed on Linux ubuntu 16.04.01.  
  
Dependent packages/tools:
----------------------  
- Korn Shell - /bin/ksh93  
- rsh or ssh  
- awk
- tools - split, sum
  
Test environment:  
-------------------  
- From ubuntu server to ubuntu server, test pass    
- From Solaris server to Solaris server, to-do  
- From ubuntu server to Solaris server, no plan to test    
	- One difference between the two systems is the result of "sum -r", this can be handled by the tool.  
	- If there is such need, need to test to see if any further modification is required   
