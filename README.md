<div  align='left'><img src='https://s3.amazonaws.com/weclouddata/images/logos/wcd_logo_new_2.png' width='15%'></div >

Setting up a Linux Environment
==================================

1. Download Multipass by following the instructions on the [website](https://multipass.run/install).
2. Open a terminal and type the following command to create a new Ubuntu instance:
    ```bash
    multipass launch --name my-vm
    multipass shell my-vm
    ```
    This will create a new Ubuntu instance and open a shell in that instance.

Essential Concepts of Linux Command Line
==================================

## Chapter 3 Essential Concepts of Linux Command Line

### Chapter 3 Outline

- 3.1 Understanding the Environment  
- 3.2 Executing a Command Line Tool & Navigating Directories
- 3.3 Getting Help
- 3.4 Combining Command Line Tools
- 3.5 Redirecting Input and Output
- 3.6 Working with Folders and Files
- 3.7 User Management
- 3.8 Permissions
- 3.9 Package Management

### 3.1 Understanding the Environment

- **Terminal**
  - The terminal, is the application where we type our commands in. If you see the following text:
    
    Terminal Example:
    
        $ seq 3
        1
        2
        3



you would type `seq 3` into your terminal and press `Enter`. 

> Note: You do not type the dollar sign. It’s just there to serve as a prompt and let you know that you can type this command. The text below seq 3 is the output of the command.


- **Shell**  
  - Once we have typed in our command and pressed `Enter`, the terminal sends that command to the shell. The shell is a program that interprets the command. Ubuntu uses Bash as the shell, but there are many others available. Once you have become a bit more proficient at the command line, you may want to look into a shell called the Z shell. It offers many additional features that can increase your productivity at the command line.

- **Operating system**
  - Linux is the name of the kernel, which is the heart of the operating system. The kernel is in direct contact with the CPU, disks, and other hardware. The kernel also executes our command-line tools. 



#####  #Check the type of command

> $ type pwd


### 3.2 Executing a Command-line Tool

#### Execute a command

Type the following in your terminal (without the dollar sign) and press `<Enter>`:

```bash
$ pwd
/home/ubuntu
```

The command-line tool `pwd` prints the name of the directory where you currently are. By default, when you log in, this is your home directory (`~`)

#### Navigating Directories

##### #enter a directory

```bash
$ cd ~
$ cd /usr/lib/python3
$ cd ~
```

##### #list a directory

```bash
$ ls
$ ls -alF
```

#####  #go up a level

```bash
$ cd /usr/lib/python3/dist-packages
$ cd ..
```

##### #go up two levels

```bash
$ cd ../..
```

##### #check the current directory

```bash
$ pwd
$ type pwd
```


### 3.3 Getting Help

##### #Check the type of a command

```bash
$ type -a date
```

##### #Get help on a command

  - type `q` to quit the help screen

  - if `man` is not supported in your os, try `help`  

    ```bash
    $ man date
    $ help date
    ```

    ​	

### 3.4 Combining Command Line Tools with `pipe`

The power of the command line comes from its ability to combine these small yet powerful command-line tools. The most common way of combining command-line tools is through a so-called **`pipe`**. The output from the first tool is passed to the second tool. There are virtually no limits to this.

#####  #generate a sequence of numbers

```bash
$ seq 5
```

#####  #combine `seq` and `grep` to see numbers that contain `3`

```bash
$ seq 50 | grep 3
```

#####  #count how many numbers contain `3`

```bash
$ seq 100 | grep 3 | wc -l
```

### 3.5 Redirecting Input and Output

By default, the output of the command-line tool in the pipeline is outputted to the `terminal`. You can also save this output to a `file`.

```bash
$ seq 3 > /home/ubuntu/seq_out
$ cat seq_out
```

>1 
>2 
>3  

`>` will overwrite the file if it already exists

```bash
$ seq 5 > /home/ubuntu/seq_out
$ cat seq_out
```

>1 
>2 
>3 
>4
>5 

`>>` will append data to the existing file

```bash
$ seq 5 >> /home/ubuntu/seq_out
$ cat seq_out
```

>1 
>2 
>3 
>4 
>5 
>1 
>2 
>3 
>4 
>5	  

### 3.6 Working with Folders and Files

#### 3.6.1 Linux File Systems

<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/linux_fs.png" width="40%">     

##### /root

- Every single file and directory starts from the root directory.
- Only the root user has write privilege under this directory.
- Please note that /root is the root user’s home directory, which is not the same as /.

##### /bin – User Binaries

- Contains binary executables.
- Common Linux commands you need to use in single-user modes are located under this directory.
- Commands used by all the users of the system are located here.
- For example: `ps, ls, ping, grep, cp`.

##### /sbin – System Binaries

- Just like /bin, /sbin also contains binary executables.
- But, the Linux commands located under this directory are used typically by the system administrator, for system maintenance purposes.
- For example: `iptables, reboot, fdisk, ifconfig`

##### /etc – Configuration Files

- Contains configuration files required by all programs.
- This also contains startup and shutdown shell scripts used to start/stop individual programs.
- For example: `/etc/resolv.conf, /etc/logrotate.conf, /etc/init.d/`
- The bash scripts under `/etc/init.d` will get executed during Linux startup
  - e.g., `mysqld, postgresql, crond, network`


##### /usr – User Programs

- `/usr/bin` contains binary files for user programs. If you can’t find a user binary under /bin, look under /usr/bin. For example `at, awk, cc, less, scp`
- `/usr/sbin` contains binary files for system administrators. If you can’t find a system binary under /sbin, look under /usr/sbin. For example: atd, cron, sshd, useradd, userdel
- `/usr/lib` contains libraries for /usr/bin and /usr/sbin
- `/usr/local` contains users programs that you install from the source. For example, when you install apache from source, it goes under /usr/local/apache2

##### /home – Home Directories

- Home directories for all users to store their personal files.
- For example: /home/john, /home/nikita

#### 3.6.2 Working with Directories

#####  #list a directory

`list` 

```bash
$ cd ~
$ ls  
```

<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_1.png" width="30%">     

`list with -l option`

```bash
$ ls -l
```

<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_2.png" width="30%">     

`list with -al optino, display hidden files`

```bash
$ ls -al
```

<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_3.png" width="30%">     

`list with -alF option, indicating folder /`

```bash
$ ls -alF
```

<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_4.png" width="30%">     


#####  #create a new directory

```bash
$ cd ~
$ mkdir ~/toolbox
$ ll
```

<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_5.png" width="30%">     

​	 

#####  #change permission of a directory

`check current permission`

```bash
$ ls -l /home/deveplopment
```

<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_6.png" width="30%">     

`change permisson of folder to 400 (owner read only)`

```bash
$ chmod 400 ~/toolbox
$ ls -l /home/deveplopment
```

<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_7.png" width="30%">     

trying to remove a 400 folder will get a warning, type `y` and enter to confirm

<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_8.png" width="30%">     

#####  #remove/delete a directory

```bash
$ mkdir ~/tmp-folder
$ rm ~/tmp-folder
$ rm -r ~/tmp-folder
```

<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_9.png" width="30%">     

> Note: `rm` with `-r` option will remove the entire directory with all it contents

#### 3.6.3 Working with Files

##### #Read and print a file to screen with `cat`

```bash
$ cat /usr/lib/python3/dist-packages/six.py | head
$ cat /usr/lib/python3/dist-packages/six.py | tail
$ cat /usr/lib/python3/dist-packages/six.py | less
$ cat /usr/lib/python3/dist-packages/six.py | head -n 5
```

For the `less` command, you need to use up and down arrow keys to scroll the content, and type `q` to close.

##### #Read and print a file with `head`, `tail`, `less`, `more`

```bash
$ head /usr/lib/python3/dist-packages/six.py
$ tail /usr/lib/python3/dist-packages/six.py
```

<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_10.png" width="30%">

​     <img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_11.png" width="30%">











##### #View and edit a file with `vi`

The default editor that comes with the UNIX operating system is called vi (visual editor). 

- Tutorial: [Basic Linux vi command](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0ahUKEwj7xomRnvPRAhVIurwKHcgHCyIQFggaMAA&url=https%3A%2F%2Fwww.cs.colostate.edu%2Fhelpdocs%2Fvi.html&usg=AFQjCNGdVL4Ru2lI7iivBAMmkmFHS79hPA)

  - hit `i` key to start editing
  - hit `esc` key to quit editing and enter view mode
  - hit `d` key twice to delete a line
  - in view mode [hit `esc` key] enter `:q!` to quit without saving
  - in view mode [hit `esc` key] enter `:wq!` to quit with saving changes 

> The default version of vim in Ubuntu is `vim.tiny`, you need to run `sudo apt-get install vim` first to get the complete version of vim

1. Write something to a file  

   ```bash
   $ mkdir toolbox
   $ echo "Linux is an essential skill a data scientist must master!" > /home/ubuntu/toolbox/testfile.txt
   $ cat ~/toolbox/testfile.txt
   ```

2. Open and edit the file with `vi`

   - type `vi` to edit the file

   - hit `i` to start editing

   - add some text in a new line "This course preps you for a smooth data science learning curve!"

   - hit `esc` to quit editing mode

   - save and quit with `:wq!`

     ```bash
     $ vi ~/toolbox/testfile.txt
     ```

     - <img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_12.png" width="30%">     

   - **NOTE** if you are not allowed to save this file, check the folder permission. The folder may be in read-only mode. Try `chmod` or use `sudo vi testfile.txt` 

3. Verify that file was saved correctly

   ```bash
   $ cat ~/toolbox/testfile.txt
   ```

   

##### #Find a file

- Find the testfile.txt you just created

  ```bash
  $ find /home testfile.txt
  ```

  Note: you get long list of results because `find` is trying to match string "testfile.txt" against full path

  ```bash
  $ find /home/ubuntu/toolbox/testfile.txt | grep testfile.txt
  ```

  <img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_13.png" width="30%"> 

  ```bash
  $ find /home -name testfile.txt
  ```


	<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_14.png" width="30%"> 

##### #Move a file

- Copy a file to a new folder

  ```bash
  $ cp /home/ubuntu/toolbox/testfile.txt /home/ubuntu/
  ```

- Move a file to a different folder

  ```bash
  $ mv /home/ubuntu/testfile.txt /home/ubuntu/testfile_copy.txt
  ```

  

##### Rename a file (using `mv`)

```bash
$ mv /home/ubuntu/toolbox/testfile.txt /home/ubuntu/toolbox/testfile_1.txt
```


​	

### 3.7 User Management

#### 3.7.1 Add User

##### #Add a testuser and set password

1. Set a password to root account first

   ```bash
   $ sudo passwd root
   ```

2. Switch to root account temporarily

   ```bash
   $ su root  
   ```

3. Add a `testuser`

   ```bash
   $ adduser testuser
   ```

4. Create a password for `testuser`	

   ```bash
   $ passwd testuser
   ```

5. Temporarily switch to `testuser` account

   ```bash
   $ su testuser
   ```

6. Try to create another new user testuser_1

   ```bash
   $ adduser testuser_1
   $ sudo adduser testuser_1
   ```

   > At this step you'd expect an error in the command line due to lack of permission to use `adduser` system command
   > You can make `testuser` a `sudo` account

#### 3.7.2 Make a `sudo` user

##### #Make user testuser a `sudo` user

```bash
$ su root 
$ usermod -aG sudo testuser
```

##### #Create a new user with `sudo` permission

```bash
$ su testuser
$ sudo adduser testuser_1		
$ sudo cat /etc/passwd
```

<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_15.png" width="30%"> 
	

#### 3.7.3 Delete User

##### #Delete a user

```bash
$ sudo userdel testuser_1
```


​	
**create command alias (shortchut)**  
for those systems that don’t support 'll' you can use alias

```bash
$ alias ll='ls -alF'
```

### 3.8 Permissions

Linux is a multi-user system which means that multiple users can access the same file/directory. Permissions will allow users to protect from each other.


#### 3.8.1 Viewing file permissions

##### #View file permissions

```bash
$ ls -l /home/ubuntu/toolbox/testfile.txt
```

<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_16.png" width="30%"> 

How to interpret file permission?  

- This file is owned by `development`
- The superuser has the right to read, write this file
- The file is owned by the group `development`
- Members of the group `development` can also read and write this file
- Everybody else can ONLY read this file	

##### #Understanding permissions

<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/linux_permission.png" width="30%"> 

#### 3.8.2 Change file access permissions

The `chmod` command is used to change the permissions of a file or directory. To use it, you specify the desired permission settings and the file or files that you wish to modify.

It is easy to think of the permission settings as a series of bits (which is how the computer thinks about them). Here's how it works:

	rwx rwx rwx = 111 111 111
	rw- rw- rw- = 110 110 110
	rwx --- --- = 111 000 000
	
	and so on...
	
	rwx = 111 in binary = 7
	rw- = 110 in binary = 6
	r-x = 101 in binary = 5
	r-- = 100 in binary = 4

##### #Change the permission of a file so that only the owner can read and write the file

```bash
$ su development
$ chmod 600 /home/ubuntu/toolbox/testfile_1.txt
```

Test by accessing this file from a different user account

```bash
$ su testuser
$ cat /home/ubuntu/toolbox/testfile_1.txt
```

<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_17.png" width="30%">

 

> Access denied due to wrong permission, but you can still read it by `sudo`ing

#### 3.8.3 Change the file ownership (`chown`)

```bash
$ exit
$ sudo chown testuser /home/ubuntu/toolbox/testfile_1.txt
$ ls -l /home/ubuntu/toolbox/testfile_1.txt
```

<img src="https://s3.amazonaws.com/weclouddata/images/data_engineer/david_linux/command_18.png" width="30%"> 

#### 3.8.4 Change the file group ownership (`chgrp`)

```bash
$ sudo chgrp testuser /home/ubuntu/toolbox/testfile_1.txt
```


### 3.9 Package Management

#### 3.9.1 Package Installation

##### #Install pip

```bash
$ sudo apt install python3-pip
```

##### #Install AWS-ClI

```bash
$ sudo pip3 install awscli
```

------

------

