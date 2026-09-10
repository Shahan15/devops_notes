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


#####

![[Screenshot 2026-09-10 at 14.37.30.png]]

```python
class Solution:

def topKFrequent(self, nums: List[int], k: int) -> List[int]:

	#This question is asking to tally how many times a number appers and the k most occuring numbers. return it.
	
	#HashMap/Dict
	
	count = {}
	
	
	for i in range(len(nums)):
	
		count[nums[i]] = count.get(nums[i],0) + 1
	
	sorted_items = sorted(count.items(), key=lambda x: x[1], reverse=True)
	
	# 3. Slice the top k items and grab just the number (x[0])
	
	return [x[0] for x in sorted_items[:k]]
```

`sorted() `-->  this function takes a list ad sorts it. By default, it sorts from lowest to highest.
	 We add `reverse=True` to sort it highest to lowest

`count.items()` --> This converts the dictionary into a list of tuples, formatted as `(key, value)`  --> or here it would be `(number, frequency)`

`key` --> this arg tells `sorted` function what to sort by

`lambda` -->  this is just a function without a name. its like AWS lambda its just a function without a name.
	 so we assign each item `x`. 
	 then we decide to sort them only looking at the frequency. so `x[1]`
