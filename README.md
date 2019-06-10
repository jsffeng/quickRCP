Tool Usage:  
------------  
USAGE:  quickRCP -f \<file name\> [-h \<remote host\>]  
		[-u \<remote login\>] [-d \<remote dir\>]  
		[-c \<remote login\>@\<remote host\>:\<remote dir\>]  
		[-m \<method\>] [-t \<time\>] [-M \<split mode\>]  
		[-N \<split number\>] [-S \<split size\>]  
		[-T] [-H]  
  
Regular options:  
	-f 	file name for shipping, required option  
	-h	remote host name or IP  
	-u	remote login  
	-d	remote directory  
	-c	if this option is used, option -h,-u,-d should not be used  
	-T	test mode, only used by tool administrator for quick debugging   
	-H	print usage message  
  
Alternative options:  
	-m	shipping method, valid value is [rcp|scp]  
	-t	seconds for periodical checks for shipping completion  
	-M	split mode, valid value is [NUMBER|SIZE] on Linux. On Solaris, only SIZE supported  
	-N	split number, when -M specify NUMBER, split input file with this number, example 10  
	-S	byte of split size, when -M specify SIZE, split input file with this size, example 100m   
  
Note: 	All alternative options have default value in Config file, and can be used to   
	overwrite the default value by command line. However, to update Config file   
	with new default value may be a simpler way to achieve the same.  
  
Examples:  
	 quickRCP -f file1.cpio -h 192.168.1.90 -u username -d /usr/tmp -m scp  
	 quickRCP -f file1.cpio -c username@192.168.1.90:/usr/tmp  
    
How it works:  
----------------------  
- The idea is quite simple: to split the large file into small pieces and ship them by multiple background 
rcp/scp processess, and finally merge them into one file in the destination once all shippings complete.  
- Why choosing script rather than programming languages supporting multi-processes or multi-threads better?  
	- Based on the basic idea, the nature of this tool is just to automate the unix/linux command  
rcp/scp in the user's own environment, and scripting is suitable such purpose. With this, to take care of      
well tracking the status of each process, simple state machine files (i.e. NS-Not Start, IP-In Progress,   
CO-Completed) have been introduced, and also /proc/<process id> is used to very if the process is alive,i.e.    
not dying without telling State machine files. Of course, neccesary environment checks, temporary   
directories' cleanup and child processes' cleanup also need to be taken care of by the tool in case that any   
unexpected aborting happens.  
	- Script could be easier for users to debug their own environment issues related to any failures.  
	- Also script could be more convient for being ported to any server which supports Linux/Unix shell.  
    
Development Environment:  
----------------------  
- Initial version developed on Solaris 10 server, with supporting rsh/rcp and basic sun day scenarios,  
but the followings were not covered:  
	- ssh/scp,rainy day handling, Config file and more options, command line interface, etc.  
- Full version completed and tested on Linux ubuntu 16.04.01, then tested on Solaris 8 server.  
To ensure to be compatible,some new syntax has been replaced with old style syntax, for example:  
	- let variable++ ===> let variable=variable+1  
	- ${variable//[0-9]}  ==> echo ${variable} |sed "s/[0-9]//g"   
	- ${varible:0-1:1} ==> echo ${variable} |sed "s/\(.*\)\(.\)$/\2/"  
  
Dependent packages/tools:  
----------------------  
- Korn Shell - /bin/ksh  
- rsh or ssh (need to config remote access w/o password, please reference Internet resources if you need help)  
- awk
- tools - split, sum, pstree
  
Test environment:  
-------------------  
- From Linux (ubuntu) server to Linux (ubuntu) server    
- From Solaris 8 server to Solaris 10 server
   
Bugfix Backlog (To-do):  
-------------------  
- rsh hanging has been observed to run rsh to some certain server(although most of Linux/Solaris server are   
okay). This may be related to the specfic configuration on the targeted server, however, this will cause   
the tool hanging unexpetedly.  
	- Status: Enhanced but no perfect fix yet. To support ConnectTimeout option has been done to ssh,  
however, for rsh, not all versions supporting timeout option, e.g. FreeBSD support "-t timeout" for rsh,  
but looks Solaris and ubuntu never support that.   
  
