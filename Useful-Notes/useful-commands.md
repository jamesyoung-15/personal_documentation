# Useful Terminal Commands I Use
Remember can use `man` to check commands and but `tldr` is quicker and easier as it gives some common examples of how to use certain commands. 

## Basics:

### Change working directory
``` bash
cd path/directory # go to directory
cd ~/ # go to home directory of user
cd / # go to root directory
```

### Listing
``` bash
ls # list directory
ls -a # list all including hidden files
ls -l # gives more info like file/directory permissions 
pwd # print working directory
```

### Copying
``` bash
cp path/file_to_copy path/file_destination # copy directory to some destination, only for single file
cp -r path/directory path/destination # copy directory content to destination
cp -r path/directory/* path/destination # copy everything inside directory but not the folder itself
```

### Moving 
``` bash
mv path/file path/file_destination # move directory to destination
mv file1 file2 file3 target_directory # move multiple files to destination 
mv directory/* target_directory # move everything inside directory to destination
mv file new_filename # can also use move command to rename file
```

### Creating file and directory
``` bash
mkdir directory # make a directory, if making multiple just add directory names all in one line
mkdir -p path/directory # make these directories recursively, will skip making it if path exist
touch file.txt # example of creating a text file, can create other formats by changing .txt
touch file{1,2,3}.txt # example of creating multiple text files
vim file.txt # can also create a file by editing using some editor like nano or vim then saving it
```
### File Permissions
``` bash
chmod u+x executable.sh # Give the [u]ser who owns a file the right to e[x]ecute it
chmod g-x executable.sh # remove permission to execute
chmod u+rw file_or_directory # [u]ser has [r]ead [w]rite permission
chmod 777 file # can also use number to represent permission, eg. 777 allows everyone to read, write, and execute
chown user file_or_directory # change owner of a file or directory
chown user:group file_or_directory # change owner user and group of a file or directory
chown -R user path/file_or_directory # recursively change ownership
```
More on chmod and it's modes: https://ss64.com/bash/chmod.html

### Remove files and directories
``` bash 
rm file # remove some file
rm -r path/directory # recursively remove a directory and everything inside
rm -rf path/directory # forcefully remove directory, useful when getting error message
rmdir directory # alternatively rmdir to remove directory
rmdir -p path/directory # recursively remove directories
```

### Quickly writing and viewing file cotent
Without using editor like vim
``` bash
cat path/to/file # prints content of file
cat path/to/file1 path/to/file2 > path/to/output_file # concatenate files into output file
cat path/to/file1 path/to/file2 >> path/to/output_file # append files into output file
cat -n path/to/file # ouput lines are numbered
echo
tee
```


## Networking
### Ping
Useful for quickly checking connection.
``` bash
ping archwiki.org # pings to some website like archwiki.org or google.com
ping 192.168.0.1 # can also ping ip address, useful for checking local network
```
### Dig
For DNS lookup, useful for checking DNS server or website DNS records/settings.
``` bash
dig archwiki.org # Get all types of records for given domain name
dig @9.9.9.9 archwiki.org # Specify an alternative DNS server to query
```
### Check Ports
``` bash
sudo lsof -i -P -n | grep LISTEN
sudo netstat -tulpn | grep LISTEN
```

### SSH
``` bash
ssh username@remote_host # ssh into remote server, default port is 22
ssh -p port_number username@remote_host # ssh with specific port number
```
Copying files over SSH:
``` bash
scp path/to/local_file remote_host:path/to/remote_file # copies file to remote host over ssh
scp -P port path/to/local_file remote_host:path/to/remote_file # copies file to remote host with specific port number
scp remote_host:path/to/remote_file path/to/local_directory # copies file from remote host
scp -r remote_host:path/to/remote_directory path/to/local_directory # copies recursively from remote to local
```
## Monitoring

### Find process
``` bash
top # Gives a real time view of processes
htop # Same as above but a bit nicer
ps aux # Lists running processes but not in real time
ps aux | grep string # search for a prcoess that matches a string, useful for finding a specific process to kill
```
### Kill process
``` bash
kill process_id # terminate program using SIGTERM signal
kill -l # list available signal names
kill %job_id #terminates background job
```
- SIGTERM terminates program by requesting program to stop running and gives it time to save progress.
- SIGKILL forces program to quit and may lose progress.
