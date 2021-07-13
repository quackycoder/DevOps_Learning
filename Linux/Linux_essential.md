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

# Ch-7/Navigating the Filesystem

- __Colored output__ is __not the default behavior__ for the `ls` command, but rather the effect of the `--color` option.
- The `ls` seems to perform this coloring automatically because there is an __alias__ for the `ls` command, so it runs with the `--color` option.
-To avoid using the __alias__, place a __backslash character \__ in front of your command:
```
sysadmin@localhost:~$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos 
sysadmin@localhost:~$ \ls
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
```
- To display all files, including __hidden files__, use the `-a` option to the `ls` command:
```
sysadmin@localhost:~$ ls -a                                            
.             .bashrc   .selected_editor  Downloads  Public           
..            .cache    Desktop           Music      Templates         
.bash_logout  .profile  Documents         Pictures   Videos
```
- Why are files hidden in the first place? Most of the hidden files are customization files, designed to customize how Linux, your shell or programs work. 
- For example, the .bashrc file in the home directory customizes features of the shell, such as creating or modifying variables and aliases.

- To __sort files by size__, we can use the `-S` option.
```
sysadmin@localhost:~$ ls -S /etc/ssh
moduli            ssh_host_ed25519_key  ssh_host_ecdsa_key.pub
sshd_config       ssh_host_rsa_key.pub  ssh_host_ed25519_key.pub
```
- While the `-S` option works by itself, it is most useful when used with the `-l` option so the file sizes are visible.
```
sysadmin@localhost:~$ ls -lS /etc/ssh
total 580
-rw-r--r-- 1 root root 553122 Feb 10  2018 moduli
-rw-r--r-- 1 root root   3264 Feb 10  2018 sshd_config
-rw------- 1 root root   1679 Jul 19 06:52 ssh_host_rsa_key
-rw-r--r-- 1 root root   1580 Feb 10  2018 ssh_config
```
- It may also be useful to use the `-h` option to display __human-readable file sizes__:
```
sysadmin@localhost:~$ ls -lSh /etc/ssh                                
total 580K                                                                      
-rw-r--r-- 1 root root 541K Feb 10  2018 moduli
-rw-r--r-- 1 root root 3.2K Feb 10  2018 sshd_config
-rw------- 1 root root 1.7K Jul 19 06:52 ssh_host_rsa_key
-rw-r--r-- 1 root root 1.6K Feb 10  2018 ssh_config
```
- The `-t` option __sorts files based on the time they were modified__.
```
sysadmin@localhost:~$ ls -tl /etc/ssh                                 
total 580
-rw------- 1 root root    227 Jul 19 06:52 ssh_host_ecdsa_key
-rw-r--r-- 1 root root    179 Jul 19 06:52 ssh_host_ecdsa_key.pub
-rw------- 1 root root    411 Jul 19 06:52 ssh_host_ed25519_key
```
- If the files in a directory were modified many days or months ago, it may be harder to tell exactly when they were modified, as only the date is provided for older files.
- For more detailed modification time information you can use the `--full-time` option to display the __complete timestamp (including hours, minutes, seconds)__.
```
sysadmin@localhost:~$ ls -t --full-time /etc/ssh
total 580
-rw------- 1 root root    227 2018-07-19 06:52:16.000000000 +0000 ssh_host_ecdsa_key
-rw-r--r-- 1 root root    179 2018-07-19 06:52:16.000000000 +0000 ssh_host_ecdsa_key.pub
-rw------- 1 root root    411 2018-07-19 06:52:16.000000000 +0000 ssh
```
- It is possible to perform a __reverse sort__ by using the `-r` option. 
```
sysadmin@localhost:~$ ls -lrS /etc/ssh
total 580
-rw-r--r-- 1 root root     99 Jul 19 06:52 ssh_host_ed25519_key.pub
-rw-r--r-- 1 root root    179 Jul 19 06:52 ssh_host_ecdsa_key.pub
-rw------- 1 root root    227 Jul 19 06:52 ssh_host_ecdsa_key
```
- The following command will list files by __modification date, oldest to newest__:
```
sysadmin@localhost:~$ ls -lrt /etc/ssh                                 
total 580
-rw-r--r-- 1 root root   3264 Feb 10  2018 sshd_config
-rw-r--r-- 1 root root   1580 Feb 10  2018 ssh_config
-rw-r--r-- 1 root root 553122 Feb 10  2018 moduli
```
# Ch-8/Managing Files and Directories

- When the `ls` command sees a filename as an argument, it just displays the __filename__. However, __for any directory__, it displays the __contents of the directory__, not just the directory name.
- This becomes even more confusing in a situation like the following:
```
sysadmin@localhost:~$ ls /etc/x*                                                
autostart  systemd  user-dirs.conf  user-dirs.defaults 
```
- In the previous example, it seems like the `ls` command is just plain wrong. However, what really happened is that __the only thing that matches the glob__ `/etc/x*` is the `/etc/xdg` directory. 
- So, the `ls` command only displayed the files in that directory!
- There is a simple solution to this problem: __always use__ the `-d` option __with globs__, which tells the `ls` command to display the name of directories, instead of their contents:
```
sysadmin@localhost:~$ls -d /etc/x*                                             
/etc/xdg
```

- Like the `cp` command, the `mv` command provides the following options:
| --- | --- |
| __Option__ | __Meaning__ |
| __-i__ |  Interactive: Ask if a file is to be overwritten. |
| __-n__ |  No Clobber: Do not overwrite a destination file's contents. |
| __-v__ |  Verbose: Show the resulting move. |

- __Important__: There is __no__ `-r` option as the `mv` command moves directories by default.

- Enter the following commands to __copy from the source directory and preserve file attributes(date and permission modes)__ by using the `-p` option:
```
sysadmin@localhost:~$ rm hosts 
sysadmin@localhost:~$ ls                                                 
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos     
sysadmin@localhost:~$ cd /etc                                                 
sysadmin@localhost:/etc$ ls -l hosts                                          
-rw-r--r-- 1 root root 150 Jan 22 15:18 hosts                                 
sysadmin@localhost:/etc$ cp -p hosts /home/sysadmin                           
sysadmin@localhost:/etc$ cd                                                   
sysadmin@localhost:~$ ls -l hosts                                             
-rw-r--r-- 1 sysadmin sysadmin 150 Jan 22 15:18 hosts                         
sysadmin@localhost:~$
```
- Type the following commands to copy using a different target name:
```
rm  hosts				
cp -p /etc/hosts ~			
cp hosts newname			
ls –l hosts newname
rm hosts newname
```
- The first copy with the `-p` option __preserved the original timestamp__. Recall that the __tilde ~__ represents your __home directory (/home/sysadmin)__.
- The second copy specified a different filename (newname) as the target. Because it was issued without the `-p` option, the system used the current date and time for the target; thus, it did not preserve the original timestamp found in the source file `/etc/hosts`.
- Finally, note that you can remove more than one file at a time as shown in the last rm command.

- To __copy all files in a directory__, use the `-R` option. 
```
mkdir Myetc
cp –R /etc/udev Myetc
ls –l Myetc
ls –lR Myetc
```
# Ch-9/Archiving and Compression

- Linux provides several tools to __compress files__; the most common is __gzip__. Here we show a file before and after compression:
```
sysadmin@localhost:~$ cd Documents
sysadmin@localhost:~/Documents$ ls -l longfile*
-rw-r--r-- 1 sysadmin sysadmin 66540 Dec 20  2017 longfile.txt
sysadmin@localhost:~/Documents$ gzip longfile.txt
sysadmin@localhost:~/Documents$ ls -l longfile*
-rw-r--r-- 1 sysadmin sysadmin 341 Dec 20  2017 longfile.txt.gz
```
- The __`gzip`__ command will provide this information, by using the `–l` option, as shown here:
```
sysadmin@localhost:~/Documents$ gzip -l longfile.txt.gz
         compressed        uncompressed  ratio uncompressed_name
                341               66540  99.5% longfile.txt
```
- __Compressed files can be restored__ to their original form using either the `gunzip` command or the `gzip –d` command. This process is called __decompression__.
```
sysadmin@localhost:~/Documents$ gunzip longfile.txt.gz
sysadmin@localhost:~/Documents$ ls -l longfile*
-rw-r--r-- 1 sysadmin sysadmin 66540 Dec 20  2017 longfile.txt
```
- The `gunzip` command is __just a script__ that calls `gzip` with the right parameters.

- There is __`bzip2`__ and __`bunzip2`__, as well as __`xz`__ and __`unxz`__.

- The `gzip` command uses the __Lempel-Ziv data compression algorithm__, while the `bzip` utilities use a different compression algorithm called __Burrows-Wheeler block sorting__, which can __compress files smaller than gzip at the expense of more CPU time__. These files can be recognized because they have a __.bz__ or __.bz2__ extension instead of a __.gz__ extension.

- The `xz` and `unxz` tools are functionally similar to `gzip` and `gunzip` in that they use the __Lempel-Ziv-Markov (LZMA) chain algorithm__, which can result in __lower decompression CPU times__ that are on par with gzip while providing the __better compression ratios__ typically associated with the `bzip2` tools. Files compressed with the `xz` command use the `.xz` extension.

- If you had several files to send to someone, you could choose to compress each one individually. You would have a smaller amount of data in total than if you sent uncompressed files, however, you would still have to deal with many files at one time.
- __Archiving__ is the solution to this problem. The traditional UNIX utility to archive files is called __tar__, which is a short form of __TApe aRchive__.
- It was used to stream many files to a tape for backups or file transfer. 
- The `tar` command takes in __several files__ and creates a __single output file__ that can be split up again into the original files on the other end of the transmission.
- The tar command has three modes that are helpful to become familiar with:

  - __Create__: Make a new archive out of a series of files.  - __Extract__: Pull one or more files out of an archive.
  - __List__: Show the contents of the archive without extracting.

`tar -c [-f ARCHIVE] [OPTIONS] [FILE...]`
- `-c`-- Create an archive.
 
- `-f ARCHIVE` Use archive file.The argument ARCHIVE will be the name of the resulting archive file.
 
- The following example shows a tar file, also called a __tarball__, being created from multiple files.
```
sysadmin@localhost:~/Documents$ tar -cf alpha_files.tar alpha*
sysadmin@localhost:~/Documents$ ls -l alpha_files.tar
-rw-rw-r-- 1 sysadmin sysadmin 10240 Oct 31 17:07 alpha_files.tar
```
- Normally, __tarball files__ are __slightly larger than the combined input files__ due to the overhead information on recreating the original files. 
- Tarballs can be compressed for easier transport, either by using `gzip` on the archive or by having tar do it with the `-z` option.
```
sysadmin@localhost:~/Documents$ tar -czf alpha_files.tar.gz alpha*
sysadmin@localhost:~/Documents$ ls -l alpha_files.tar.gz
-rw-rw-r-- 1 sysadmin sysadmin 417 Oct 31 17:15 alpha_files.tar.gz
```
- The `bzip2` compression can be used instead of `gzip` by substituting the `-j` option for the `-z` option and using `.tar.bz2`, `.tbz`, or `.tbz2` as the file extension. 
` sysadmin@localhost:~/Documents$ tar -cjf folders.tbz School`

- Given a __tar archive__, compressed or not, you can see what’s in it by using the `-t` option. The next example uses three options:
`tar -t [-f ARCHIVE] [OPTIONS]`
- `-t`-- List the files in an archive.
- `-j`-- Decompress with an bzip2 command.
- `-f ARCHIVE`-- Operate on the given archive. 
```
sysadmin@localhost:~/Documents$ tar -tjf folders.tbz
School/
School/Engineering/
School/Engineering/hello.sh
School/Art/
```
- We will __list the contents of the file__ in two steps using a __pipeline, the |__ character.
```
sysadmin@localhost:~/Documents$ bunzip2 -c folders.tbz | tar -t
School/
School/Engineering/
School/Engineering/hello.sh
School/Art/
```
- `bunzip2 –c folders.tbz`, which __decompresses the file__, but the `-c` option __sends the output to the screen__.

- Extracting tarball or tar compressed file.
`tar -x [-f ARCHIVE] [OPTIONS]`

- `-x`--  Extract files from an archive.
- `-j`-- Decompress with the bzip2 command.
- `-f ARCHIVE`-- Operate on the given archive.
- `-v`-- Verbosely list the files processed.
```
sysadmin@localhost:~/Downloads$ tar -xjf folders.tbz
sysadmin@localhost:~/Downloads$ ls -l
total 8
drwx------ 5 sysadmin sysadmin 4096 Dec 20  2017 School
-rw-rw-r-- 1 sysadmin sysadmin  413 Oct 31 18:37 folders.tbz
```
- It is important to keep the `–f` flag __at the end__, as __tar__ assumes whatever follows this option is a __file name__. In the next example, the `–f` and `–v` flags were transposed, leading to tar interpreting the command as an operation on a file called `v`, which __does not exist__.
```
sysadmin@localhost:~/Downloads$ tar -xjfv folders.tbz 
tar (child): v: Cannot open: No such file or directory
tar (child): Error is not recoverable: exiting now
tar: Child returned status 2
tar: Error is not recoverable: exiting now
```
- If you only want some files out of the archive, add their names to the end of the command, but by default, they must match the name in the archive exactly, or use a pattern. 
```
sysadmin@localhost:~/Downloads$ tar -xjvf folders.tbz School/Art/linux.txt
School/Art/linux.txt
```
- If you want __tar like behavior__ in `zip` command, you must use the `–r` option to indicate recursion is to be used:
```
sysadmin@localhost:~/Documents$ zip -r School.zip School
updating: School/ (stored 0%)
updating: School/Engineering/ (stored 0%)
```
- The `–l` list option of the `unzip` command lists files in `.zip` archives:

# Ch-10/Working With Text

- The `-n` option can also be used to indicate __how many lines to output__.
```
sysadmin@localhost:~$ head -n 3 /etc/sysctl.conf
#
# /etc/sysctl.conf - Configuration file for setting system variables
# See /etc/sysctl.d/ for additional system variables
```

- Traditionally in UNIX, the number of lines to output would be specified as an option with either command, so `-3` meant to show __three lines__. For the `tail` command, either `-3` or `-n -3` still means show __three lines__.

- However, the GNU version of the `head` command recognizes `-n -3` as show all but the last three lines, and yet the `head` command still recognizes the option `-3` as show the __first three lines__.

- If the `-n` option is used with a number __prefixed by the plus sign__, then the `tail` command recognizes this to mean to display the contents starting at the __specified line__ and continuing __all the way to the end__.
```
sysadmin@localhost:~$ nl /etc/passwd | tail -n +25
    25  sshd:x:103:65534::/var/run/sshd:/usr/sbin/nologin
    26  operator:x:1000:37::/root:/bin/sh
    27  sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```
## IMPORTANT

- __Live file__ changes can be viewed by using the `-f` option to the `tail` command—useful when you want to see changes to a file as they are happening.

- A good example of this would be when __viewing log files__ as a system administrator. Log files can be used to troubleshoot problems and administrators often view them "interactively" with the `tail` command while performing commands in a separate window. 
- For example, if you were to log in as the root user, you could troubleshoot issues with the email server by viewing live changes to the /var/log/mail.log log file. 

- The `sort` command can rearrange the output based on the contents of one or more fields. Fields are determined by a field delimiter contained on each line.

- The following command can be used to sort the third field of the mypasswd file numerically. Three options are used to achieve this sort:
```
sysadmin@localhost:~$ sort -t: -n -k3 mypasswd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
```
- __`-t:`__ -- The -t option specifies the field delimiter. If the file or input is separated by a delimiter other than whitespace, for example a comma or colon, the -t option will allow for another field separator to be specified as an argument.

The mypasswd file used in the previous example uses a colon : character as a delimiter to separate the fields, so the following example uses the -t: option.

- __`-k3`__ -- The -k option specifies the field number. To specify which field to sort by, use the -k option with an argument to indicate the field number, starting with 1 for the first field.

The following example uses the -k3 option to sort by the third field.

- __`-n`__ -- This option specifies the sort type.

The third field in the mypasswd file contains numbers, so the -n option is used to perform a numeric sort.

- Another commonly used option to the `sort` command is the `-r` option, which is used to perform a __reverse sort__.
```
sysadmin@localhost:~$ sort -t: -n -r -k3 mypasswd
sync:x:4:65534:sync:/bin:/bin/sync 
sys:x:3:3:sys:/dev:/usr/sbin/nologin  
bin:x:2:2:bin:/bin:/usr/sbin/nologin  
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
root:x:0:0:root:/root:/bin/bash    
```
- To sort first by the operating system (field #2) and then year (field #1) and then by last name (field #3), use the following command:
```
sysadmin@localhost:~/Documents$ sort -t, -k2 -k1n -k3 os.csv
1991,Linux,Torvalds
1987,Minix,Tanenbaum
1970,Unix,Richie
1970,Unix,Thompson
```
- The following table breaks down the options used in the previous example:
| --- | --- |
| Option | Function |
| __-t,__ | Specifies the comma character as the field delimiter |
| __-k2__ | Sort by field #2 |
| __-k1n__ | Numerically sort by field #1 |
| __-k3__ | Sort by field #3 |


- The `cut` command can __extract columns of text from a file__ or __standard input__. It’s primarily used for working with __delimited database files__.

- __By default__, the `cut` command expects its input to be __separated by the tab__ character, but the `-d` option can specify alternative delimiters such as the __colon__ or __comma__.

- The `-f` option can specify __which fields to display__, either as a __hyphenated range__ or a __comma-separated list__.

- In the following example, the first, fifth, sixth and seventh fields from the mypasswd database file are displayed:
```
sysadmin@localhost:~$ cut -d: -f1,5-7 mypasswd
root:root:/root:/bin/bash
daemon:daemon:/usr/sbin:/usr/sbin/nologin
bin:bin:/bin:/usr/sbin/nologin
sys:sys:/dev:/usr/sbin/nologin
sync:sync:/bin:/bin/sync
```
- The `cut` command is also able to __extract columns of text__ based upon character position with the `-c` option—useful when working with fixed-width database files or command outputs.

- For example, the fields of the ls -l command are always in the same character positions. The following will display just the file type (character 1), permissions (characters 2-10), a space (character 11), and filename (characters 50+):
```
sysadmin@localhost:~$ ls -l | cut -c1-11,50-
total 44
drwxr-xr-x Desktop
drwxr-xr-x Documents
drwxr-xr-x Downloads
drwxr-xr-x Music
drwxr-xr-x Pictures
```

- The `-c` option provides a count of how many lines match:
```
sysadmin@localhost:~$ grep -c bash /etc/passwd
2
```
- The `-n` option to the `grep` command will display __original line numbers__. To display all lines and their line numbers in the `/etc/passwd` file which contain the pattern bash:
```
sysadmin@localhost:~$ grep -n bash /etc/passwd                          
1:root:x:0:0:root:/root:/bin/bash                                       
27:sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```
- The `-v` option __inverts the match__, outputting __all lines that do not contain the pattern__. To display all lines not containing nologin in the `/etc/passwd` file:
```
sysadmin@localhost:~$ grep -v nologin /etc/passwd
root:x:0:0:root:/root:/bin/bash
sync:x:4:65534:sync:/bin:/bin/sync
operator:x:1000:37::/root:/bin/sh
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```
- The `-i` option __ignores the case__ (capitalization) distinctions.
```
sysadmin@localhost:~/Documents$ grep -i the newhome.txt
There are three bathrooms.
**Beware** of the ghost in the bedroom.
The kitchen is open for entertaining.
**Caution** the spirits don't like guests.
```
- The `-w` option only __returns lines__ which contain __matches that form whole words__.
```
sysadmin@localhost:~/Documents$ grep are newhome.txt
There are three bathrooms.
**Beware** of the ghost in the bedroom.
sysadmin@localhost:~/Documents$ grep -w are newhome.txt
There are three bathrooms.
```
- Use the `-E` switch to allow `grep` to operate in __extended mode__ in order to recognize the alternation operator:
```
sysadmin@localhost:/etc$ grep -E 'sshd|root|operator' passwd                  
root:x:0:0:root:/root:/bin/bash                                               
sshd:x:103:65534::/var/run/sshd:/usr/sbin/nologin                             
operator:x:1000:37::/root:/bin/sh 
```
- Suppose you want to search for a pattern containing a __sequence of three digits__. You can use __{ }__ characters with a number to express that you want to repeat a pattern a specific number of times; for example: {3}. The use of the numeric qualifier requires the extended mode of `grep`:
```
sysadmin@localhost:/etc$ grep -E '[0-9]{3}' passwd                              
sync:x:4:65534:sync:/bin:/bin/sync                                              
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin                      
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin                                
systemd-network:x:101:102:systemd Network Management,,,:/run/systemd/netif:/usr/
sbin/nologin              
```


