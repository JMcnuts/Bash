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




