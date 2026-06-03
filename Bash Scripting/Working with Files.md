### Reading Files

```bash
read_files(){
	local file_path="$1"
	
	while IFS= read -r line; do
		echo "$line"
	done < "$file_path"
}

read_file "./log.txt"
```

**NOTE:** bash reads the while loop as one single command. it collects it ALL and stores into memory and THEN executes it. So it sees the 
`done < "$file_path"` and passes in the `$file_path` into loop.



`IFS`  --> Internal Field Separator, This ensures that any leading or trailing whitespaces is preserved

normally Linux would strip away whitespaces. IFS stops that and keeps it. 

`read -r line` --> `read` grabs one line of text at a time and stories it in a variable named `line`. 
`-r` this prevents backslashes `(\)` from acting as escape characters e.g. `\n` wont turn into new lines


`done < "$file_path"` --> Redirection. 

Read command normally wait for the KEYBOARD to input the command. instead we are redirecting the input. and It passes in $file_path 


Alternative way to write this: 

```bash
process_file(){
	local file_path="$1"
	cat "$file_path" | while IFS= read -r line; do
		echo "Processing Line: $line"
	done
}

process_file "./log.txt"
```

### Writing Files

```bash
write_to_file(){
	local file_path="$1"
	data="$2"
	
	echo "$data" > "$file_path"
}

write_to_file "read.txt" "Hello World"
```

### File Checksums

Checksums are cryptographic hashes that provide a unique fingerprint for a file. Used to verify the authenticity of a file 


to generate a file Checksum

```bash
calculate_md5sum(){
	local file_path="$1"
	md5sum "$file_path"
}

calculate_md5sum "read.txt"
```

NOTE: `md5sum` is not a standard linux command, need to install it 

can alternatively use `sha256sum` 


```bash
comapre_checksums(){
	local checksum1="$1"
	local checksum2="$2"
	
	if [[ "$checksum1" == "$checksum2" ]];
		echo "Checksums match. File is intact"
	else
		echo "Checksums do not match"
	fi
}

compare_checksums "123" "123"

```