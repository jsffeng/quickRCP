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
  
How it works:  
----------------------  
- The idea is quite simple - split the large file into small pieces and ship them in multiple rcp or   
scp processess, then merge them into the final file at the destination once all shippings complete.  
- Why choosing script rather than programming languages supporting multi-processes or multi-threads?  
	- Based on the basic idea, the nature of this tool is just to automate the unix/linux command  
rcp/scp in the user's own environment, and script is suitable to achieve this. The challenging part may   
be to track the status of each process. State machine files (NS -Not Start, IP - In Progress, CO -   
Completed) used to help this. Also /proc/<process id> is used to ensure the process is still alive,  
and not dying without updating State machine files. Of course, neccesary environment checks, temprary   
directories' cleanup and sub-processes clean up also need to be taken care of by the tool whenever any   
abormal aborting happens.  
	- Use script is easy for users to debug their own environment issues causing any failure.  
	- Also using script could more portable for any server which supports Linux/Unix shell.  
    
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
- From Linux (ubuntu) server to Linux (ubuntu) server, test pass    
- From Solaris server to Solaris server, to-do  
- From Linux (ubuntu) server to Solaris server, no plan to test    
	- One difference between the two systems is the result of "sum -r", and now tool can handle it.     
	- A further testing is needed if intending to use it between Linux and Solaris or other UNIX servers.     
