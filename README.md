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

Activity: Using Brace-Expansion, creatWrite a script that determines your default gateway ip address. Assign that address to a variable using command substitution.
NOTE: Networking on the CTFd is limited for security reasons. ip route and route are emulated. Use either of those with no switches.

Have your script determine the absolute path of the ping application. Assign the absolute path to a variable using command substitution.

Have your script send six ping packets to your default gateway, utilizing the path discovered in the previous step, and assign the response to a variable using command substitution.

Evaluate the response as being either successful or failure, and print an appropriate message to the screen.

dg=$(route | tail -2 | head -1 | cut -d" " -f2)
pr=$(whereis ping | cut -d" " -f2)
num=$($pr $dg -c 6 | tail -2 | head -1 | cut -d" " -f4)
if [[ $num == "0" ]]; then
echo "failure";
else
echo "successful";
fi
"RIGHT" Answer:

A=$(route | grep 'default.*[[:digit:]]' | awk '{print $2}')
B=$(which ping)
C=" 0% packet loss"
D=$($B -c 6 $A | grep -Eo "$C")
if [[ "$C" == "$D" ]]; then
echo "successful";
else
echo "failure";
fie the following directories within the $HOME directory:

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

#Where -d is my delimiter, allows me to set a parameter that divides the text, -f1 will output only the information about the field 1 and -s will avoid outputing anything that does not comply with the delimiter.Write a script that determines your default gateway ip address. Assign that address to a variable using command substitution.
NOTE: Networking on the CTFd is limited for security reasons. ip route and route are emulated. Use either of those with no switches.

Have your script determine the absolute path of the ping application. Assign the absolute path to a variable using command substitution.

Have your script send six ping packets to your default gateway, utilizing the path discovered in the previous step, and assign the response to a variable using command substitution.

Evaluate the response as being either successful or failure, and print an appropriate message to the screen.

dg=$(route | tail -2 | head -1 | cut -d" " -f2)
pr=$(whereis ping | cut -d" " -f2)
num=$($pr $dg -c 6 | tail -2 | head -1 | cut -d" " -f4)
if [[ $num == "0" ]]; then
echo "failure";
else
echo "successful";
fi
"RIGHT" Answer:

A=$(route | grep 'default.*[[:digit:]]' | awk '{print $2}')
B=$(which ping)
C=" 0% packet loss"
D=$($B -c 6 $A | grep -Eo "$C")
if [[ "$C" == "$D" ]]; then
echo "successful";
else
echo "failure";
fi


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


Find all dmesg kernel messages that contain CPU or BIOS (uppercase) in the string, but not usable or reserved (case-insensitive)
Print only the msg itself, omitting the bracketed numerical expressions ie: [1.132775]
Note: For security reasons, the dmesg command is being emulated on the CTFd backend. You can still use it as normal on your Linux OpStation, but to get a similar output, do not use any dmesg switches. The intent of this activity is to take raw dmesg output and combine it with grep and either awk or cut to manipulate the output into a desired end state.

Tip: As you may have noticed, when using grep you can simulate a logical AND by piping the output of one grep command to the next. This will filter down your output to only what contains all your patterns. But, for this activity, you will need to use a logical OR to match on a wide range of strings. If you do not recall how to utilize that option in grep, go research it from the resources available to you.


```
dmesg | grep "CPU\|BIOS" | grep -vi "usable\|reserved" | cut -d] -f2-
```

## sed command. 

```
sed -e 's/Chicken/Cheese/g' -e 's/Peppers/Jalapenos/' pizza.txt
```
#Where g is global sign so it will do the whole line, no g just the first string in that line 

### delete a string with sed.

```
sed -e '/Cheese/d'  pizza.txt 
```


13-Find all executable files under the following four directories:
/bin
/sbin
/usr/bin
/usr/sbin
Sort the filenames with absolute path, and get the md5sum of the 10th file from the top of the list.
Tip: In the below example, you can see the different uses of md5sum. While not wrong, the first command is hashing the string output of the the find command. In the second, md5sum is hashing the file contents of the given file, which is what is intended for this activity. You can also tell the second method hashed the file as the file name is listed in the hash output; the first only lists a hyphen indicating a string was hashed. For this activity, to provide md5sum with the 10th file of the sorted output, it is recommended to use Command Subtitution.


```
file=$1
name=$2
ugid=$3
base=$(tail -1 $file)
echo $base > myfile

awk -F: -v "awk_var1=$name" -v "awk_var2=$ugid" 'BEGIN {OFS=":"} {$1=awk_var1} {$3=awk_var2} {$4=awk_var2} {$6="/home/"awk_var1} {$7="/bin/bash"} {print}' myfile >> $file

```
14-Using any BASH command complete the following:
Sort the /etc/passwd file numerically by the GID field.

For the 10th entry in the sorted passwd file, get an md5 hash of that entry’s home directory.

Output ONLY the MD5 hash of the directory's name to standard output.

Use sort -t* for delimiter

```
sort -t: -k4 -n /etc/passwd | head -10 | tail -1 | cut -d: -f6 | md5sum | cut -d" " -f1
```



15- Write a script which will find and hash the contents 3 levels deep from each of these directories: /bin /etc /var
Your script should:

Exclude named pipes. These can break your script.

Redirect STDOUT and STDERR to separate files.

Determine the count of files hashed in the file with hashes.

Determine the count of unsuccessfully hashed directories.

Have both counts output to the screen with an appropriate title for each count.

HINT: use wc -l

```
mkdir $HOME/HASHES
find /bin /etc /var -maxdepth 3 ! -type p -exec md5sum {} > $HOME/HASHES/success 2>$HOME/HASHES/fail \;
A=$(wc -l $HOME/HASHES/success | awk '{print $1}')
B=$(grep -c "Is a directory" $HOME/HASHES/fail)
if [[ "$A" ]]; then
echo "Successfully Hashed Files: $A";
echo "Unsuccessfully Hashed Directories: $B";
else
echo "oops"; -maxdepth 3
fi

```
```

DIRS='/bin /etc /var'
find $DIRS -maxdepth 3 ! -type p -exec md5sum {} \; >STDOUT.del 2>STDERR.del
Good=$(cat STDOUT.del | wc -l)
Bad=$(egrep "Is a" STDERR.del | wc -l)
echo "Successfully Hashed Files: $Good"
echo "Unsuccessfully Hashed Directories: $Bad"
rm *.del
```

16-Design a script that detects the existence of directory: $HOME/.ssh

Upon successful detection, copies any and all files from within the directory $HOME/.ssh to directory $HOME/SSH and produce no output. You will need to create $HOME/SSH.
Upon un-successful detection, displays the error message "Run ssh-keygen" to the user.
NOTE: If the $HOME/.ssh directory does not exist, one may run the ssh-keygen command. Accept all defaults for the purposes of this exercise. This is not necessary for passing the activity but can be used for testing on your local machine.


```
if [[ -d $HOME/.ssh ]]; then 
    mkdir $HOME/SSH
    cp $HOME/.ssh/* $HOME/SSH/ 
else
    echo "Run ssh-keygen"
fi
```

17-Write a script that determines your default gateway ip address. Assign that address to a variable using command substitution.
NOTE: Networking on the CTFd is limited for security reasons. ip route and route are emulated. Use either of those with no switches.

Have your script determine the absolute path of the ping application. Assign the absolute path to a variable using command substitution.

Have your script send six ping packets to your default gateway, utilizing the path discovered in the previous step, and assign the response to a variable using command substitution.

Evaluate the response as being either successful or failure, and print an appropriate message to the screen.


```

dg=$(route | tail -2 | head -1 | cut -d" " -f2)
pr=$(whereis ping | cut -d" " -f2)
num=$($pr $dg -c 6 | tail -2 | head -1 | cut -d" " -f4)
if [[ $num == "0" ]]; then
echo "failure";
else
echo "successful";
fi

```

"RIGHT" Answer:


```
A=$(route | grep 'default.*[[:digit:]]' | awk '{print $2}')
B=$(which ping)
C=" 0% packet loss"
D=$($B -c 6 $A | grep -Eo "$C")
if [[ "$C" == "$D" ]]; then
echo "successful";
else
echo "failure";
fi
```


18-Create the following files in a new directory you create $HOME/ZIP:

file1 will contain the md5sum of the text 12345

file2 will contain the md5sum of the text 6789

file3 will contain the md5sum of the text abcdef

Create a zip file containing the three files above, without being stored inside a directory in the zip file. Name the zip file $HOME/ZIP/file.zip

HINT: "Junk" the paths

Utilize tar on $HOME/ZIP/file.zip to archive it into a file called $HOME/ZIP/file.tar.gz which should not include directories. Use the gzip option in tar, DO NOT use a seperate gzip binary.

HINT: You might need an option to change directories first.

```
mkdir $HOME/ZIP
echo "12345" | md5sum | cut -d" " -f1 > $HOME/ZIP/file1
echo "6789" | md5sum | cut -d" " -f1 > $HOME/ZIP/file2
echo "abcdef" | md5sum | cut -d" " -f1 > $HOME/ZIP/file3
zip -j $HOME/ZIP/file.zip $HOME/ZIP/file{1,2,3}
tar -czf $HOME/ZIP/file.tar.gz -C $HOME/ZIP/ file.zip
```
19-Design a basic FOR Loop that iteratively alters the file system and user entries in a passwd-like file for new users: LARRY, CURLY, and MOE.
Each user should have an entry in the $HOME/passwd file
The userid and groupid will be the same and can be found as the sole contents of a file with the user's name in the $HOME directory (i.e. $HOME/LARRY.txt might contain 123)
The home directory will be a directory with the user's name located under the $HOME directory (i.e. $HOME/LARRY)
NOTE: Do NOT use shell expansion when specifying this in the $HOME/passwd file.
The default shell will be /bin/bash
The other fields in the new entries should match root's entry
Users should be created in the order specified

```
rootline=$(head -1 $HOME/passwd)
for x in {LARRY,CURLY,MOE} ; do
myuid=$(cat $HOME/$x.txt)
mkdir $HOME/$x
echo $rootline | awk -F: -v uu=$x -v ii=$myuid 'BEGIN{OFS=":"}{$1=uu;$3=ii;$4=ii;$6="$HOME/"uu}{print $0}' >> $HOME/passwd
done
```

20-Write a bash script that will find all the files in the /etc directory, and obtains the octal permission of those files. The stat command will be useful for this task.
Depending how you go about your script, you may find writing to the local directory useful. What you must seperate out from the initial results are the octal permissions of 0-640 and those equal to and greater than 642, ie 0-640 goes to low.txt, while 642 is sent to high.txt.

Have your script uniquely sort the contents of the two files by count, numerically-reversed, and output the results, with applicable titles, to the screen. An example of the desired output is shown below.

NOTE: There is a blank line being printed between the two sections of the output below.

```
find /etc -type f -exec stat -c '%a' {} \; > ./A 2>/dev/null
for x in $(cat ./A) ; do
if [[ $x -le 640 ]] ; then
echo $x >> ./less
elif [[ $x -ge 642 ]] ; then
echo $x >> ./more
fi
done
echo 'Files w/ OCTAL Perm Values 642+:'
cat ./more | sort | uniq -c | sort -nr
echo
echo 'Files w/ OCTAL Perm Values 0-640:'
cat ./less | sort | uniq -c | sort -nr
```

done


#Practice-Test
## 1-Replace every instance of 'cat' in "infile" with 'dog'.
Replace every instance of 'Navy' in "infile" with 'Army'. Replacements are case-sensitive. Write the output to the file specifed by the variable 'outfile'.

```
  infile=$1
  outfile=$2
  #Your code here
sed -e 's/cat/dog/g' -e 's/Navy/Army/g' $1 > $2
```



## 2-Create a script that will print to standard output all user names from the /etc/passwd file.

```
cut -d: -f1 /etc/passwd
```



## 3-Print to standard output all usernames from the file path specified by the parameter filename sorted ascending numerically by user id.
The file will be in the format of /etc/passwd

```
  filename=$1
  #Your code here
cat /etc/passwd | sort -t: -k3 -n | cut -d: -f1
```
```
sort -n -t: -k 3 fakepasswd.txt | cut -d":" -f1
```


## 4-Print to standard output the total number of files in the directory specified by dirname.
If the directory does not exist, print 'Invalid Directory' The count excludes the '.' and '..' pseudo-directories.
```
  dirname=$1
  #Your code here
if [[ $1 ]] ; then
find $1 -type f -maxdepth 1 | wc -l
else
echo "Invalid Directory"
fi
```

## 5-Delete all files contained in the directory specified by dirdel
Also delete the directory specified by dirdel
```
  dirdel=$1
  #Your code here
rm -rf $1
```

## 6-Create a file specified by the name newfile.
Set the file modified date to the value specified in filedate and time to '1730'. NOTE: filedate contains only a valid date in YYYYMMDD format, not a time.
```
  newfile=$1
  filedate=$2
  #Your code here
touch $1
touch -t ${2}1730 $1
```
```
touch -t "$filedate"1730 $newfile
```

## 7-Read the file specified by fname and perform an action based on the contents of the file:
If contents are 0 to 9, print "single digit" to standard output. If contents are 10 to 99, print "double digit" to standard output. If contents are 100 to 999, print "triple digit" to standard output. Otherwise, print "Error" to standard output.
```
  fname=$1
  #Your code here
var=$(cat $1)
num=$(echo "${#var}")
if [[ "$num" == 1 ]] ; then
echo "single digit"
elif [[ "$num" == 2 ]] ; then
echo "double digit"
elif [[ "$num" == 3 ]] ; then
echo "triple digit"
else
echo "Error"
fi
```
```
cont='cat $fname'
if [[ $cont -lt 10 ]] ; then
 echo single digit
if [[ $cont -lt 100 ]] ; then
 echo double digit
if [[ $cont -lt 10000 ]] ; then
 echo triple digit
else
 echo Error
fi
```


## 8-Copy all lines from the file specified by src variable to the file specified by dst variable which DO NOT contain the text specified by match variable

```  
  src=$1
  dst=$2
  match=$3
  #Your code here
cat $1 | grep -v $3 > $2
```
```
cat $src | grep -v $match > $dst
```

## 9-Terminate the process that has the randomly assigned name specified by procname variable. procname does not contain path information.
  
```
  procname=$1
  #Your code here
pkill $1
```
```
pkill $procname
```

## 10-Create a sorted full-path list of all files in the directory dirpath that were modified within the previous day. Directories should not be included in the output. Print the list to the screen, one item per line.
NOTE: The full paths to files should be in your output. (i.e. /etc/passwd would be included)

NOTE: Directory entries should not be included. (i.e. /etc would NOT be included)

```
  dirpath=$1
  #Your code here
find $dirpath -type f -mtime -1 | sort
```
