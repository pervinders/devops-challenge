# Devops Challenge

# Assignment 1

Troubleshooting

The interface that integrates our system with that of our SMS Gateway partner started
to produce some weird intermittent errors recently.
Here is how the process works:
1) Periodically, we run a program called generate_data, which generates a number of files that
are stored in /opt/sms/AU/mo

2) Also periodically, we run a program called process_data that processes these files and inte-
grates them into our system.

3) When we run process_data, the correct/expected output should be:
1. All files processed, or
2. Processing skipped

4) When an error occurs, the output is:

1. ERROR: Failed processing files.

To trigger the issue you can run the following from the command line:
generate_data && process_data
Running this a few times in a row should definitely trigger the mentioned error.
Can you:
1) What all are the possibilities that may cause this intermetent error
2) Explain the steps you took troubleshooting this intermittent error?



Answer 1 : 
Other Possibilites
1) generate_data will create another process for the data which has to be processed and will log error as file/directory already in use due to which log may generate in bulk printing same error . 
  - if the process which is running to generate_data is in stale mode or had the error due to which generate_data was unable to create complete the file and have some error , it can go in exit mode and failure of generate_data , and  as we are using "&&" to process_data the return code will not be 0 so process_data should  exit immediately  after generate_data pid process exits .


  - one of the reason that can cause the issue as generate_data using other tool to generate data such as DB , REST API , WEBSOCKET to fetch data and inserting onto to memory/db/file but due to the connection issues the response time is longer than usual . That can cause false data in storage system , which may lead to ERROR: Failed processing file 


  - Another possible reason that can cause the error permissions issue of the user for reading a particular path 


  - Another possible reason due to disk space full due to which reading of file and process will start throwing same error 


  - Another possible reason due to machine resources utillization as due to heavy data , consumption of reasources may go high resulting in error.

  - Any of the service which is being used by the process_data is down .




  
2) Troubleshooting steps 
  -  First check disk/memory  utilization 
  -  Check user has the access of all the paths/directories/files which is used by both the generate_data and process_data 
  -  check if the process is already running or in stalled PID using ps -ef | grep "generate_data\|process_data" 
  -  connectivity of the host and client machine 
  -  check services are up and running , services being used don't have any error , if services are running on other container/vm or locally don't have error in generating data .
  -  check connectivity of external connection used by generate_data/process_data .
  -  check cron jobs if make sure to hash them while performing manual execution .
  -  Take Health Check of entire system so that conditions required to process_data are fulfilled .




 






# Assigment 2

A client has a Linux server that has just paged you because of a high 
load average issue. Upon connecting and running uptime you see:
12:20:50 up 1 day, 10:52, 6 users, load average: 44.28, 33.34, 30.44
How would you troubleshoot this issue to find out what is the source of 
the load and what tools would you use? Please list also what would you 
look for in the output of the commands that you would run.


Answer :
as mentioned 
12:20:50 up 1 day, 10:52, 6 users, load average: 44.28, 33.34, 30.44

uptime copmmands shows load average used in 1 , 5 , 15 minutes 

commands : 
free -h
 - check the memory consumption of free and used  , swap usage 


 
df -kh
 - disk space of any directory is full or have files being logged to some directory 


iostat
 - check i/o of file read write of the disk mounted device or folder consuming space 


vmstat <seconds> <number of output>
  - to check ip system memory swap cpu , traps disks and block IO 



 
top
 - to check the tasks, service total running , sleeping and zombie processes . 



htop 
  - to check the usage of memory in interactive way by sorting of process with memory consumption / CPU 

  - nice value priority given by the system to run if consuming memory cpu or have child process running 


ps -ef 
  - by using variouse option grep the process of zombie process or process have exited but still showing on ps -ef 
  - killing process using PID 
  - sorting process with mem usage ps aux --sort -rss




 











# Assigment 3
Complete quickly this AWS Quiz 
https://forms.gle/dHyVMCubGiHEL3ev9


Submitted on above link
