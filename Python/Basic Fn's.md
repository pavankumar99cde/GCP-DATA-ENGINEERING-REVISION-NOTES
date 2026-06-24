# 1. Reverse a String
```python
s = "hello"
### Method 1: Without Built-in Functions
reversed_str = ""
# Add each character to the front
for ch in s:
    reversed_str = ch + reversed_str
print(reversed_str)
# Output: olleh


### Method 1: Using Python Built-in Features
result = s[::-1]
print(result)
# Output: olleh
```
# 2. Check Whether a String is a Palindrome
```python
s = "madam"
### Method 1: Without Built-in Functions
left = 0
right = len(s) - 1
is_palindrome = True
# Compare characters from both ends
while left < right:
    if s[left] != s[right]:
        is_palindrome = False
        break
    left += 1
    right -= 1
print(is_palindrome)
# Output: True

### Method 1: Using Python Built-in Features
result = s == s[::-1]
print(result)
# Output: True
```
# 3. Find the Factorial of a Number Using Recursion
```python
n = 5
### Method 1: Using Recursion
def factorial(num):
    if num == 0 or num == 1:
        return 1
    return num * factorial(num - 1)
print(factorial(n))
# Output: 120

### Method 1: Using math.factorial()
import math
print(math.factorial(n))
# Output: 120
```
# 4. Find the Fibonacci Series Up to N Terms
```python
n = 7
### Method 1: Without Built-in Functions
a = 0
b = 1
for i in range(n):
    print(a, end=" ")
    temp = a + b
    a = b
    b = temp
# Output: 0 1 1 2 3 5 8

### Method 1: Using List Approach
fib = [0, 1]
for i in range(2, n):
    fib.append(fib[i - 1] + fib[i - 2])
print(fib)
# Output: [0, 1, 1, 2, 3, 5, 8]
```
# 5. Find the Largest and Smallest Number in a List
```python
nums = [10, 25, 3, 78, 15]
### Method 1: Without Built-in Functions
largest = nums[0]
smallest = nums[0]
for num in nums:
    if num > largest:
        largest = num
    if num < smallest:
        smallest = num
print("Largest:", largest)
print("Smallest:", smallest)
# Output:
# Largest: 78
# Smallest: 3

### Method 1: Using Built-in Functions
print("Largest:", max(nums))
print("Smallest:", min(nums))
# Output:
# Largest: 78
# Smallest: 3
```
# 6. Remove Duplicates from a List While Preserving Order
```python
nums = [1, 2, 3, 2, 4, 1, 5]
### Method 1: Without Built-in Functions
result = []
for num in nums:
    if num not in result:
        result.append(num)
print(result)
# Output:
# [1, 2, 3, 4, 5]

### Method 1: Using dict.fromkeys()
result = list(dict.fromkeys(nums))
print(result)
# Output:
# [1, 2, 3, 4, 5]
```
# 7. Find the Second Largest Number in a List
```python
nums = [10, 20, 5, 40, 30]
### Method 1: Without Built-in Functions
largest = second = float('-inf')
for num in nums:
    if num > largest:
        second = largest
        largest = num
    elif num > second and num != largest:
        second = num
print(second)
# Output:
# 30

### Method 1: Using Built-in Functions
result = sorted(set(nums))[-2]
print(result)
# Output:
# 30
```
# 8. Count the Frequency of Each Character in a String
```python
s = "banana"
### Method 1: Without Built-in Functions
freq = {}
for ch in s:
    if ch in freq:
        freq[ch] += 1
    else:
        freq[ch] = 1
print(freq)
# Output:
# {'b': 1, 'a': 3, 'n': 2}

### Method 1: Using Counter
from collections import Counter
print(Counter(s))
# Output:
# Counter({'a': 3, 'n': 2, 'b': 1})
```
# 9. Check Whether Two Strings are Anagrams
```python
s1 = "listen"
s2 = "silent"
### Method 1: Without Built-in Functions
freq1 = {}
freq2 = {}
for ch in s1:
    freq1[ch] = freq1.get(ch, 0) + 1
for ch in s2:
    freq2[ch] = freq2.get(ch, 0) + 1
print(freq1 == freq2)
# Output:
# True

### Method 1: Using sorted()
print(sorted(s1) == sorted(s2))
# Output:
# True
```
# 10. Find the Missing Number in an Array Containing Numbers from 1 to N
```python
nums = [1, 2, 3, 5]
n = 5
### Method 1: Without Built-in Functions
expected_sum = n * (n + 1) // 2
actual_sum = 0
for num in nums:
    actual_sum += num
print(expected_sum - actual_sum)
# Output:
# 4

### Method 1: Using Set Difference
all_nums = set(range(1, n + 1))
missing = all_nums - set(nums)
print(missing)
# Output:
# {4}
```
# 11. Find Duplicate Elements in a List
```python
nums = [1, 2, 3, 2, 4, 5, 1, 6]
### Method 1: Without Built-in Functions
duplicates = []
seen = []
for num in nums:
    if num in seen:
        if num not in duplicates:
            duplicates.append(num)
    else:
        seen.append(num)
print(duplicates)
# Output:
# [2, 1]

### Method 1: Using Collections Counter
from collections import Counter
result = []
for key, value in Counter(nums).items():
    if value > 1:
        result.append(key)
print(result)
# Output:
# [1, 2]
```
# 12. Merge Two Sorted Lists into a Single Sorted List
```python
list1 = [1, 3, 5, 7]
list2 = [2, 4, 6, 8]
### Method 1: Without Built-in Functions
merged = []
i = 0
j = 0
while i < len(list1) and j < len(list2):
    if list1[i] < list2[j]:
        merged.append(list1[i])
        i += 1
    else:
        merged.append(list2[j])
        j += 1
while i < len(list1):
    merged.append(list1[i])
    i += 1
while j < len(list2):
    merged.append(list2[j])
    j += 1
print(merged)
# Output:
# [1, 2, 3, 4, 5, 6, 7, 8]

### Method 1: Using Built-in Functions
result = sorted(list1 + list2)
print(result)
# Output:
# [1, 2, 3, 4, 5, 6, 7, 8]
```
# 13. Sort a List Without Using sort()
```python
nums = [5, 2, 8, 1, 9]
### Method 1: Bubble Sort
arr = nums.copy()
for i in range(len(arr)):
    for j in range(0, len(arr) - i - 1):
        if arr[j] > arr[j + 1]:
            temp = arr[j]
            arr[j] = arr[j + 1]
            arr[j + 1] = temp
print(arr)
# Output:
# [1, 2, 5, 8, 9]

### Method 1: Using sorted()
print(sorted(nums))
# Output:
# [1, 2, 5, 8, 9]
```
# 14. Find the First Non-Repeating Character in a String
```python
s = "aabbcdde"
### Method 1: Without Built-in Functions
freq = {}
for ch in s:
    if ch in freq:
        freq[ch] += 1
    else:
        freq[ch] = 1
for ch in s:
    if freq[ch] == 1:
        print(ch)
        break
# Output:
# c

### Method 1: Using Counter
from collections import Counter
counter = Counter(s)
for ch in s:
    if counter[ch] == 1:
        print(ch)
        break
# Output:
# c
```
# 15. Count the Occurrence of Each Word in a Sentence
```python
sentence = "python is good python is easy"
### Method 1: Without Built-in Functions
words = sentence.split()
freq = {}
for word in words:
    if word in freq:
        freq[word] += 1
    else:
        freq[word] = 1
print(freq)
# Output:
# {'python': 2, 'is': 2, 'good': 1, 'easy': 1}

### Method 1: Using Counter
from collections import Counter
print(Counter(words))
# Output:
# Counter({'python': 2, 'is': 2, 'good': 1, 'easy': 1})
```
# 16. Find the Intersection of Two Lists
```python
list1 = [1, 2, 3, 4, 5]
list2 = [3, 4, 5, 6, 7]
### Method 1: Without Built-in Functions
intersection = []
for num in list1:
    if num in list2 and num not in intersection:
        intersection.append(num)
print(intersection)
# Output:
# [3, 4, 5]

### Method 1: Using Set Intersection
result = list(set(list1) & set(list2))
print(result)
# Output:
# [3, 4, 5]
```
# 17. Move All Zeros to the End of a List
```python
nums = [1, 0, 2, 0, 3, 0, 4]
### Method 1: Without Built-in Functions
result = []
zero_count = 0
for num in nums:
    if num == 0:
        zero_count += 1
    else:
        result.append(num)
for i in range(zero_count):
    result.append(0)
print(result)
# Output:
# [1, 2, 3, 4, 0, 0, 0]

### Method 1: Using List Comprehension
non_zero = [x for x in nums if x != 0]
zeros = [0] * nums.count(0)
print(non_zero + zeros)
# Output:
# [1, 2, 3, 4, 0, 0, 0]
```
# 18. Find the Longest Substring Without Repeating Characters
```python
s = "abcabcbb"
### Method 1: Sliding Window
start = 0
max_len = 0
seen = {}
for end in range(len(s)):
    if s[end] in seen and seen[s[end]] >= start:
        start = seen[s[end]] + 1
    seen[s[end]] = end
    current_len = end - start + 1
    if current_len > max_len:
        max_len = current_len
print(max_len)
# Output:
# 3

### Method 1: Using Set
left = 0
right = 0
unique = set()
max_len = 0
while right < len(s):
    while s[right] in unique:
        unique.remove(s[left])
        left += 1
    unique.add(s[right])
    max_len = max(max_len, right - left + 1)
    right += 1
print(max_len)
# Output:
# 3
```
# 19. Find the Maximum Occurring Element in a List
```python
nums = [1, 2, 2, 3, 4, 2, 5, 3]
### Method 1: Without Built-in Functions
freq = {}
for num in nums:
    if num in freq:
        freq[num] += 1
    else:
        freq[num] = 1
max_element = None
max_count = 0
for key in freq:
    if freq[key] > max_count:
        max_count = freq[key]
        max_element = key
print(max_element)
# Output:
# 2

### Method 1: Using Counter
from collections import Counter
result = Counter(nums).most_common(1)
print(result[0][0])
# Output:
# 2
```
# 20. Implement the Two Sum Problem
```python
nums = [2, 7, 11, 15]
target = 9
### Method 1: Brute Force
for i in range(len(nums)):
    for j in range(i + 1, len(nums)):
        if nums[i] + nums[j] == target:
            print([i, j])
# Output:
# [0, 1]

### Method 1: Hash Map
lookup = {}
for i, num in enumerate(nums):
    diff = target - num
    if diff in lookup:
        print([lookup[diff], i])
        break
    lookup[num] = i
# Output:
# [0, 1]
```
# 21. Check if a Number is Prime
```python
n = 17
### Method 1: Without Built-in Functions
is_prime = True
if n <= 1:
    is_prime = False
else:
    for i in range(2, n):
        if n % i == 0:
            is_prime = False
            break
print(is_prime)
# Output:
# True

### Method 1: Optimized Approach
is_prime = True
if n <= 1:
    is_prime = False
else:
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            is_prime = False
            break
print(is_prime)
# Output:
# True
```
# 22. Generate All Prime Numbers Within a Range
```python
start = 1
end = 20
### Method 1: Basic Approach
for num in range(start, end + 1):
    if num > 1:
        is_prime = True
        for i in range(2, num):
            if num % i == 0:
                is_prime = False
                break
        if is_prime:
            print(num, end=" ")
# Output:
# 2 3 5 7 11 13 17 19

### Method 1: Optimized Approach
for num in range(start, end + 1):
    if num > 1:
        is_prime = True
        for i in range(2, int(num ** 0.5) + 1):
            if num % i == 0:
                is_prime = False
                break
        if is_prime:
            print(num, end=" ")
# Output:
# 2 3 5 7 11 13 17 19
```
# 23. Find Whether a Number is an Armstrong Number
```python
n = 153
### Method 1: Without Built-in Functions
temp = n
total = 0
while temp > 0:
    digit = temp % 10
    total += digit * digit * digit
    temp = temp // 10
print(total == n)
# Output:
# True

### Method 1: Generalized Armstrong Logic
num = str(n)
power = len(num)
total = sum(int(digit) ** power for digit in num)
print(total == n)
# Output:
# True
```
# 24. Find the Longest Common Prefix Among Strings
```python
strs = ["flower", "flow", "flight"]
### Method 1: Character Comparison
prefix = ""
for i in range(len(strs[0])):
    ch = strs[0][i]
    for word in strs[1:]:
        if i >= len(word) or word[i] != ch:
            print(prefix)
            exit()
    prefix += ch
print(prefix)
# Output:
# fl

### Method 1: Using Sorting
strs.sort()
first = strs[0]
last = strs[-1]
result = ""
for i in range(min(len(first), len(last))):
    if first[i] == last[i]:
        result += first[i]
    else:
        break
print(result)
# Output:
# fl
```
# 25. Flatten a Nested List
```python
nested = [[1, 2], [3, 4], [5, 6]]
### Method 1: Without Built-in Functions
flat = []
for sublist in nested:
    for item in sublist:
        flat.append(item)
print(flat)
# Output:
# [1, 2, 3, 4, 5, 6]

### Method 1: List Comprehension
flat = [item for sublist in nested for item in sublist]
print(flat)
# Output:
# [1, 2, 3, 4, 5, 6]
```
# 26. Find the Kth Largest Element in a List
```python
nums = [3, 2, 1, 5, 6, 4]
k = 2
### Method 1: Without Built-in Functions
arr = nums.copy()
for i in range(len(arr)):
    for j in range(0, len(arr) - i - 1):
        if arr[j] > arr[j + 1]:
            arr[j], arr[j + 1] = arr[j + 1], arr[j]
print(arr[-k])
# Output:
# 5

### Method 1: Using Built-in Functions
result = sorted(nums, reverse=True)[k - 1]
print(result)
# Output:
# 5
```
# 27. Implement a Stack Using a List
```python
### Method 1: Using List Operations
stack = []
stack.append(10)
stack.append(20)
stack.append(30)
print(stack.pop())
# Output:
# 30

### Method 1: Stack Class
class Stack:
    def __init__(self):
        self.items = []
    def push(self, value):
        self.items.append(value)
    def pop(self):
        return self.items.pop()
s = Stack()
s.push(10)
s.push(20)
s.push(30)
print(s.pop())
# Output:
# 30
```
# 28. Implement a Queue Using a List
```python
### Method 1: Using List
queue = []
queue.append(10)
queue.append(20)
queue.append(30)
print(queue.pop(0))
# Output:
# 10

### Method 1: Using deque
from collections import deque
queue = deque()
queue.append(10)
queue.append(20)
queue.append(30)
print(queue.popleft())
# Output:
# 10
```
# 29. Find Pairs in an Array Whose Sum Equals a Target Value
```python
nums = [1, 2, 3, 4, 5]
target = 6
### Method 1: Brute Force
for i in range(len(nums)):
    for j in range(i + 1, len(nums)):
        if nums[i] + nums[j] == target:
            print((nums[i], nums[j]))
# Output:
# (1, 5)
# (2, 4)

### Method 1: Using Hash Set
seen = set()
for num in nums:
    diff = target - num
    if diff in seen:
        print((diff, num))
    seen.add(num)
# Output:
# (2, 4)
# (1, 5)
```
# 30. Find the Maximum Subarray Sum (Kadane's Algorithm)
```python
nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
### Method 1: Brute Force
max_sum = float("-inf")
for i in range(len(nums)):
    current_sum = 0
    for j in range(i, len(nums)):
        current_sum += nums[j]
        if current_sum > max_sum:
            max_sum = current_sum
print(max_sum)
# Output:
# 6

### Method 1: Kadane's Algorithm
current_sum = nums[0]
max_sum = nums[0]
for num in nums[1:]:
    current_sum = max(num, current_sum + num)
    max_sum = max(max_sum, current_sum)
print(max_sum)
# Output:
# 6
```
