# Analysis of Algorithms

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?pid=aa72b06b-7af5-4ac7-8e60-afb20057bdf0&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=true&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## Learning Goals

By the end of this lesson we will be able to:

* Describe why we need Big O
* Define time and space complexity
* Evaluate the time & space complexity of a function

## Overview

When we analyze an algorithm we generally do not care how an algorithm performs on a specific input size.  Instead we look at how the runtime and memory usage changes as the input size grows.  Looking at how an algorithm's runtime and memory usage increases with increasing input is called, **Asymptotic Analysis**, i.e. Big O.

Why bother with asymptotic analysis?  Why bother with examining how an algorithm increases in runtime and memory usage as the input size grows?  Asymptotic analysis allows us to compare algorithms and select one over another.  It also allows us to judge if any algorithm will be able to solve a particular problem within a meaningful amount of time or within the system's limited storage capacity.

Most often, we measure things in terms of _worst-case_ performance of an algorithm.  This is important when response time and memory usage is critical like when managing a self-driving car or autopilot system.  There are also times where the _average-case_ performance is important, especially where an algorithm is run often or across many instances, like an analysis program run regularly on a cloud platform; the average runtime (and standard deviation) can be important for a task run thousands of times an hour.

<!-- Add graphs -->
| Big O            | English Term   |
|---               |---             |
| O(1)             | Constant       |
| O(log n)         | Logarithmic    |
| O(n)             | Linear         |
| O(n<sup>2</sup>) | Quadratic      |
| O(n<sup>3</sup>) | Cubic          |
| O(2<sup>n</sup>) | Exponential    |
| O(n!)            | Factorial      |

## Review of Big O Notation 

### Time Complexity

When we consider sample input to programming exercises like the type often asked in technical interviews, we usually consider relatively small inputs because they are easier for us to understand. Analyzing different algorithms on such small inputs, it can be difficult to understand why time complexity might matter. Even inefficient algorithms often perform well on small inputs. But as the size of the input `n` increases, the number of operations performed by the algorithm often also increases. *We care about how the trend in the number of operations changes with the size of the input*. We also attempt to estimate the worst-case scenario for the number of operations. Big O provides a way to measure and discuss how the worst-case scenario for the number of operations changes with the size of the input.

#### Constant Time Complexity

Some algorithms take essentially the same or _constant_ amount of time to run regardless of the size of the input. 

Consider the example below which returns the sum of numbers 1 through n. 

```py
def add_from_1_to_n(n):
    return (n * (n + 1)) / 2
```

<details style="max-width: 700px; margin: auto;">
  <summary>How does this solution work?</summary>

One alternative solution to this same problem would be to loop through the numbers from 1 to n and return the result:

`1  +   2  +  3  + ...  + (n-1)  + n`

We could rewrite the above expression in descending order as:

`n + (n-1) + ... +  3 +  2  + 1`

If we add both of the above expressions together, we get two times the sum we are looking for: 

```
   1    +    2    +    3    + ... + (n-1) + n
+  n    +  (n-1)  +  (n-2)  + ... +   2   + 1
----------------------------------------------
(n+1)   +  (n+1)  +  (n+1)  + ... + (n+1) + (n+1) <-- adds (n+1) n times

n * (n+1)
```
</details>

Notice that regardless of the size of n, we perform the same number of operations: Whether n is 1 or one million, we multiply its value by itself plus one, then divide the resulting product in half. 

In Big O terms, we can say an algorithm that perform essentially the same number of operations regardless of the size of the input has a **constant time complexity** or is `O(1)`. Note that `1` is a constant (not variable) value. 

#### Linear Time Complexity

On the other hand, for some algorithms, the amount of time it takes to run the algorithm is proportional to changes in the size of the input. A good example is a loop based version of our function that calculates the sum of numbers 1 through n.  

```py
def add_from_1_to_n(n):
    total = 0
    for i in range(1, n + 1):
        total += i

    return total
```

If the input size doubles, our function will take roughly double the time to run. We can see this in action by estimating the runtime on specific inputs. 

Imagine that assigning `total` to 0 takes 1 second, incrementing `i` takes 1 second, and adding `i` to the total also takes 1 second. Regardless of whether the n is 10 or 20, initializing `total` to 0 will take the same amount of time (1 second). But if n is 10, we will need to increment `i` 10 times (10 seconds) and add `i` to `total` 10 times (10 seconds) resulting in an overall runtime of 1 + 10 + 10 = 21 seconds. 

If n is 20, we will need to increment `i` 20 times (20 seconds) and add `i` to `total` 20 times (20 seconds) resulting in an overall runtime of 1 + 20 + 20 = 41 seconds.

A function where the runtime increases in direct proportion to the size of the input is a function  with **linear time complexity** or `O(n)`.

If we altered our algorithm slightly to instead use a loop to print all the numbers from 1 to n and then down from n to 1 it would take `O(n + n)` = `O(2n)` time to execute. For Big O, we drop any coefficients or constant terms. Thus `O(2n)` => `O(n)`.

```py
def count_up_and_down(n):
    # Takes n time to run
    for i in range(1, n + 1):
        print(i)
    
    # takes n time to run
    for i in range(n, 0, -1):
        print(i)
```

So although `count_up_and_down` may be doing more operations than `add_from_1_to_n` it also has a **linear time complexity** or `O(n)`. 

In general, whenever we do operations that are sequential (one after another) we add their time complexities together. If the time complexities being added are different, say an O(n) and O(1) operation (as opposed to the O(n) + O(n) operation in the example above), the less dominant (faster/better) time complexity is dropped. Thus `O(n + 1)` => `O(n)`.

#### Quadratic Time Complexity

Often we encounter algorithms which involve nested loops. For example the code below contains a for loop which runs n times and a loop nested inside of it which runs, worst-case, n-1 times where n is the length of `numbers`.

```py
def duplicates_within_k(numbers, k):
    lst_length = len(numbers)

    if lst_length < 2 or k == 0:
      return False
    
    for i in range(lst_length):
      j = i + 1
      dist_remaining = k
      while dist_remaining > 0 and j < lst_length:
        if numbers[i] == numbers[j]:
          return True
        j += 1
        dist_remaining -= 1
    return False
```

When we encounter nested loops or other nested operations, we multiply the time complexity of the inner loop by the number of iterations of the outer loop. 

So in this case:

* If we multiply the number of iterations the outer loop does by the number of iterations the inner loop does in the worst case we have `(n * (n-1))` which is equivalent to `(n^2 - n)`.
* We can drop the less significant term `n` because `n^2` will dominate the result. 
* We end up with a time complexity of `O(n^2)`.

This is called a **quadratic time complexity** or `O(n^2)`.

#### Logarithms

Sometimes algorithms may produce time complexities more sophisticated than quadratic or linear. For example, the following function will take `O(log n)` time.

```py
def binary_search(test_array, value):
    low = 0
    high = len(test_array) - 1
    while low <= high:
        mid = (low + high)//2
        if test_array[mid] > value:
            high = mid - 1
        elif test_array[mid] < value:
            low = mid + 1
        else:
            return mid

        if test_array[low] == value:
            return low

    return None
```

**What is a log again**?

A logarithm can be thought of as the inverse of an exponent. It is the power to which a fixed number (the base) must be raised to produce a given number. For example we say the log with base 2 of 8 is 3 because 2<sup>3</sup> = 8.  The log of base 10 of 10000 is 4 because 10<sup>4</sup> = 10000.

![Log example](images/problem-solving__log-example.png)

What does this mean practically speaking? In a coding problem, if we reduce the size of a problem by dividing the remaining input at a constant rate with each iteration we often get a time complexity involving a logarithm.

Taking an [example from Stack Overflow](https://stackoverflow.com/questions/2307283/what-does-olog-n-mean-exactly/2307314#2307314), a physical example of a logarithmic algorithm is:

```
Given a person's name, find the phone number by picking a random point 
about halfway through the part of the book you haven't searched yet, 
then checking to see whether the person's name is at that point. Then 
repeat the process about halfway through the part of the book where 
the person's name lies. (This is a binary search for a person's name.)
```


Indeed, the classical example of a logarithmic problem is binary search:

```py
def binary_search(numbers, value):
    low = 0
    high = len(numbers) - 1
    while low <= high:
        mid = (low + high)//2
        if numbers[mid] > value:
            high = mid - 1
        elif numbers[mid] < value:
            low = mid + 1
        else:
            return mid

        if numbers[low] == value:
            return low

    return None
```

If the input is eight elements [1, 2, 3, 4, 5, 6, 7, 8] and `value` we are searching for is 2:

* In the first iteration `low` will be 0 and `high` would be 7, and  `mid` would be 3 ( (0+7) / 2).
* On the second iteration `low` remains 0 and `high` becomes 2 and `mid` becomes 1.
* Then value is found in the list and the function returns 1.

Notice with each iteration the size of the input involved in the search (`low` to `high`) is halved. So worst-case a list of 8 items would take 3 iterations to find the value. We could double the size of `numbers` to 16 items and it would only take 4 iteration to find the value and for 32 items it would only take 5 iterations. Thus while the function *does* take longer as the input size increases it does not increase very rapidly.

In the worst case scenario, the algorithm will take the following number of iterations given the input of size `n`:

|   n	|   Number of iterations	|
|---	|---	                    |
|   8	|   3	                    |
|   16	|   4	                    |
|   32	|   5	                    |
|   64	|   6	                    |

*Table. Number of iterations for each input size.*

In general:

* If the size of the input is *divided* by some value with each iteration, the time complexity involves a logarithm with a base equal to the divisor.
* By far, the most common logarithmic base is 2 because our algorithms often, like binary search, divide the input size by two with each iteration.
  * However, we could have a different base such as 4 which would mean we are dividing the input size by 4 with each iteration
  * Often we drop the base of the logarithm on the assumption that it is 2.
  * For Big-O notation, we do not need to indicate the base.

#### Other Time Complexities

We will occassionally encounter algorithms that have other time complexities. Later in the course we will encounter algorithms which have exponential and factorial time complexities. Algorithms with these time complexities run extremely slow at even moderate inputs and for large inputs are effectively useless.

[![Time complexity chart](images/problem-solving__big-o-cheat-sheet.png)](https://www.bigocheatsheet.com/)

*Fig. From Big O Cheat Sheet*

We may also encounter time complexities which use variables other than `n`. One typical scenario for this is when we have multiple inputs, each with variable size, that both affect time complexity.

For example, say we have the following function which will make a 2D matrix with `rows` number of rows and `columns` number of columns where all values inside the matrix are initialized to `None`.

```python
def init_matrix(rows, columns):
    matrix = []
    for r in range(rows):
        matrix.append([])
        for c in range(columns):
            matrix[r].append(None)
    return matrix
```

We could say this algorithm has an **`O(m*n)` time complexity** where `m` is the number of rows and `n` is the number of columns. When discussing time complexity, we want to use separate variables to represent the number of rows and number of columns because their respective values could be drastically different. We could be trying to create a matrix with just 1 row and 1000 columns. 

Multiple variables is one reason it is very important that we clearly define what our Big O variables represent when discussing time and space complexity. When multiple variables are at play, we want to communicate clearly which ones are affecting the overall runtime and/or memory usage.

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: d5fd6476-897a-4690-a620-8c1f1a185852
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
* id: 552c0146-f390-4eac-a6a3-15365bae8233
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
* id: bcf1318d-c0ce-4436-a918-6d8b2f7f73bb
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
* id: 0099e250-1cb3-4540-a740-223186c00c0c
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

### Space Complexity

Space complexity measures the amount of memory an algorithm uses as it runs. Sometimes it can be called *auxiliary space* or *extra space* required by the algorithm beyond the space required by the input. 

The rules with regard to space complexity are:

* Most single-value variables take up constant space.
  * booleans, integers, floats, etc
  * Sometimes these are called *primitives*
* Strings take up O(n) space where n is the string length
* Lists take up O(n) space where n is the list length
* Dictionaries take up O(n) space where n is the number of key-value pairs

Consider the following function:

```py
def sum_up(numbers):
    total = 0
    for number in numbers:
        total += number

    return total
```

This function requires 2 numeric variables to store the total and the current number. We can say that the function requires 2 (i.e. *constant space*) to run or `O(1)`. The amount of memory used does not change as the length of `numbers` increases.

On the other hand the following function requires a list to store double all the numbers.

```py
def double_numbers(numbers):
    doubled = [num * 2 for num in numbers]

    return doubled
```

This function created a new list of numbers proportional in size to the input. So the space complexity is `O(n)`.

Now try to estimate time complexity for the following function.

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 8889dceb-5f2e-4192-9981-e8ce85fcf89e
* title: Estimate Space Complexity
* points: 1
* topics: python, space complexity

##### !question

What is the *space complexity* of the following function?

```py
def mystery_function(test_array, value):
    low = 0
    high = len(test_array) - 1
    while low <= high:
        mid = (low + high)//2
        if test_array[mid] > value:
            high = mid - 1
        elif test_array[mid] < value:
            low = mid + 1
        else:
            return mid

        if test_array[low] == value:
            return low

    return None
```

##### !end-question

##### !options

* O(1)
* O(log n)
* O(n)
* O(n^2)
* O(2^n)

##### !end-options

##### !answer

* O(1)

##### !end-answer

<!-- other optional sections -->
##### !hint

Is the function creating new lists or dictionaries?

##### !end-hint

##### !explanation

Because the function only creates 3 "primitive" variables no matter the size of the input list, the space complexity is `O(1)`.

##### !end-explanation

### !end-challenge
### !challenge

* type: multiple-choice
* id: 9e84ae63-2f27-47a9-8bf5-41192f7c3a7a
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
* id: a29ddd8c-4a9e-4fb9-a286-8d987b55fdb8
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


**Note on Recursion**

When we look at recursive functions, we also need to consider the call stack as part of the space complexity. For example the following function prints all the numbers from 1 to n, but because it makes another function call for each number from 1 to n, it requires `O(n)` space.

```py
def count_up(n):
    if n == 0:
        return
    
    count_up(n - 1)
    print(n)
```

This is because the Python interpreter needs to save every active function call on something called the *call stack* with all of it's local variables etc.

![Call Stack diagram](images/problem-solving__call-stack.svg)

*Fig. Call stack diagram*

We'll discuss how the recursive call stack affects space complexity more in future lessons.

## Summary

Big O is a standard way to measure how much the time an algorithm takes and how much memory an algorithm requires to run as the input size increases. This allows us to compare different solutions to measure them against each other. Big O is helpful in selecting the proper algorithm to use for a problem.

Some general rules to use when thinking about time and space complexity:

* Constants do not matter so `O(27)` = `O(1)` and `O(3n)` = `O(n)`
* Smaller terms do not matter so `O(n + 27)` = `O(n)` and `O(n^2 + 3n + 3)` = `O(n^2)`.
* Arithmetic operations are constant `O(1)`
* Variable assignment is constant `O(1)`
* Accessing an element in an array or a value in a dictionary by the key is constant `O(1)`
* In a loop the time complexity is the length of the outer loop multiplied by the time complexity of the loop body

## Categories of Algorithms

There are a [number of different categories of algorithms](https://s2.smu.edu/~vdebroy/cse3353/Lectures/Lecture-7/Algorithm-Types.pdf).  Each category describes the general approach to the algorithm's use in solving its particular problem.  Categories are not exclusive; an algorithm can be a member of multiple categories.  For example QuickSort can be both a divide and conquer algorithm and a randomized algorithm if it picks a random element as a pivot to sort against at each stage. Categories of algorithms can provide us with useful tips and techniques for devising algorithms to problems that fall within a category.

Next, we will look at two categories:  _divide and conquer_ algorithms and _dynamic programming_ algorithms.