
#### If statement

structure:

```bash
if condition
then

#code block to be executed

fi
```

spaces between the operators matter. i.e. 
if condition 

note the space between 'if' and 'condition'


comparison operators:

| **Abbreviation** | **Description**          |
| ---------------- | ------------------------ |
| **eq**           | equals                   |
| **ne**           | not equal to             |
| **lt**           | less than                |
| **gt**           | greater than             |
| **le**           | less than or equal to    |
| **ge**           | greater than or equal to |
`&&` - AND
`||` - OR

`==` to compare 

```bash
age=25
if [ $age -gt 10 ]
then
	echo "age is greater 10"
	
else
	echo "age is less than 10"
fi
```

can also use standard `elif`:
```bash
if [ $age -gt 10 ]
then
	echo "age is greater 10"
	
elif[ $age -lt 10 ]
	echo "age is less than 10"
else
	echo "age is 10"
fi
```

**you can also nest the if statements**

NOTE: the spaces before and after are very important. 
`if [ $age -gt 10 ]`. the syntax here is precise. there is a space before and after. 