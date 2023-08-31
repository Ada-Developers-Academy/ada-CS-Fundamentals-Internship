# Introduction to Algorithms

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?pid=97e5271b-1f70-4acf-ae40-afb1005116f5&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=true&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## Learning Goals

By the end of this lesson you should be able to:

- Explain the term algorithm
- Further explain time and space complexity
- Further explain recursion
- Explain two categories of algorithms: _divide and conquer_ and _dynamic programming_


### !callout-danger

## How to Approach This Topic

This topic contains review on several topics previously covered in classroom. We recommend first doing a quick skim of each topic and completing each of the included exercises to refamiliarize yourself with the topic. 

After skimming all of the topics, go back and do a closer read of topics you need extra review on. Included in your re-review should be a close reading of dynamic programming.

### !end-callout



## What is an Algorithm?

Before we can discuss different algorithmic strategies, we need to understand what an algorithm _is_.  An **algorithm** is a finite set of instructions that, if followed, accomplishes a particular task.  We can think of it as a series of steps to accomplish a task.  For example, Google Maps has an algorithm to calculate the best route to drive between any two points on a map.  

All algorithms must have:

- Input
  - An algorithm may accept zero or more inputs
- Output
  - An algorithm should produce some result
- Clarity
  - Each step in an algorithm should be a clear and unambiguous
- Finiteness
  - An algorithm should end after a finite number of steps. 
  - An algorithm cannot repeat forever (otherwise it doesn't solve a problem)
- Effectiveness
  - It should be possible for a person or computer to fulfill each step in an algorithm and the algorithm should accomplish the given task.

### Areas of Study

The study of computer science is the study of algorithms. At its core, computer science is really the art of devising, analyzing, proving the correctness of, and testing algorithms:

- **Devising** algorithms
  - This is the art of using data structures and design strategies to develop new and useful algorithms
  - It also encompasses optimizing and generalizing existing algorithms
- **Validating** algorithms
  - This is the art of proving the correctness of an algorithm for all possible inputs
  - This is very similar to a mathematical proof
- **Analyzing** algorithms
  - This is identifying the efficency of an algorithm using time and space complexity
- **Testing** algorithms
  - This is really debugging the algorithm  
  - When the algorithm is tested, it is run on sample data. If the tests produce unexpected output, the error causing the unexpected output needs to be debugged
  - Algorithms are also _profiled_ or assessed on their performance measurements by running the algorithm on sample data and measuring performance changes and memory usage.
    - For example [leetcode](https://leetcode.com/) takes your solution to a common programming problem and compares its performance to solutions from other developers

This course will focus on devising, analyzing, and, testing algorithms. We are choosing to focus on these three aspects because they are the skills most often evaluated during technical interviews for junior software developer roles. Validating algorithms is beyond the scope of this course, but feel free to follow your curiosity!

## Devising and Testing Algorithms
Devising algorithms is really just problem solving. So how do we approach solving a new, knotty problem? What steps can we take when we sit down in front of a programming problem and... have no idea what to do? This lesson describes a systematic approach to problem solving. Notice the similarity to Problem Solving Exercises. In follow-up lessons, we will practice using Big-O notation to compare multiple approaches to the same problem.  


## Vocabulary and Synonyms

Vocab | Definition | Synonyms | How to Use in a Sentence
:-----:|:-----:|:-----:|:-----:
Nominal Case | A "normal" or typical input to an application. | normal case, typical case| I used `x=5` as the nominal case.
Edge Case | An input that is at the extreme of the allowable range of inputs. |extreme case| I used `x=0` as an edge case.


### Steps in Problem Solving

When we look at programming problems - either interview problems or challenges encountered on the job - we can approach the task systematically. Let's examine one particular strategy which involves first ensuring we understand the problem followed by breaking down the larger problem into smaller, more approachable steps and solving each step in turn. Then, we will examine our solution, evaluate how effective it is and attempt to improve upon it.

Our steps are:

* Understand the problem
* Explore Examples
* Break Down the Problem
* Solve or Reduce the Problem
* Simplify/Refactor

These steps are adapted from [George Pólya](https://en.wikipedia.org/wiki/George_P%C3%B3lya) a 20th century mathematician who wrote a book called [How to solve it](https://www.adasbooks.com/book/9780691164076) about how to go about solving math problems.

### Sample Problem

We will walk through the steps of solving a problem using the following sample problem:

*Write a function `duplicates_within_k` that takes in an unsorted list of integers that may contain duplicate elements and a number `k`.*  

*The function should return `True` if the array contains duplicates within k distance and `False` otherwise.*

### Understand the Problem

When we look at a given problem we need to understand what our code is expected to do.  Without solid understanding of our requirements, we might write code which does not fully address the problem or even write a solution to a different problem entirely!

#### Interview Problems

In an interview problem like `duplicates_within_k` we need to carefully examine the question and ask the interviewer follow-up questions to make sure we understand what is expected.

In this interview problem we can examine the problem statement and figure out that we need to:

* Write a function named `duplicates_within_k`
* The function should take in an unsorted list of integers as well as an integer `k`
* The function should return `True` if any integer appears twice or more in the list within `k` indices of each other and `False` if there are no duplicate integers within `k` indices. 

Restating the problem statement in our own words can help us find any points of confusion we have about the problem. We might have clarifying questions about what the input or output should be. For example, can `k` be larger than the length of the given list? If so, what should we return?

We should also look for any terminology that is unfamiliar to us (say if we're not sure what is meant by the word `duplicate`) and use Google or other resources to learn its meaning.

### !callout-star

## What if Google isn't allowed?

If you are in an interview setting and Google isn't allowed, ask your interviewer! While it may feel nervewracking to admit you are unfamiliar with a term (or multiple terms), asking for clarification can also signal that you are a clear communicator, collaborative, and detail-oriented.

### !end-callout

####  Summarizing Our Understanding

So in this problem we need to write a function `duplicates_within_k` which takes in a list of integers and a separate integer `k` and will return a boolean indicating whether or not the same integer occurs multiple times within `k` indices of the input list.

### Explore Example Input/Output

Next to ensure we understand the problem we need to develop example inputs and determine what the output *should* be for those given inputs.  In industry this might involve drawing mock-ups of the program and running through scenarios or asking a customer or a team member to do so.  It could also involve generating sample input data and determining what the output should be.

While we want to ensure our algorithm will work on typical input or **nominal cases**, it is also very important to develop a few examples which will test the boundaries of what is possible for input.  These are called **edge cases**.

We should consider:
* **Truthy Nominal Case**
  * In this example we could give a list that contains one integer that occurs twice within the given distance `k`.
  * For example: an input list of `[1, 0, 2, 1, 3, 4]` and `k` value 5 would return `True` because the integer 1 occurs twice: once at index 0 and once at index 3 which is within 5 indices.
* **Falsy Nominal Case**
  * In this example we could give a list where no integers occur twice within the given distance. 
  * For example: an input list of `[1, 0, 2, 1, 3, 4]` and `k` value 1 would return `False` because while 1 occurs twice in the given list, their distance from each other is greater than 1
* **Input List Edge Case**
  * In this example we could give an input list on the edge of what is possible. 
    * For example: an empty input list `[]` and any value of `k` would need to return *something* to indicate that it is not possible for there to be duplicates when the list is empty.  
    * Another example: an input list of `[1]` and any value of `k` needs to return *something* to indicate that it is not possible for there to be duplicates when there is only one element in the list.
* **K Edge Case**
  * This would be an input on the edge of what is possible for our integer value `k`
  * For example: given any input list and a `k` value of 0 would need to return *something* to indicating either that `k` must be greater than one or that it is not possible for there to be duplicates within 0 distance of each other (because 0 distance means we can only be looking at a single element)
  
By looking at concrete sample input and output examples, we can see that our problem is not as simple as it seems. We need to consider cases where we have a list with less than two elements or `k` is zero. 

For our purposes we will expect the function to return `False` if the length of the list is less than two or if `k` is zero. In an interview setting, consider asking your interviewer if there is a preferred return value when the algorithm encounters the edge case scenarios. If there is no preferred return value, make a thoughtful decision about what the algorithm should return and communicate your choice to your interviewer.

<!-- available callout types: info, success, warning, danger, secondary, star  -->
### !callout-star

## Devising and Testing Go Hand in Hand

These sample inputs and outputs make **excellent** test cases to use when verifying the algorithm we devise. Creating tests for an algorithm is often an integral step in helping us devise our algorithm!

### !end-callout

### Break Down the Problem

Big massive problems are *hard*.  As developers it is often easier to break down the problem into smaller, easier to understand steps.  This also helps us make an application more modular, testable and maintainable.  Clearly not all problems need to be broken up, but most substantial problems in interviews and in the workplace do.

How could you break up our sample problem?  Answer and then check the explanation below.

### !challenge

* type: paragraph
* id: 819220a4-080c-4818-a984-29766400d819
* title: What subproblems do you see?

##### !question

How would you break down the problem into two or more subproblems?

##### !end-question

##### !placeholder

##### !end-placeholder
##### !hint
When you think about attempting to solve this problem, what about it seems difficult to you? Where are you getting stuck? 

Feeling stuck often means you've found a subproblem you need to solve!
##### !end-hint

##### !explanation

Sample subproblems could be:

1.  Finding all sublists of size `k+1`. An element + the next k elements in the list means each sublist we are interested in sublists of size `k+1`.
2.  Determining if a single sublist has duplicate elements.

##### !end-explanation

### !end-challenge

### Solve or Reduce the Problem

Once a problem is understood and broken into more manageable pieces we can then solve the problem.

Write your solution and then look below to see a sample solution.

### !challenge

* type: code-snippet
* language: python3.6
* id: 4dc81336-1c2d-421e-8fe8-27326736b2e3
* title: Duplicates within K Problem
* points: 1
* topics: python, lists, hashtables

##### !question

Write a function called `duplicates_within_k` that takes in a list of integers numbers, `numbers`, and an integer `k`.

The function should return `True` if the same integer occurs multiple times within `k` distance. It should return `False` otherwise.

Spend no more than 15 minutes working through this independently. Use the hints below or reach out for help if you are still feeling stuck after 15 minutes.

##### !end-question

##### !placeholder

```py
def duplicates_within_k(numbers, k):
    '''
    INPUT: list of integers and integer k
    OUTPUT: Boolean indicating whether there is are duplicate elements in the list within k distance
    '''
    pass

```

##### !end-placeholder

##### !tests

```py
import unittest
from main import *

class TestPython1(unittest.TestCase):
  def empty_list_returns_false(self):
    self.assertEqual(False,duplicates_within_k([], 3))

  def test_list_with_only_one_number_returns_false(self):
    self.assertEqual(False,duplicates_within_k([0], 3))

  def test_nominal_truthy_case(self):
    self.assertEqual(True,duplicates_within_k([1, 0, 2, 1, 3, 4], 5))

  def test_nominal_falsey_case(self):
    self.assertEqual(False, duplicates_within_k([1, 0, 2, 3, 4, 1], 4))

  def test_duplicate_exactly_k_spaces_away_returns_true(self):
    self.assertEqual(True, duplicates_within_k([1, 0, 2, 1, 3, 4],4))

  def test_returns_true_when_not_first_subarray(self):
    self.assertEqual(True, duplicates_within_k([5,6,2,0,3,0,1],2))

  def test_returns_false_no_dupes_k_larger_than_list(self):
    self.assertEqual(False, duplicates_within_k([1,2,3,4,5,6],7))

  def test_returns_true_dupes_k_larger_than_list(self):
      self.assertEqual(True,duplicates_within_k([1,1,3,4,5,6],7))
  
  def test_false_when_k_is_0(self):
      self.assertEqual(False,duplicates_within_k([1,1,3,4,5,6],0))
```

##### !end-tests

<!-- other optional sections -->
##### !hint 
Start by solving each subproblem. Then see if you combine the solutions to each subproblem to come up with an overall solution. 

Still feeling stuck? Try watching the video walkthrough of a sample solution below:
<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=0300a58b-3411-466b-89b4-afb1000e153b&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=true&interactivity=all" height="360" width="640" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

##### !end-hint 
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

A sample solution could be:

```py
  def duplicates_within_k(numbers, k):
    '''
    INPUT: list of integers and integer k
    OUTPUT: Boolean indicating whether there is are duplicate elements in the list within k distance
    '''
    # get length of input list
    lst_length = len(numbers)

    # if the input list has less than two elements or k is zero
    if lst_length < 2 or k == 0:
      # return false, there cannot be duplicates
      return False
    
    # loop through indices of list
    for i in range(lst_length):
      # initialize a second pointer to track end of subarray
      j = i + 1
      # initialize a variable to k
      # will help make sure our subarray stays within size k + 1
      dist_remaining = k
      
      # while we are within k distance from i
      # and j is not out of bounds of list
      while dist_remaining > 0 and j < lst_length:
        # if elements at index i and j are the same
        if numbers[i] == numbers[j]:
          # a duplicate within k distance exists
          return True
        # otherwise increment j to increase subarray size
        j += 1
        # decrement dist_remaining so subarray will stay within
        # k distance from i
        dist_remaining -= 1
    # if we loop through all subarrays and have not found a duplicate
    # return False
    return False

```


##### !end-explanation

### !end-challenge

<details style="max-width: 700px; margin: auto;">
  <summary>Click here to see a sample solution</summary>

  The solution below works, but as we will see later below, it is not optimal.  We can do better.

  ```py  def duplicates_within_k(numbers, k):
    '''
    INPUT: list of integers and integer k
    OUTPUT: Boolean indicating whether there is are duplicate elements in the list within k distance
    '''
    # get length of input list
    lst_length = len(numbers)

    # if the input list has less than two elements or k is zero
    if lst_length < 2 or k == 0:
      # return false, there cannot be duplicates
      return False
    
    # loop through indices of list
    for i in range(lst_length):
      # initialize a second pointer to track end of subarray
      j = i + 1
      # initialize a variable to k
      # will help make sure our subarray stays within size k + 1
      dist_remaining = k
      
      # while we are within k distance from i
      # and j is not out of bounds of list
      while dist_remaining > 0 and j < lst_length:
        # if elements at index i and j are the same
        if numbers[i] == numbers[j]:
          # a duplicate within k distance exists
          return True
        # otherwise increment j to increase subarray size
        j += 1
        # decrement dist_remaining so subarray will stay within
        # k distance from i
        dist_remaining -= 1
    # if we loop through all subarrays and have not found a duplicate
    # return False
    return False

  ```
</details>

This solution works and is a relatively direct straight forward approach. This is often called a **brute force** solution.

### Simplify/Refactor

The first big challenge in software development is to _produce working code_. If we still have time after producing working code, we should consider opportunites to simplify or refactor (improve) our solution.

In the sample solution above we are using a nested loop to repeatedly traverse the list. The outer loop tracked the starting index of our subarrays and the inner loop tracked the ending index of our subarrays. This solution isn't very time efficient because we examine the same elements of the list repeatedly.

<!-- add visualization if time allows -->

Is it possible that an alternative approach can help us achieve simpler or more efficient code? Recall that for this problem we came up with the following subproblems:

1. Finding all subarrays of size `k + 1`
2. Determining whether a single subarray contains duplicates

In our current approach we work through a single subarray and check as we move through that subarray whether it contains duplicates. Then we repeat the process with the next subarray. 

Ideally, it would be nice to find all subarrays by only making a single loop through our input array. But if we eliminate the second loop in our current implementation, we no longer update the value that tracks the end index of our subarrays.

What if we flipped our approach so that instead of first confirming we are within a subarray of length k and then checking whether it contains duplicates, we instead track the indices of every value in our array and use arithmetic to see if any value with more than two instances is less than k?

For this approach, we could pair elements in the array with the indices at which they occur using a dictionary. We know dictionaries are also called hashtables, and that hashtables have very fast look-up times!

Say we have an input list `[1, 0, 2, 1, 3, 4]` and k value of 5. We could generate the dictionary:
```python
{
  0: [1],
  1 : [0, 3],
  2 : [2],
  3: [4],
  4: [5]
}
```
In the dictionary above the key is an element occuring in the input list and the value is a list of indices at which that element occurs.

We can see that the key 1 has multiple indices paired with it - 0 and 3 - indicating that it occurs in our input list at least twice.

If we find the difference between the two indices `3-0=3` we will find that `3 < 5` where 5 is the value of k. Thus we can see that the value 1 occurs multiple times within the distance k.

To make our hash table, we'll only have to look at each element in the list once, so this approach should be more efficient than our original solution!

#### Implementing Our Refactor

In our refactor we can start by creating a dictionary that maps sums to indices. We track the following values:

* `elt_to_idx_map` - dictionary mapping element values from the input list to their corresponding indices 
  
Then we can repeat this algorithm for each index in the list:

1. Check if the element already exists in the dictionary
2.  If the element is already in the dictionary, we've found a duplicate. 
3. Find the difference between our current index and the index already in the dictionary for that value
4.  If the difference is less than or equal to `k`, return `True`
5.  Otherwise, add the current element-index pair to the dictionary

Note that this improves on our proposed refactor even more! Instead of creating the dictionary first, and then checking for duplicates within the dictionary we check for duplicates as we iterate through the list.

Instead of storing a list of all indices associated with a value, we only store the most recent index seen for that value.

**Practice**:  Go back to the exercise above and try to implement the refactor.  Spend no more than 10 minutes on it.

<details style="max-width: 700px; margin: auto;">
  <summary>Click here to see a sample solution</summary>

  A detailed walkthrough of this solution is included in the last video lesson.

  ```py
    
  def duplicates_within_k(numbers, k):
    '''
    INPUT: list of integers and integer k
    OUTPUT: Boolean indicating whether there is are duplicate elements in the list within k distance
    '''

    # if the input list has less than two elements or k is zero
    if len(numbers) < 2 or k == 0:
      # return false, there cannot be duplicates
      return False

    # create a dictionary to store (element, index) pairs
    elt_to_idx_map = {}

    # loop through indices and values of input list
    for index, element in enumerate(numbers):
      # if the element has been seen previously
      if element in elt_to_idx_map:
        # if the difference between current index
        # and index already in the dictionary 
        # is less than or equal to k
        if index - elt_to_idx_map[element] <= k:
          # there exists a duplicate within distance k
          return True
      # pair most recently seen index with element in dictionary
      elt_to_idx_map[element] = index

    # there are no duplicates within distance k
    return False
        
  ```
</details>

This solution now makes only one pass through the list, meaning as the input array grows, the solution will perform better compared to our original solution. The video lesson contains a more detailed walkthrough of the sample refactored solution above.

## Summary

In this lesson we have walked through a general approach to problem solving.  By breaking the approach into a set of steps we can systematically approach problems in computer science.

The steps we created are:

* Understand the problem
* Explore Examples
* Break Down the Problem
* Solve or Reduce the Problem
* Simplify/Refactor

By making problem solving a process we can reduce stress and improve our ability to work toward solutions.


<!-- available callout types: info, success, warning, danger, secondary, star  -->
### !callout-star

## Should I Be Concerned if I Couldn't Come Up with a Solution Myself?

As you move through the unit curriculum, you will be asked to attempt many interview practice problems, many of which you may not be able to solve quickly or independently. 

That's okay! Part of the learning process for interviewing includes attempting and 'failing' problems, especially when you're first learning new material. Your progress may be slow and incremental. If you need to use provided and/or outside resources to come to a full solution, focus on understanding the _techniques_ used in the solution. You can bring these techniques with you to help solve future programming problems. 

### !end-callout

