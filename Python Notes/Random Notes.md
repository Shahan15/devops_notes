##### Slicing

```python
word = "flower"
print(word[:1])   # Output: "f"

word = "flower"
print(word[:-1])  # Output: "flowe"  (dropped the 'r')
```


Slicing follows the following syntax `[start : stop : step]`
	 So when we do `[:-1]` the `start` is left blank. it starts at index 0
	 `stop` is set to `-1` this means it counts backwards. 

Note: 
- If you use **one colon**, Python expects `[ start : stop ]`.
- If you use **two colons**, Python expects `[ start : stop : step ]`.

```python
word = "abcdefgh" 

# 1. Default step (1) - takes every letter normally 
print(word[0:6:1]) # Output: "abcdef" 

# 2. Step of 2 - skips every other letter 
print(word[0:8:2]) # Output: "aceg" (took 'a', skipped 'b', took 'c', skipped 'd'...) 

# 3. Negative step (-1) - reverses the entire string 
print(word[::-1]) # Output: "hgfedcba"
```
