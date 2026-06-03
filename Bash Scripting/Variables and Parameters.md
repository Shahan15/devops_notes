#### Variables
we can write variables like this: 

```bash
#In VIM
name="Shahan
echo 'Hello, $name'

fruits=("apple","orange","banana")
echo ${fruits[0]} #outputs apple
echo ${fruits[@]} #outputs the entire array

```


#### Parameters
we can pass parameters into our script like this:

```bash
./script.sh parameter1 parameter2
```

to access these parameters
```bash
#IN VIM

#!/bin/bash
echo "Parameter 1: $1"
echo "Parameter 1: $2"
echo "Parameter 1: $3"
echo "All Parameters: $@"
```

we access the parameters as $1,$2, $3
to acces all parameter we do $@


#### Arithmetic Expansion

```bash
num1 = 5
num2 = 10

result = $((num1 + num2))
echo "the sum of $num1 and $num2 is: $result"

length = 5 
width = 6
area = $((length * width))

#with parameters
parameter1 = "$1"
parameter2 = "$2"
```


`()` --> this is a command 

`((num1*num2))` --> this is a math operation. the double parenthesis 