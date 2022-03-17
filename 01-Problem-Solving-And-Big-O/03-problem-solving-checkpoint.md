# Problem Solving & Big O Exercise

Answer the following questions.  **Pay particular attention when you are asked about either space or time complexity.**

### !challenge

* type: short-answer
* id: 8f9ce926-298f-42e5-bf3a-8354d752063e
* title: Why is Big O important?
* points: 1
* topics: Big O

##### !question

Why is Big O important?

##### !end-question

##### !placeholder

Why use Big O

##### !end-placeholder

##### !answer

/.+/

##### !end-answer

##### !hint

Why don't we just time our application, or count the number of operations a function does?

##### !end-hint

##### !explanation

Big O provides a standard and precise way to measure and compare how fast and memory intensive our code is.

##### !end-explanation

### !end-challenge

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 3f40c6ee-e651-4800-811a-46759ae9d5d0
* title: Even Elements
* points: 1
* topics: Big-O, time-complexity

##### !question

What is the *time complexity* of the following function?

```python
def only_even_elements(array):
    new_array = []
    for i in range(0, len(array)):
        if i % 2 == 0:
            new_array.append(array[i])

    return new_array
```

##### !end-question

##### !options

* O(1)
* O(n)
* O(log n)
* O(n^2)

##### !end-options

##### !answer

* O(n)

##### !end-answer

### !end-challenge

### !challenge

* type: multiple-choice
* id: b6e79e12-0746-4852-b8f0-30b88d214aad
* title: Even Elements
* points: 1
* topics: Big-O, space-complexity

##### !question

What is the *space complexity* of the following function?

```python
def only_even_elements(array):
    new_array = []
    for i in range(0, len(array)):
        if i % 2 == 0:
            new_array.append(array[i])

    return new_array
```

##### !end-question

##### !options

* O(1)
* O(n)
* O(log n)
* O(n^2)

##### !end-options

##### !answer

* O(n)

##### !end-answer

### !end-challenge

### !challenge

* type: multiple-choice
* id: 4dd37fb7-79b2-499b-867b-187df51bbdda
* title: Sum Digits
* points: 1
* topics: python, big-o, sum-digits, time-complexity

##### !question

What is the time complexity of the following function where `n` is the number passed in as a parameter?

```py
def sum_digits(n):
    total = 0
    while n > 0:
        total += n % 10 # get last digit
        n //= 10        # remove last digit
    
    return total
```

##### !end-question

##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n^2)

##### !end-options

##### !answer

* O(log n)

##### !end-answer

##### !hint

Remember `n` is the number passed in, not the number of digits.

##### !end-hint

##### !explanation

Because we *divide* n by 10 with each iteration of the loop the time complexity is logarithmic.  This is a case where the base of the logarithm is 10, instead of 2 (because we're dividing by 10 with each loop iteration).  If `n` is 57, the loop will execute 2 times.  If we make it a 4 digit number ~100 times bigger, 1057, the loop will execute 4 times.

##### !end-explanation

### !end-challenge

### !challenge

* type: multiple-choice
* id: a080d31c-03f6-46ff-9f4d-b601a5959730
* title: Subtotal List time complexity
* points: 1
* topics: python, big-o, time-complexity

##### !question

What is the *time complexity* of the following function?

```py
def subtotals_list(numbers):
    subtotals_list = []

    for i in range(0, len(numbers)):
        subtotal = 0
        for j in range(0, i + 1):
            subtotal += numbers[j]

        subtotals_list.append(subtotal)

    return subtotals_list
```

##### !end-question

##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n^2)

##### !end-options

##### !answer

* O(n^2)

##### !end-answer

### !end-challenge

### !challenge

* type: multiple-choice
* id: 3ebc656a-17a4-4aca-aff0-35acbc5a4ba9
* title: Subtotal List space complexity
* points: 1
* topics: python, big-o, space-complexity

##### !question

What is the *space complexity* of the following function?

```py
def subtotals_list(numbers):
    subtotals_list = []

    for i in range(0, len(numbers)):
        subtotal = 0
        for j in range(0, i + 1):
            subtotal += numbers[j]

        subtotals_list.append(subtotal)

    return subtotals_list
```

##### !end-question

##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n^2)

##### !end-options

##### !answer

* O(n)

##### !end-answer

### !end-challenge

### !challenge

* type: multiple-choice
* id: 2d6fbcb2-931a-4c2b-a5ea-f186515651fe
* title: Picking Between Solutions
* points: 1
* topics: python, big-o, time-complexity

##### !question

Consider the following solutions to a problem.  Which one is the best?

*Code Sample: Solution 1*

```py
def isAnagram(self, s: str, t: str) -> bool:
    s_list = []
    t_list = []
    s_list[:0] = s
    t_list[:0] = t
    
    for s_letter in s_list:
        if s_letter in t_list:
            t_list.remove(s_letter)
        else:
            return False
    
    return len(t_list) == 0
```

*Code Sample: Solution 2*

```py
def isAnagram(self, s: str, t: str) -> bool:
    s_freq_map = {}
    t_freq_map = {}
    if len(s) != len(t):
        return False
    
    for letter in s:
        if not s_freq_map.get(letter):
            s_freq_map[letter] = 0
        
        s_freq_map[letter] += 1
    
    for letter in t:
        if not t_freq_map.get(letter):
            t_freq_map[letter] = 0
        
        t_freq_map[letter] += 1
    
    for letter, count in s_freq_map.items():
        if t_freq_map.get(letter) != count:
            return False
    
    return True
```

##### !end-question

##### !options

* Solution 1
* Solution 2
* Both are the same

##### !end-options

##### !answer

* Solution 2

##### !end-answer

<!-- other optional sections -->
##### !hint

What are the time complexities of the two solutions?  Are there any hidden nested loops?

##### !end-hint

### !end-challenge

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: short-answer
* id: d8b19e21-8bc1-411a-9824-ab9c681566e6
* title: Why
* points: 1
* topics: python, big-o, time-complexity

##### !question

Why did you pick that answer?

##### !end-question

##### !placeholder

Why?

##### !end-placeholder

##### !answer

/.+/

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

* The 1st solution has an O(n^2) time complexity because it uses a hidden nested loop.  
* The 2nd solution has an O(n) time complexity

`if letter in t_list:` loops through `t_list` and it is nested inside a loop.  Furthermore, deleting a letter from `t_list` also require O(n) time because removing an element from a list requires a loop.

##### !end-explanation

### !end-challenge

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: paragraph
* id: 523a7217-6d47-4e80-8cff-01d4ec733b52
* title: Improving isAnagram
* points: 1
* topics: python, big-o, time-complexity, space-complexity

##### !question

Can you think of any better solution to this problem?  

What is the time complexity of the best solution you can devise?

##### !end-question

##### !placeholder

Can you think of any better ways to solve the problem?

Does the time/space complexity change with your solution?

##### !end-placeholder

### !end-challenge

## Optional Exercise

### !challenge

* type: code-snippet
* language: python3.6
* id: 16992c53-2608-47bd-a3d5-d5c310250328
* title: Using A sliding Window
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
<!-- * topics: [python, pandas] (optional the topics for analyzing points) -->

##### !question

The following solution **works**, but it is not efficient.  Try to improve it.

A string s is nice if, for every letter of the alphabet that s contains, it appears both in uppercase and lowercase. For example, "abABB" is nice because 'A' and 'a' appear, and 'B' and 'b' appear. However, "abA" is not because 'b' appears, but 'B' does not.

Write a function `longest_nice_substring(s)`. Given a string `s`, return the longest contiguous substring of `s` that is nice. If there are multiple substrings tied for the longest, return the substring of the earliest occurrence.

If there are none, return an empty string.

| <div style="width:100px">Input (`s`)</div>|<div style="width:100px">Output</div>|<div style="width:350px">Input (`s`)</div>|
|--|--|--|
|`"YazaAay"`|`"aAa"`|`"aAa"` is a nice string because `'A/a'` is the only letter of the alphabet in `s`, and both `'A'` and `'a'` appear.|
|`"Bb"`|`"Bb"`|`"Bb"` is a nice string because both `'B'` and `'b'` appear. The whole string is a substring.|
|`"c"`|`""`|There are no nice substrings.|

##### !end-question

##### !placeholder

```py
def is_nice_string(string):
    swapped = list(string.swapcase())
    original = list(string)

    for c in swapped:
        if c not in original:
            return False
    return True

def longest_nice_substring(s: str) -> str:
    longest_substring = ""
    for i in range(len(s)):
        for j in range(i+1,len(s)):
            current_substring = s[i:j+1]
            if is_nice_string(current_substring) and \
                    len(current_substring) > len(longest_substring):
                longest_substring = current_substring
    return longest_substring
```

##### !end-placeholder

##### !tests

```py
import unittest
from main import *

class TestPython1(unittest.TestCase):
    def test_example_1(self):
      self.assertEqual("aAa",longest_nice_substring("YazaAay"))

    def test_example_2(self):
      self.assertEqual("Bb",longest_nice_substring("Bb"))

    def test_example_3(self):
      self.assertEqual("",longest_nice_substring("c"))

    def test_example_empty_string(self):
        self.assertEqual("",longest_nice_substring(""))

    def test_example_AaBbxcCdDaA(self):
        self.assertEqual("cCdDaA",longest_nice_substring("AaBbxcCdDaA"))

```

##### !end-tests

### !end-challenge

The Challenge problem was taken from [leetcode](https://leetcode.com/problems/longest-nice-substring/).
