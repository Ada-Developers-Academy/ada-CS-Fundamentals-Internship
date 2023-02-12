# Recursion Review
<!-- Insert video here -->

## Learning Goals
 - Review recursion
 - Understand how to write recursive functions

## Vocabulary

| Term      | Definition |
|---        |---         |
| Recursion | A problem solving technique in which a function calls itself repeatedly on smaller versions of the original input to solve the overall problem|
| Bottom-Up | An approach to problem solving where smaller subproblems are solved, then combined to find a complete solution | 
| Top-Down  | An approach to problem solving where in whichthe problem is solved by breaking apart the overall problem into smaller subproblems |

## Overview

Before we dive deeper into different categories of algorithms, it may be helpful to review a technique often used when devising algorithms, including divide and conquer and dynamic programming algorithms: **recursion**. 

Recall from the classroom phase that recursive functions are functions which call themselves. For example, the function `hello_crash` prints the string `"Hello, crash!"` and then invokes itself. 

```python
def hello_crash():
    print("Hello, crash!")
    hello_crash()
```
By invoking itself, the function body will execute again - printing `"Hello, crash!"` then calling itself yet again. The invocation at end of the function body causes the function to run in an endless cycle, until eventually the program crashes. 

### Iteration vs Recursion

Like iteration, recursion is an way of repeatedly executing a piece of code. In fact, recursion and iteration achieve the same goal (repetition) but with inverse approaches.

Iteration uses a **bottom-up** approach. This means that we start by solving the smallest subproblem (ex. printing `"Hello, crash!"` once) and use the solutions to the subproblems to work our way up to the overall problem solution (ex. printing `Hello, crash!"` an infinite number of times).

In contrast, recursion uses a **top-down** approach. It takes the overall problem and breaks it apart into smaller and smaller subproblems until it finally finds one it can solve readily. Then, if necessary, it follows the same pattern as iteration of using the subproblems to build back up to the overall solution.

The difference is subtle. Let's compare the two approaches more closely with an example problem. Say we want to  modify our function `hello_crash` so that it no longer crashes. Instead of trying to print `"Hello, crash!"` an infinite number of times, let's instead alter the function so that it prints `"Hello"` `num` times, where `num` is an integer parameter. 

<table>
    <tr>
        <th> Iterative Approach </th>
        <th> Recursive Approach </th>
    </tr>
    <tr>
        <td>
        <pre>
def hello_repeat_iterative(num):
    i = 1
    while i <= num:
        print(f"Hello {i}!")
        i += 1
        </pre>
        </td>
        <td>
        <pre>
def hello_repeat_recursive(num):
    print(f"Hello {num}!")
    if num == 1:
        return
    else:
        hello_repeat_recursive(num - 1)
        </pre>
        </td>
    </tr>
    <tr>
        <td>
            Input: <code>5</code><br>
            Output:<br>
            <code>"Hello 1!"</code><br>
            <code>"Hello 2!"</code><br>
            <code>"Hello 3!"</code><br>
            <code>"Hello 4!"</code><br>
            <code>"Hello 5!"</code><br>
        </td>
        <td>
            Input: <code>5</code><br>
            Output:<br>
            <code>"Hello 5!"</code><br>
            <code>"Hello 4!"</code><br>
            <code>"Hello 3!"</code><br>
            <code>"Hello 2!"</code><br>
            <code>"Hello 1!"</code><br>
        </td>
    </tr>
    <tr>
        <td> Try it yourself: <a href = "https://replit.com/@adadev/hellorepeatiterative">hello repeat iterative</a></td>
        <td> Try it yourself: <a href = "https://replit.com/@adadev/hellorepeatrecursive">hello repeat recursive</a></td>
    </tr>
</table>

Notice that with the iterative approach, we use a loop to repeat code. We initialize a loop control variable `i` to value `1` and work forward, _repeating the loop body_ which _increments_ `i` until we reach our final value of `num` which stops the repetition.

In contrast, the recursive implementation uses recursive function calls to work backwards. We start with the original `num` value of 5, and with each recursive invocation of `hello_repeat_recursive` _decrement_ `num` and _repeat the function body_ until num is assigned to value `1`. When num has value `1`, we exit our function with a `return` statement instead of making another recursive call, thus ending the cycle of repetition.

 A recursive function should always have two basic components. The first is the **base case** which is our _end condition_. In other words, the base case is the condition under which we want to stop making recursive calls. If is our function returns a value, the base case usually returns the answer to the subproblem which cannot be solved without simply providing the answer. In our example function, our base case is when `num` is assigned value `1`. Since our program is not returning any values (just printing), the body of our base case is a simple `return` statement.


 The second component in a recursive function is the **recursive case**. The code we execute in the recursive case will run for all subproblems (including the overall problem) that do not match the base case. It includes invoking our function again, but passing in a simpler, smaller input/subproblem. With each subsequent recursive invocation of the function, we should be moving closer to our base case. In our example function, with each recursive call to `hello_repeat_recursive` we pass in `num - 1`, moving us closer to the base case where `num == 1`. The initial input passed in to a recursive function is often similar to the loop's end condition in the matching iterative function. 

```python
def hello_repeat_recursive(num):
    # print Hello whether num is 1 or something else
    print(f"Hello {num}!")

    # base case
    if num == 1:
        return
    # recursive case
    else:
        hello_repeat_recursive(num - 1)

```

<!-- available callout types: info, success, warning, danger, secondary, star  -->
### !callout-info

## Strengthening Recursive Coding Skills

Struggling with recursion? If you are trying but struggling to come up with a recursive implementation, see if you can implement an iterative solution first. Then try transforming your iterative implementation into a recursive implementation. 

### !end-callout


### Why use recursion? 

Looking at the above example, we may . Iteration achieves the same result. 

## Expanding Our Recursion Toolbox

There are a variety of subtechniques we can use to help us devise recursive algorithms to a wider array of problems. 

### Combining Results

Our first recursive example `hello_repeat` was a simple case of doing the exact same action repeatedly. What we wanted to print with the first call to `hello_repeat` (print `"Hello!"`) wasn't any different than what we wanted to do with the nth recurisve call to `hello_repeat` (also print `"Hello!"`). 

But often what we want to do in one recursive call depends on the results of other recursive calls. This is most often the case when we are using recursive function calls to solve subproblems then combining their results to find the solution to the overall problem. 

For example, say we want to sum numbers 0...n where n is a non-negative integer. The iterative solution is pretty straightforward:

```python
def sum_zero_to_n_iterative(n):
    sum = 0
    for num in range(n+1):
        sum += num
    return sum
```

We create an accumulator variable `sum` with an initial value of 0. Then we iterate over numbers 0...n adding each number to `sum` as we go. Once we finish iterating, we simply return `sum`.

In general, the pattern for the iterative solution is to find the sum of 0...1, then the sum of 0...2, then the sum of 0...3, and so on - continuing the pattern until we eventually find the target sum, the sum of 0...n. 

How could we implement this same function recursively? Observe that the sum of numbers 0...n is the same as the sum of numbers n...0. In other words, we can solve this problem backwards (top-down with recursion) as easily as we can solve it forwards (bottom-up with iteration). 

What does it look like to solve this problem 'backwards'? If we flip the pattern we observed in the iterative solution, we get that the sum of n...0 is n itself plus the sum of n-1...0. For example if we passed in `n=5`, we could observe that the sum of 5...0 is the same as 5 + 4...0. We can continue this pattern (ex. the sum of 4...0 is 4 + 3...0) until all we're left to sum is 0 with... nothing. 

The fact that we have nothing left we can sum with 0 is a good indication that `n == 0` is our end condition or base case. With this function, we would actually like to return a value. The value we would like to return is the sum of 0...n, but in this case n _is_ 0, so the sum we should return is 0. 

Let's write out our recursive function so far:

```python
def sum_zero_to_n_recursive(n):
    # base case
    if n == 0:
        return 0
``` 

<!-- available callout types: info, success, warning, danger, secondary, star  -->
### !callout-info

## 'Base Case' in the Iterative Solution

Notice that we still have to provide the answer directly when we do this function iteratively. We set our accumulator variable `sum` to 0. Otherwise, we have no initial value to sum with the subsequent numbers we iterate over. In the case that the input passed into the function is 0, the iterative solution will just return the intial value of `sum` which is also 0. 

### !end-callout

Our recursive case can be handled by generalizing the pattern we observed above: the sum of n...0 is the same as the sum of n + n-1...0. This is true whether n is 5 or some other value. So in our recursive case, we want to sum our current input of `n` with the result of calling our `sum_zero_to_n` function on a subproblem: `n-1`.

This sum is also what we want to return in the recursive case because it represents the sum of 0 to `n`. It is very common in recursive problem, that the recursive case will return the result of some operation between the current input and the return value of a recursive call.

```python
def sum_zero_to_n_recursive(n):
    # base case
    if n == 0:
        return 0
    # recursive case
    else:
        return n + sum_zero_to_n_recursive(n-1)
```

#### The Call Stack

When we make function calls, the body of the called function may invoke other functions which may themselves invoke even more functions. Recall that to keep track of a chain of function calls, the computer uses a **call stack**.

The call stack is a stack data structure that stores function calls. When we invoke a function, that function call is added to the top of the stack as a new element. When the function call finishes executing, it is popped off the top of the stack.

<!-- available callout types: info, success, warning, danger, secondary, star  -->
### !callout-info

## What's a stack?

A **stack** is a special type of array in which items are inserted and removed from the array like a stack of plates. When we insert a new plate onto the stack, we add it to the top of the stack. When we remove a plate, it also comes off the top of the stack. 

Think of the end of the array as the top of the stack - new elements are appended to the end of the array and taken from the end of the array. We never insert or remove elements from any other index in the array. For this reason, stacks are commonly referred to as Last-In-First-Out (LIFO) data structures because the last element to be inserted is the first one to come out of the array.

### !end-callout

Below we can see the call stack for our `sum_zero_to_n` recursive implementation. With each recursive function call, a new element or frame is added to the top of the stack. When we reach our base case, we finally stop adding recursive calls to the stack and `sum_zero_to_n(0)` finishes executing in full. It returns `0` and gets popped off the stack. We then go back to our previous recursive call `sum_zero_to_n(1)` and finish executing this function call by combining `1` (n) with the result of our base case. It gets removed from the stack and we continue the pattern with the next element at the top of the stack until the stack is empty and we have the answer to `sum_zero_to_n(5)`!
![sum_zero_to_n call stack](images/call-stack-sum-zero-to-n.gif)


### Multiple Base Cases

Fibonacci is a good example here. 

### Multiple Recursive Cases
Name in a phone book example 
 
### Using Helper Functions
Sum but with other functions


## The Call Stack


## Summary


