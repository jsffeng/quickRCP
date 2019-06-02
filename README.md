Current usage:  
  
quickRCP \<filename\> \<remote hostname or IP\> \<remote login\> \<remote dir\>  
  
To-do:  
quickRCP  options:  
	-f: filename to ship  
	-h: remote hostname or IP  
	-u: remote login  
	-d: remote dir  
        -c: \<remote ogin\>@\<remote hostname or IP\>:\<remote path\>  
	-T: test mode, only for debugging purpose. Used by tool adminstrator only.  
Following option has default value in config file, but can be overwritten by command lines. If need to run this tool for a similar size file periodically between two servers, suggest to update config file as one time effort. In this way, no need to specify the following parameters again in commmand line.   
	-m: scp or rcp, default defined in config  
	-t: Seconds for periodical checks on if shipping complete  
	-s0: splitmode,[num|size]  
	-s1: splitnumber, example 10  
	-s2: splitsize, example 100m  
  
Example:  
quickRCP -f \<filename\> -c  \<remote login\>@\<remote hostname or IP\>:\<remote dir\>  
quickRCP -f \<filename\> -h \<remote hostname or IP\> -u \<remote login\> -p \<remote dir\>  
  
