# Bash Notes

Linux codes and commands:

```
ls -latr
```

```
ls -latp
```

```
ls -al #This will show hidden files 
```

```
cd 
```

```
sudo
```

```
sudo lso -c cron 
```

```
lsof breakdown for cron
```

```
lsod -i :123 mach with ip find in netstat breakout earlier
```

```
establish persistance /etc.inittab or crontab
```

```
man #Manual with information about commands.
```

```
cat /etc/passwd
```



## Create a file: 


```
touch -t yymmddhhmm.ss #Will make a file, with arguments will create a file with a certain timestamp 
```

```
mkdir -p #Will make a dir, with arguments will make a dir with nested directories on it.
```
cut -d: -f1- -s fakepasswd.txt

```
chmod 777
```

```
umask
```

```
rm -rf #To force removal
```

```
rmdir #Remove dir
```

```
rm -r #removes a nested directory
```

```
ls~/*.log #Shows all the files with log on it------------------------------------------------------------------------------
```

## Move a file:

```
mv <source> <destination> #Moves a file from source to destination
```

Difference in between hard and symbolic links?---------------------------------------------------------------------------------


## Head more, less tail 

```
more

```

```
less
```

```
head
```

```
tail
```

## Will locate a certain string:

```
find | grep <striing>-----------------------------------------------------------------------------------------------------
```

## find a certain file:

```
whereis <string> #

```

```
find -name, -iname, -ilname, -inum, -size, -maxdepth #Name case sensitive, case non-sensitve, symbolic link, , size of the file----------
```

```
 find / -type---------------------------------------------------------------------------------------------------------------------
```

```
find -name/.txt--------------------------------------------------------------------------------------------------------------------
```
## Find modified files within a certain timestamp:

```
find -cmin -30 #Find everything that was changed within the last 30 minutes
```

```
find /var/log/ -iname *.log -exec ls -al {} 2>/dev/null \;-------------------------------------------------------------------------


```
01 - BASH Activity
1
coding bash
Brace expansion is a mechanism by which arbitrary strings may be generated, for commands that will take multiple arguements. For the below examples, the first example is equivalent to the second command.

$ mkdir /var/log/{auth,syslog,dmesg}_log

Results in

$ mkdir /var/log/auth_log /var/log/syslog_log /var/log/dmesg_log

Activity: Using Brace-Expansion, create the following directories within the $HOME directory:

1123
1134
1145
1156
To read more on Brace Expansion, go to the following resource:

https://www.gnu.org/software/bash/manual/bash.html#Brace-Expansion



```
mkdir {1123,1134,1145,1156}
```

01.2 - BASH Activity
1
coding bash
As we learned, the following example would create five files with one command.

touch file1.txt file2.txt file3.txt passwd.txt shadow.txt

But, with Brace Expansion it can be shortened to the following.

touch file{1..3}.txt passwd.txt shadow.txt

Activity:

Use Brace-Expansion to create the following files within the $HOME/1123 directory. You may need to create the $HOME/1123 directory. Make the following files, but utilze Brace Expansion to make all nine files with one touch command.

Files to create:

1.txt
2.txt
3.txt
4.txt
5.txt
6~.txt
7~.txt
8~.txt
9~.txt

```
mkdir 1123
cd 1123
touch {1,2,3,4,5}.txt {6~,7~,8~,9~}.txt
```

01.3 - BASH Activity
1
coding bash
Activity:

Using the find command, list all files in $HOME/1123 that end in .txt.

Be aware that if you use Pattern Matching to locate the files you may have unintended results based on if you use quotes around the pattern or not. If you do not quote the pattern, the Bash shell interprets the pattern. If you quote the pattern, it is passed to the command for it to interpret. You can have a properly functioning command, yet unintended output, based on which of these two gets to interpret the pattern.

To read more on Pattern Matching, go to the following resource:

https://www.gnu.org/software/bash/manual/bash.html#Pattern-Matching
To read more on Quoting, go to the following resource:

https://www.gnu.org/software/bash/manual/bash.html#Quoting

```
find $HOME/1123 | grep .txt
```

01.3 Challenge - BASH Activity
1
coding bash
Challenge Activity:

List all files in $HOME/1123 that end in .txt. Omit the files containing a tilde (~) character.

While this activity can be accomplished with only find, it can also be combined with grep as well.

```
find $HOME/1123/*.txt | grep -v '~'
```
## Find files ended in .txt on a particular dir and disregard the ones ended in containing ~
then copy the .txt files to $HOME/CUT dir

Copy all files in the $HOME/1123 directory, that end in ".txt", and omit files containing a tilde "~" character, to directory $HOME/CUT.

Use only the find and cp commands. You will need to utilize the -exec option on find to accomplish this activity.

The find command uses BOOLEAN "!" to designate that it does not want to find any files or directories that follows.


```
find -path "$HOME/1123/*.txt"  ! -path "$HOME/1123/*~.txt" -exec cp {} $HOME/CUT \;
```

## Find all empty files/directories and print out the filename and inode number in diferent lines

Using ONLY the find command, find all empty files/directories in directory /var and print out ONLY the filename (not absolute path), and the inode number, separated by newlines.

Tip: When using the man pages, it is better to focus your search then to visually scan 1000+ lines of text. Combining the output with the grep command, possibly with its -A, -B, or -C options, can help drive context driven searches of those manual pages.

Example Output

123 file1
456 file2
789 file3

```
find /var -empty 2>/dev/null -printf "%i %f\n" 
```

## Find all files with a certain inode number (find -inode ####) and print their filename only (-printf "%f\n") in different lines.

Using ONLY the find command, find all files on the system with inode 4026532575 and print only the filename to the screen, not the absolute path to the file, separating each filename with a newline. Ensure unneeded output is not visible.

Tip: The above inode is specific to this CTFd question and might not be in use on your Linux Opstation. Instead, you can test your command on your Linux OpStation against inode 999.

```
find -inum 4026532575 -printf "%f\n"
```

## Find certain strings within a file 

```
cut -d: -f1 -s fakepasswd.txt
```

#Where -d is my delimiter, allows me to set a parameter that divides the text, -f1 will output only the information about the field 1 and -s will avoid outputing anything that does not comply with the delimiter.


## Find all files, disregard directories and move them to a different directory.

```
ls -p $HOME/CUT | grep -v / | grep /*.txt > $HOME/CUT/names
```
#Where $HOME/CUT is my current dir and $HOME/CUT/names is the dir to where I wanna write all my files.


## Same output only using ls and cut:

```
ls -l $HOME/CUT | cut -d. -f1- -s | cut -d: -f2 | cut -d" " -f2 > $HOME/CUT/names 

```

## Awk scripting language inside of a language, inception.

```
tail fakepasswd.txt | awk -F: '{print $1}'
```
#Will print everything in front of the : for tail fakepasswd and field 1, if we specify $1,$4 will print fields 1-4




## In between parenthesis () we introduce the if statement (if field 3 == 0) print field 1

```
awk -F: '($3 == 0) {print $1}' fakepasswd.txt
```
## $NF Field refers tp the last field 
```
awk -F: '($3 > 150) {print $1,$6,$3,$NF}' fakepasswd.txt 
```
#Will print fields 1,6,3 and last field 

## Sort

```
cat fakepasswd.txt | awk -F: '{print$3}' | sort -t:
```
## Sort, organize the results by numeric number present on field 2.

```
ps aux | sort -k 2
```

Using ONLY the awk command, write a BASH one-liner script that extracts ONLY the names of all the system and user accounts that are not UIDs 0-3.
Only display those that use /bin/bash as their default shell.
The input file is named $HOME/passwd and is located in the current directory.
Output the results to a file called $HOME/SED/names.txt
Tip: awk can use conditional statements, e.g. print only the line in /etc/passwd that has "root" as its first field.



```
awk -F: '($3 > 3 && $NF == "/bin/bash") {print $1}' passwd > SED/names.txt
```


