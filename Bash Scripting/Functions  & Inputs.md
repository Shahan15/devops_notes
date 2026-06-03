
syntax: 
```bash
greet_person(){
	local name='$1'
	echo "hello $name"
}

greet_person "Shahan"
```

local limits the scope of the variable to only within that function

### Parameters
``
```bash
print_args () {
	echo "Number of arguments: $#"
	echo "Script name: $0"
	echo "First argument: $1"
	echo "Second argument: $2"
	echo "All arguments: $@"
}
```


### User Input

syntax: 
```bash
greet_user(){

	echo "what is your name:?"
	read name
	echo "Hello, $name!"
}

greet_user
```

### Piping

used to input the output of one function into another

```bash
get_file_count(){
	
	local directory = "$1"
	local file_count
	
	file_count=$(ls "$directory" | wc -l)
	
	echo "Number of files in $directory: $file_count"
}

get_file_count = "./"
```