Taken from Cisco Linux Essential course!

# Ch-3/Working in Linux

## Email Services

- When discussing email servers, it is always helpful to look at the 3 different tasks required to get email between people:

__Mail Transfer Agent (MTA)__

- The most well known MTA (software that is used to transfer electronic messages to other systems) is __Sendmail__. __Postfix__ is another popular one and aims to be simpler and more secure than Sendmail.
    
__Mail Delivery Agent (MDA)__

- Also called the __Local Delivery Agent__, it takes care of storing the email in the user’s mailbox. Usually invoked from the final MTA in the chain.
    
__POP/IMAP Server__

- The __Post Office Protocol (POP)__ and __Internet Message Access Protocol (IMAP)__ are two communication protocols that let an email client running on your computer talk to a remote server to pick up the email.

- __Dovecot__ is a popular POP/IMAP server owing to its ease of use and low maintenance. __Cyrus IMAP__ is another option.

# File Sharing

- For __Windows-centric__ file sharing, __Samba__ is the clear winner.
- Samba allows a Linux machine to look and behave like a Windows machine so that it can share files and participate in a Windows domain. 

- The __Netatalk project__ lets a Linux machine perform as an __Apple Macintosh__ file server.
- The __native file sharing protocol__ for __UNIX/Linux__ is called the __Network File System (NFS)__.
- NFS is usually part of the kernel which means that a remote file system can be mounted (made accessible) just like a regular disk, making file access transparent to other applications.

- One of the oldest __network directory systems__ is the __Domain Name System (DNS)__. 
- It is used to __convert a name__ like __https://www.icann.org/__ to an __IP address__ like __192.0.43.7__, which is a unique identifier of a computer on the Internet.
-  DNS also holds global information like the __address of the MTA__ for a given domain name.
- The __Internet Software Consortium__ maintains the most popular __DNS server__, simply called bind after the name of the process that runs the service.

- The DNS is focused mainly on computer names and IP addresses and is not easily searchable. 

- The __Lightweight Directory Access Protocol (LDAP)__ is one common directory system which also powers __Microsoft’s Active Directory__.
- In __LDAP__, an object is __stored in a tree__, and the position of that object on the tree can be used to derive information about the object and what it stores. 
- For example, a Linux administrator may be stored in a branch of the tree called “IT Department,” which is under a branch called “Operations.” Thus one can find all the technical staff by searching under the “IT Department” branch. 

- __OpenLDAP__ is the dominant program used in __Linux infrastructure__.


- Another network infrastructure is __Dynamic Host Configuration Protocol (DHCP)__
- When a computer __boots up__, it needs an __IP address__ for the local network so it can be uniquely identified.
- __DHCP’s job__ is to __listen for requests__ and to __assign a free address from the DHCP pool__.
- The __Internet Software Consortium__ also maintains the ISC DHCP server, which is the most common open source DHCP server.


# Ch-5/Command Line Skills

## `History`

When a command is executed in the terminal, it is stored in a history list.

```
sysadmin@localhost:~$ date                                       
Wed Dec 12 04:28:12 UTC 2018                                   
sysadmin@localhost:~$ ls                                           
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos       
sysadmin@localhost:~$ cal 5 2030                                  
     May 2030                                                                  
Su Mo Tu We Th Fr Sa                                                            
          1  2  3  4                                                            
 5  6  7  8  9 10 11                                                            
12 13 14 15 16 17 18                                                            
19 20 21 22 23 24 25                                                            
26 27 28 29 30 31                                                               
sysadmin@localhost:~$ history                                   
    1  date                                                       
    2  ls                                                      
    3  cal 5 2030                                             
    4  history    
```
- If the desired command is in the list that the __history command__ generates, it can be executed by typing an __exclamation point `!` character__ and then the __number next to the command__, for example, to execute the `cal` command again:
```
sysadmin@localhost:~$ history                                     
    1  date                                                      
    2  ls                                                         
    3  cal 5 2030                                                 
    4  history                                                    
sysadmin@localhost:~$ !3                                        
cal 5 2030                                                        
     May 2030                                                                  
Su Mo Tu We Th Fr Sa                                                            
          1  2  3  4                                                            
 5  6  7  8  9 10 11                                                            
12 13 14 15 16 17 18                                                            
19 20 21 22 23 24 25   
```
- If the __history command__ is passed __a number as an argument__, it outputs that number of previous commands from the history list.
```
sysadmin@localhost:~$ history 3
    6  date                                                                     
    7  ls /home                                                                   
    8  history 3
```
- To execute the __nth command from the bottom of the history list__, type `!-n` and hit Enter.
```
sysadmin@localhost:~$ !-3                                                       
date                                                                            
Wed Dec 12 04:31:55 UTC 2018 
```
- To execute the __most recent command__ type `!!` and hit Enter:
```
sysadmin@localhost:~$ date                                                      
Wed Dec 12 04:32:36 UTC 2018                                                    
sysadmin@localhost:~$ !!                                                        
date
Wed Dec 12 04:32:38 UTC 2018
```
- To execute the __most recent iteration of a specific command__, type `! followed by the name of the command` and hit Enter.
```
sysadmin@localhost:~$ !ls                                                       
ls /home                                                                        
sysadmin 
```
## Local Variables

- __Local varibales__ exist only in the curent shell, and cannot affecet other commands or applications. When the user clises a terminal window or shell, all if the variables are lost.
- They are often associated with use-based taskes and are lowercase by convention.

- If the variable already exists, the value of the variable is modified.
- If the variable name does not exist, the shell creates a new local variable and sets the value:

`variable=value`
Example:

`sysadmin@localhost:~$ variable1='Something'`

- The `echo` command is used to __display output__ in the terminal.
- Use a __dollar sign `$`__ character _followed by the variable name_ as an argument to the echo command:
```
sysadmin@localhost:~$ echo $variable1                                   
Something
```
## Environment Variables

- __Environment variables__, also called __global variables__, are available system-wide, in all shells used by Bash when interpreting commands and performing tasks.
- The system automatically recreates environment variables when a new shell is opened. Examples include the __PATH__, __HOME__, and __HISTSIZE__ variables.
- The command in the example below displays the value of the HISTSIZE variable:
```
sysadmin@localhost:~$ echo $HISTSIZE
1000
```
- To modify the value of an existing variable, use the assignment expression:
```
sysadmin@localhost:~$ HISTSIZE=500                                            
sysadmin@localhost:~$ echo $HISTSIZE                              
500 
```
- When run without arguments, the `env` command outputs a list of the __environment variables__. Because the output of the `env` command can be quite long, the following examples use a text search to filter that output.
`sysadmin@localhost:~$ env | grep variable1  `
- In a previous example __variable1__ was created as a __local variable__, so the following search in the environment variables results in __no output__:

- The `export` command is used to __turn a local variable__ into __an environment variable__.

- After exporting variable1, it is now an environment variable. It is now found in the search through the environment variables:
```
sysadmin@localhost:~$ export variable1                                  
sysadmin@localhost:~$ env | grep variable1
variable1=Something
```
- The `export` command can also be used to make a variable an environment variable upon its creation by using the __assignment expression__ as the argument: 
```
sysadmin@localhost:~$ export variable2='Else'                           
sysadmin@localhost:~$ env | grep variable2                             
variable2=Else
```
- To change the value of an environment variable, use the assignment expression:```
sysadmin@localhost:~$ variable1=$variable1' '$variable2                
sysadmin@localhost:~$ echo $variable1                                   
Something Else
```
- Exported variables can be __removed__ using the `unset` command:
`sysadmin@localhost:~$ unset variable2`

## Path Variable

- One of the most __important Bash shell variables__ to understand is the __PATH__ variable. 
- It __contains a list__ that defines which directories the shell __looks in to find commands__. 
- If a valid command is entered and the shell returns a __"command not found"__ error, it is because the __Bash shell was unable to locate a command__ by that name in any of the directories included in the path. 

- This displays the path of the current shell:
```
sysadmin@localhost:~$ echo $PATH                                        
/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
sysadmin@localhost:~$
```
- If custom software is installed on the system it may be necessary to __modify the PATH__ to make it easier to execute these commands. 
- For example, the following will add and verify the `/usr/bin/custom` directory to the __PATH variable__:
```
sysadmin@localhost:~$ PATH=/usr/bin/custom:$PATH                                
sysadmin@localhost:~$ echo $PATH                                                
/usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr
/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin 
```
- One way to __learn more about a command__ is to look at where it comes from. 
- The `type` command can be used to determine information about command type. 

## External Commands

- External commands are stored in files that are searched by the shell. 
- If a user types the `ls` command, then the shell searches through the directories that are listed in the __PATH variable__ to try to find a file named `l`s that it can execute.
- If a command does not behave as expected or if a command is not accessible that should be, it can be beneficial to know where the shell is finding the command by using `which` command. 
```
sysadmin@localhost:~$ which ls                                       
/bin/ls                                                               
sysadmin@localhost:~$ which cal                                        
/usr/bin/cal
```
- External commands can also be executed by typing the complete path to the command. For example, to execute the `ls` command:
```
sysadmin@localhost:~$ /bin/ls                                                   
Desktop    Downloads  Pictures  Templates  calender_2030.txt                    
Documents  Music      Public    Videos 
```
- For __external commands__, the `type` command displays the __location of the command__:
```
sysadmin@localhost:~$ type cal                                      
cal is /usr/bin/cal
```
- In some cases the __output__ of the `type` command __may differ significantly__ from the output of the `which` command:
```
sysadmin@localhost:~$ type echo                                     
echo is a shell builtin
sysadmin@localhost:~$ which echo                                        
/bin/echo
```
- Using the `-a` option of the `type` command __displays all locations__ that contain the command named:
```
sysadmin@localhost:~$ type -a echo                                      
echo is a shell builtin                                                
echo is /bin/echo
```
## Aliases

- An __alias__ can be used to __map longer commands__ to __shorter key sequences__.

- To see what aliases are set in the current shell:
```
sysadmin@localhost:~$ alias                                                     
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo
 error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'
')"'                                                                            
alias egrep='egrep --color=auto'                                                
alias fgrep='fgrep --color=auto'                                                
alias grep='grep --color=auto'                                                  
alias l='ls -CF'                                                                
alias la='ls -A'                                                                
alias ll='ls -alF'                                                              
alias ls='ls --color=auto' 
```
- __New aliases can be created__ using the following format, where __name__ is the name to be given the alias and __command__ is the command to be executed when the alias is run.
`alias name=command`
Example:
```
sysadmin@localhost:~$ alias mycal="cal 3 2025"                                  
sysadmin@localhost:~$ mycal                                                     
     March 2025                                                                 
Su Mo Tu We Th Fr Sa                                                            
                   1                                                            
 2  3  4  5  6  7  8                                                            
 9 10 11 12 13 14 15                                                            
16 17 18 19 20 21 22                                                            
23 24 25 26 27 28 29                                                            
30 31 
```
- Once the shell is closed, the new aliases are lost.
- The `type` command can __identify aliases__ to other commands:
```
sysadmin@localhost:~$ type mycal                                                
mycal is aliased to `cal 3 2025'                                                
sysadmin@localhost:~$ type la                                                   
la is aliased to `ls -A'  
```
- __Aliases__ and __functions__ are normally loaded from the initialization files when the shell first starts.

## Double Quotes

- __Double quotes__ stop the shell from interpreting some __metacharacters (special characters)__, including __glob characters__.
- __NOTE__ that __Glob characters__, also called __wild cards__, are symbols that have special meaning to the shell; they are interpreted by the shell itself before it attempts to run any command. __Glob characters include__ the __asterisk *__ character, the __question ? mark__ character, and the __brackets [ ]__, among others.

- In the `echo` command below, the Bash shell doesn't convert the __glob pattern__ into filenames that match the pattern:
```
sysadmin@localhost:~$ echo "The glob characters are *, ? and [ ]"      
The glob characters are *, ? and [ ]
```
- __Double quotes__ still allow for __command substitution__, __variable substitution__, and __permit some other shell metacharacters__
- The following demonstration shows that the __value of the PATH variable__ is still displayed:
```
sysadmin@localhost:~$ echo "The path is $PATH"                          
The path is /usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
```
- __Double quote__ characters will have an __effect on wildcard__ characters, disabling their special meaning. Execute the following:
```
sysadmin@localhost:~$ echo D*                                        
Desktop Documents Downloads                                          
sysadmin@localhost:~$ echo "D*"                                      
D*     
```


## Single Quotes

- __Single quotes__ also prevent the shell from doing any interpreting of __special characters__, including __globs__, __variables__, __command substitution__ and other metacharacters

- For example, to make the __$ character__ simply mean a __$__, rather than it acting as an indicator to the shell to look for the value of a variable, execute the second command displayed below:
```
sysadmin@localhost:~$ echo The car costs $100                           
The car costs 00                                                        
sysadmin@localhost:~$ echo 'The car costs $100'                        
The car costs $100
```
## Backslash Character

- There is also an __alternative technique__ to essentially __single quote a single character__. Consider the following message: 
`The service costs $1 and the path is $PATH`

- If this sentence is placed in __double quotes__, __$1__ and __$PATH__ are considered __variables__.
```
sysadmin@localhost:~$ echo "The service costs $1 and the path is $PATH"

The service costs  and the path is /usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games 
```
- If it is placed in __single quotes__, __$1__ and __$PATH__ are __not considered variables__.
```
sysadmin@localhost:~$ echo 'The service costs $1 and the path is $PATH' 
The service costs $1 and the path is $PATH 
```
- But __what if__ you want to have __$PATH treated as a variable__ and __$1 not__?
- In this case, use a backslash \ character in front of the dollar sign $ character to prevent the shell from interpreting it.
```
sysadmin@localhost:~$ echo The service costs \$1 and the path is $PATH
The service costs $1 and the path is /usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
```
## Backquotes

- __Backquotes__, or __backticks__, are used to specify a __command within a command__, a process called __command substitution__. This allows for powerful and sophisticated use of commands. 

- An example should make things more clear:
- To begin, note the __output__ of the `date` command:
```
sysadmin@localhost:~$ date                                                      
Fri Jul  2 16:21:22 UTC 2021  
```
- Now, note the __output__ of the `echo` command:
```
sysadmin@localhost:~$ echo Today is date                               
Today is date
```
- In the __previous command__, the word __date__ is treated as __regular text__, and the shell passes date to the `echo` command. 
- To execute the `date` command and have the __output of that command__ sent to the `echo` command, put the `date` command in between __two backquote__ characters:
```
sysadmin@localhost:~$ echo Today is `date`                         
Today is Mon Nov 4 03:40:04 UTC 2018
```
- You can also place __$( before the command and )__ after the command to accomplish __command substitution__:
```
sysadmin@localhost:~$ echo Today is $(date)                                     
Today is Fri Jul 2 16:50:03 UTC 2021  
```
- If you __don't want the backquotes to be used to execute a command__, place __single quotes around them__. Execute the following:
```
sysadmin@localhost:~$ echo This is the command '`date`'                         
This is the command `date` 
```
- You could also __place a backslash character__ in front of each backquote character. Execute the following:
```
sysadmin@localhost:~$ echo This is the command \`date\`     
This is the command `date` 
```
- __Double quote__ characters __don't have any effect on backquote__ characters. 
```
sysadmin@localhost:~$ echo This is the command "`date`"                         
This is the command Fri Jul  2 16:53:34 UTC 2021 
```

## Control Statements

- Control statements __allow you to use multiple commands at once__ or __run additional commands__, depending on the success of a previous command.
- Typically these control statements are used within scripts, but they can also be used on the command line as well.
- The __Bash shell__ offers __three different statements__ that can be used to __separate multiple commands__ typed together.
1. The simplest separator is the semicolon (;).
2. The && characters create a logical "and" statement.
3. The || characters create a logical "or" statement, which also causes conditional execution.

## Semicolon

- The __semicolon ;__ character can be used to __run multiple commands__, __one after the other__. 
- __Each command runs independently and consecutively__; regardless of the result of the first command, the second command runs once the first has completed, then the third and so on.

## Double Ampersand

- The __double ampersand &&__ acts as a __logical "and"__; if the first command is successful, then the second command will also run. If the first command fails, then the second command will not run.

```
sysadmin@localhost:~$ ls /etc/ppp && echo success          
ip-down.d  ip-up.d        
success  

sysadmin@localhost:~$ ls /etc/junk && echo success          
ls: cannot access /etc/junk: No such file or directory
```
## Double Pipe

- The __double pipe ||__ is a __logical "or"__. Depending on the result of the first command, the second command will either run or be skipped.
```
sysadmin@localhost:~$ ls /etc/ppp || echo failed                 
ip-down.d  ip-up.d              
sysadmin@localhost:~$ ls /etc/junk || echo failed                  
ls: cannot access /etc/junk: No such file or directory             
failed
```


