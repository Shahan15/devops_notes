Bash scripting is essentially a file containing commands you can execute 
- used for automating tasks
- managing systems

Shebang `(#!)`: The first line in your script `#!/bin/bash` tells your computer to use Bash to run this script 

to make it executable - `chmod +x your_script.sh`

to run it: `./your_script.sh`

#### Basic Concepts 

**Variables:** 
- `name = "Shahan"
- Use them: `echo "Hello, $name"`

**Comments:**
- `(#)` to use comments 
- for multi line comment
```bash
: '
Multi 
line
comment
 '
```

make sure to add the space after the colon

**Conditionals**: 
- Make decisions with `if` statements.  
  Example:
  
```bash
if [ $name == "Alice" ]; then echo "Hi Alice!" fi
```

**Loops**:

- Repeat actions with `for` or `while`.  
  Example:
```bash
for i in 1 2 3; do echo "Number $i" done
```

**Functions**:
- Group commands for reuse.  
  Example:

```bash
greet() { echo "Hello, $1!" } greet "Alice"
```

**User Input:**
```bash
read -p "Enter your name: " name echo "Hello, $name!"
```



to run a executable we have been using ./myscript.sh
meaning search for that file in the current directory. 
if we wanted to execute it from anywhere we need to add it to our $PATH