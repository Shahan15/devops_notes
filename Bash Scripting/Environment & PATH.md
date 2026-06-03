here we will explore how bashrc and zshrc can be used to configure our shell. i.e. changing PATH environment variable. 

Note: PATH environment variable is where the shell looks for, for executable files.

Example: 
```bash
mkdir myScripts
vi myScripts/hello_world.sh #this is a out script to do whatever
chmod +x myScripts/hello_world.sh

echo "export PATH=$PATH:~/myScripts" >> /.zshrc
```

Note: `>>` is the append command. add the line to the BOTTOM of the file we are appending to. 


initially we are just adding the line:
`"export PATH=$PATH: ~/myScripts"` to the bottom of `./zshrc` file. 

when the `./zshrc` file gets executed it adds the `~myScripts` to the `$PATH`. so now the `$PATH` is something like this: 
`/usr/bin:/bin:~/myScripts`

you also have your standard shell commands but you also now have myScripts.

the `/usr/bin:/bin:` are completely separate folders CHAINED together. they are separated by `(:)`. so when we now run hello_world.sh. it looks through all the folders until it finds it, in `/usr/bin:/bin:~/myScripts` . 

then we run:
```bash
source /.zshrc
```

The `source` command is a built-in shell tool that reads and executes the contents of a file **inside the current terminal session**.s

Normally, when you run a script like `./myscript.sh`, your terminal doesn't actually run the code itself. Instead, it creates a temporary, isolated background process called a **subshell**.

The script runs inside that subshell, finishes, and then the subshell destroys itself. Because of this isolation:

- Any variables created inside the script are lost.
- Any changes to the environment (like switching directories with `cd`) disappear.
### Reading Environment Variables 

```bash
echo "Home Directory $HOME"
echo "Current User: $USER"
echo "OS Type: $OSTYPE"
```

```bash
$LOGNAME #logging name of current user
$SHELL #path of current user shell 
$PWD #current working directory
$PATH #PATH environment variables
$LANG #Default language setting
```

