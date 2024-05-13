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


