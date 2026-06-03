	
```bash
num1=10
num2=0
result=$((num1/num2))

echo "The result is: $result"
```

this above code will fail as 10 cant be divided by 0. This would cause a large script to fail 


```bash
num1=10
num2=0
result=$((num1/num2))

if [$num2 -eq 0]; then
	echo "Error: Cant divide by 0"
	exit 1
fi


echo "The result is: $result"
```

```bash
FILE='/nonexistent'

if [[ -f "$FILE"]]; then
	echo "File exists."
else
	echo "File does not exist"
fi
```

| **Operator** | **What it checks**                                                                    |
| ------------ | ------------------------------------------------------------------------------------- |
| **`-f`**     | True if the file exists and is a **regular file** (like text files, images, scripts). |
| **`-d`**     | True if the path exists and is a **directory** (folder).                              |
| **`-e`**     | True if the path **exists** at all (doesn't care if it's a file or a folder).         |
| **`-s`**     | True if the file exists and has a **size greater than zero** (is not empty).          |
| **`-r`**     | True if the file exists and is **readable** by you.                                   |

### Exit codes

when a command or script ends. it sends an exit code to the system. this is a numerical value. if it was successful or not: 0 or non zero (respectively)

`set -e` --> stops execution when it encounters an error. a non zero exit code

```bash
set -e

echo "Before the script"
nonexistentcommand
echo "After script"
#This wouldnt print "After script"
```

`set -u` --> stops at uninitialised variables

`set -x` --> prints each command to the terminal before it is executed. Used for debugging

![[Screenshot 2026-05-18 at 12.43.06.png|697]]

can exit debug mode with `set +x` i.e. :
```bash
set -x
	#code to be executed
set +x
```


`set -eux`--> all commands combined.  Stops script when encounters error, uninitialised variable and debugs. 


set -o nounset --> fails at uninitialised variable 

set -o errexit --> fails at error 

set -o pipefail --> causes pipeline to return the last command that exited with a non zero status

```bash
cat nonexistantfile | grep "something"
```

grep doesnt run here and entire pipe fails. Normally, if you run a chain of commands like `command1 | command2 | command3`, the final exit status of the whole pipeline is **only determined by the very last command (`command3`)**.