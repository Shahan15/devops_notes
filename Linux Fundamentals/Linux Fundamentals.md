
core concept is that everything is treated as a file. These are organised within a hierarchical structure called the ***filesystem*** 

the filesystem starts from the top-level directory called the root directory. Represented by ' /  '. Example structure: 

![[Screenshot 2026-05-11 at 12.06.11.png]]

when you open a Terminal you will be greeted with `Shahan@icebox:/home/shahan $`
the $ means it is simply ready to accept a command

and we are communicating directly with the OS. 

we do this via `Shell` and there are different Shell's such as Bash -> which means 'Born again shell'.

on MacOS: 
```bash
echo $SHELL #this would print /bin/zsh
#on a bash shell it would print bash
```

the commands we use are actually Programs. so when we run `ls` or `echo` we running the `ls` program.  these are listed in the 'path environment variable'

we can change shells by just typing the name in the shell e.g. `shell` or `bash`

## **Commands**

##### **📂 Linux Navigation & Files**

`echo` - this outputs whatever you write back to you i.e. 

```bash
echo "hello world"    # Simply prints 'hello world'
echo $USER            # Prints your current username
```

this would simply just output 'hello world' back to the terminal. 

this can also be used to write to files e.g.

```bash
echo "Hello World" > file.txt #this would write Hello World to the file.txt

echo "Hey There" >> file.txt #this appends the file. so it would add Hey There to the file
```

`pwd` --> print working directory, prints the full working directory you are currently in starting from root. 

`cd` --> Change directory. 
Changes your current directory
	`cd .` (current directory): Represents the directory you are currently in.
	`cd ..` (parent directory): Moves you one level up to the directory containing your current one.
	`cd ~` (home directory): A shortcut to your personal home directory, like `/home/pete`.
	`cd -` (previous directory): Takes you back to the last directory you were in.

to navigate into empty directories
```bash
cd "My Project"
```

`ls` --> lists the directories and files in your current directory or specified path

hidden files start with a (`.`). can view this with (`-a`). can use (`-l`) for detailed view

```bash
ls 
ls /home/shahan
ls /project/src/componenets

ls -R project
#this lists directories recursively. 
```

`touch` --> creates an empty file.

```bash
touch mysuperduperfile.txt
```

`mkdir` --> make directory. creates a directory

```bash
mkdir favourites

mkdir -p books/hemmingway/favorites #this is for nested directories
```

what if you want to make a directory called 
'My Directory'. Bash would create two directories 'My' and 'Directory'. 

```bash
mkdir "My Project" 
#can also use 
mkdir My\ Project\ 2
```

`rmdir` --> removes empty directories

```bash
#books/hemmingway/favorites
rmdir favourites 
```

`rm` --> remove. Deletes a directory

```bash
rm file1.txt

rm -r mydirectory #for directories
```

> [!WARNING]
> `rm -rf /` deletes EVERYTHING. do not run this.


mv --> move. moves directory . also renames.

```bash
mv myfile.txt my_directory

mv file1.txt fileRenamed.txt
```

cp --> copy. copies directory into another directory

```bash
cp multiline.txt multiline_copy.txt

cp -r my_directory my_directory_copy 
#-r is for directories
```


##### **🔍 Reading & Searching**

`cat` --> displays the content of a single file 

```bash
cat file.txt
```

this can also be used to combine files into one. e.g.
```bash
cat file.txt myfile2.txt > combined.txt
#this would combine file and myfile2 into the combined.txt file
```


`less` --> some texts are too large for the screen. you can use 'less' to view the file page by page. 

```bash
less /home/shahan/Documents/text1
```

`head` or `tail` 
	`head` prints the first 10 lines 
	`tail` prints the last 10 lines
you can add options too to view specific number of lines 

```bash
head -n 3 multiplelines.txt
```

you can also use these together to print the specific sections e.g. lines 6-10 

```bash
head -n 10 multiline.txt | tail -n 5 
```

what this essentially does is print first 10 lines. from those 10 lines. it prints the last 5 lines. so you would print 6,7,8,9,10
(assuming the first line is Line 1)
##### find / grep

`find` --> finds a specific file in a directory. For example, to search for a file named `puppies.jpg` within the `/home` directory and all its subdirectories or if you want to find a directory instead of a file, you can use `d`.

```bash
find /home -name puppies.jpg

find /home -type d -name MyFolder
```

common flags with this: 
```bash
find . -type f -exec file {} +

# (.) means current directory
# -type f. only files. otherwise it would return everything 
#exec --> its like for every file execute the following command. {} is the current file 
#outputs the file type
# + -> this bundles teh files together and executes the command once
```

Here are the most common letters you'll use with `-type`:

| **Code** | **Meaning**       | **Description**                                          |
| -------- | ----------------- | -------------------------------------------------------- |
| **`f`**  | **Regular File**  | Text files, images, PDFs, programs.                      |
| **`d`**  | **Directory**     | Just the folders themselves.                             |
| **`l`**  | **Symbolic Link** | A "shortcut" that points to another file.                |
| **`p`**  | **Named Pipe**    | A special file used for communication between processes. |

`grep` --> this searches for specific TEXT inside a file. For example:

```bash
grep "Tax" invoice.pdf
```
can also use it on a directory and it will search all subfolders: 

```bash
grep -r "password" .
```

to further clean up output you can use: 

`awk`--> picks out specific parts/columns you need. sees text as a series of columns. E.g.

`[Col 1] [Col 2]  [Col 3]  [Col 4]` 
  `User     ID      Status   App`

$1 - would be the 'User'
$2 would be 'ID'

`sed` --> cleans the text, can replace text for something else

```bash
cat /etc/passwd | awk -F':' '{print $1}' | sed 's/^/User: /'
```

the syntax for `sed` is 's/find/replace/'

lets say /etc/passwrd is a database of all user accounts. and each line is a messy string separated by colons e.g.
`root:x:0:0:root:/root:/bin/bash
`daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin`

`sed 's/^/User: /'` 
- **`s`**: Substitute (find and replace).
    
- **`^`**: This is a special symbol that means **"the very start of the line."**
    
- **`/User: /`**: This is what we want to put at that starting point.

making the Final Output: 
`User: root` 
`User: daemon`
##### Processes

`ps` --> process status, shows you what processes are currently running in background. 
You can use `aux`. 
	`a` all, shows all processes
	 `u` user-orientated, changes output to user orientated 
	 `x` eXtra, shows programs running in the background

```bash
ps aux
```

`systemctl` --> used to control services. background services e.g. wifi, servers. `sudo` allows you to execute a command as the super user

```bash
systemctl start [service] # — Start a program.

systemctl stop [service] # — Stop it.

systemctl status [service] # — Ask the system, "Is this program running okay or did it crash?"

#Example 
sudo systemctl start postgresql
```

`ssh` --> secure shell, allows you to manage other computers 

```bash
ssh sam@192.168.1.50
```


## Permissions and User Management

##### File Permissions

when we run `ls -l` the terminal may output something like

```bash
$ ls -l Desktop/ drwxr-xr-x 2 pete penguins 4096 Dec 1 11:45 .
```

`drwxr-xr-x` - this represents the file types + permissions

d - this signifies that Desktop is a **directory** otherwise you would just see (`-`)

`d | rwx | r-x | r-x`

**r** : Read permission.	
**w** : Write permission.
**x** : Execute permission.
**-** : No permission granted.

The three sets of permissions apply to different levels of access:

1. **User (Owner)**: The first set (`rwx`) applies to the owner of the file, which is `pete` in our example. The owner has read, write, and execute permissions.
2. **Group**: The second set (`r-x`) applies to the group associated with the file, which is `penguins`. Members of this group have read and execute permissions but cannot write to the file.
3. **Other**: The final set (`r-x`) applies to all other users on the system. They have read and execute permissions.

##### Modifying Permissions

you use `chmod` to modify file or directory access rights. 
`chmod` offers two methods: **symbolic** and **numerical**

###### symbolic

this is more readable as letters represent users and permissions.
use a `+` to add a permission or a `-` to remove it.

- `u` (user/owner)
- `g` (group)
- `o` (others)
- `a` (all: user, group, and others)

```bash
chmod g-w myfile #removes write permission from group

chmod u+x myfile #adds (+) the executable (x) permission for the user (u) on 'myfile'

chmod ug+w myfile #adds write permission for group & user

#can also do
chmod ug=rw, o=r example.txt
```

###### numerical

this is standard for large files

- `4`: read (r)
- `2`: write (w)
- `1`: execute (x)

to set permission set, you add the numbers e.g. to give read, write and execute. Use, `4 + 2 + 1 = 7`

```bash
chmod 755 myfile

#User gets read,write and execute permission
#Group and Others, Read and execute
```

first number represents User
second represents Group 
Third represents Others


##### Ownership Permissions

to transfer the ownership of a file, you can use `chown`. you would also need (`sudo`) to change owner of a file you don't own 

```bash
sudo chown patty myfile
#changes user owner of 'myfile' to the user 'patty'

sudo chgrp whales myfile
#changes group ownership of 'myfile' to the user 'whales'

sudo chown patty:whales myfile
#changes user ownership to 'patty' and group owenership to 'whales'
```

there are other ways of changing ownership too: 

```bash
sudo chown shahan:users example.txt

sudo chown -R shahan:users myDirectory #this is for Directories
```

'Shahan' is the **New Owner**, users is the **New Group**

you can switch to super user overall by typing `sudo su`

##### User managment

`useradd` --> creates a new user
`passwrd` --> creates a password

```bash
sudo useradd newuser
sudo passwrd newuser
#will get prompted to update password

su - newuser #will switch to the new user
```

`sudo usermod -ag sudo newuser` --> this would give sudo privileges to the new user. have to be a sudo user to give sudo permissions

`sudo deluser newuser sudo` --> this would remove sudo permissions

When you give permissions such as `sudo` to a user you adding them to a user the root *'group'*. you can alternatively make your own group. this is available in etc/groups

```bash
sudo groupadd devops
```

## Process monitoring and troubleshooting 

##### Processes

processes are the programs currently running on your machine. Each process is assigned a **process ID(PID)** 

`ps` shows  processes

![[Screenshot 2026-05-08 at 12.08.24.png]]

This output shows a few key details:

- **PID**: The unique Process ID.
- **TTY**: The controlling terminal for the process.
- **STAT**: The current status of the process.
- **TIME**: The total CPU time the process has used.
- **CMD**: The command that started the process.

## VIM

this is a text editor

```bash
vim example.txt
```

you have 3 modes: 
	**Command Mode** - Default mode. allows you to move around file and perform operations. to get to this mode we press `esc`
	**Insert Mode** - This is for editing text. for this we press `I`
	**Visual Mode** - This is for for selecting text. for this we press `V`

in ***Command Mode*** you can use:
	 'H' to move left 
	 'L' to move right
	 'J' to move down
	 'K' to move up

after done writing you type `:wq` --> to force you use `:wq!`

to search for a word you can use ***'/example'*** and then you can press enter and search for next occurance using ***'n'***

you can undo by pressing ***'u'*** and redo via ***'control r'***



## Data Redirection

##### Standard Streams

- Standard Input `(stdin)` - This is how you give instructions or data ***to*** the program. When you type a search term into command.
	- `(<)`: you can tell the worker to stop looking at the keyboard and instead take data from a file. 


- Standard Output `(stdout)` - This is where the program sends its successful results.  When you type `ls` you are given the `stdout` 
	-  `(>)`: You can 'catch' this output and put it in a file

- Standard Error `(stderr)` - This is for error messages and warnings. 
	- `(2>)`: You can tell the program to send errors to a log file while still showing the successful results on the screen

you can redirect stuff to a file called '/dev/null' - this will discard anything that is inside it. 


## Environment variables

these are variables set in the environment and effect the behaviour of processes. ![[Screenshot 2026-05-11 at 22.41.45.png|663]]

`printenv` - prints the current environment variables 

to set an environment variable we can use

```bash
export MY_VAR="Hello World"
#this creates a MY_VAR environment variable for this session
```

## Aliases

alias is a command you can run that is a shortcut to run a longer different command. 

you can also make your own aliases. 

```bash
alias hello='echo Hello World'
```

to make this permanent you can add it to your shell e.g. 
```bash
vim .zhrc 
#then add it at the bottom and save
```

so now when you run hello, it will  run 'echo Hello World'