# Divide and Conquer

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?pid=04387545-7ced-4c84-9ce4-ad44002bde36&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&start=0&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## Goals

As developers, we need as many tools to solve problems as possible.

When we understand the _kind_ of solution or algorithm we are using or can use, we can more easily read and understand it.

There are a number of solutions and algorithms classified as using the divide-and-conquer approach. Learning about divide-and-conquer approaches will:

- Help us identify divide and conquer algorithms
- Help us think about, design, and write divide and conquer solutions

## Overview

**Divide and Conquer** is an approach to problem solving that breaks down a large problem into multiple, smaller subproblems. We use the results of those subproblems to solve the original problem.

When we write a divide-and-conquer solution we can follow these steps:

1. Break the problem into subproblems of the same type
1. Recursively solve the subproblems
1. Combine the solved subproblems to solve the larger problem

This name is sometimes applied to algorithms that only need to solve a single, reduced subproblem without the need to combine any results.

This sounds very similar to a recursive algorithm! In this case, the distinction between a general recursive algorithm, and one that might be called "divide and conquer," is largely based on how much we're able to divide the original problem at each recursive step.

For example, if we are working with a list and are only able to remove a single element at each recursive step, we are unlikely to call such a solution a divide-and-conquer algorithm. But if at each recursive step we can reduce the size of the list by half, we might call that solution a divide-and-conquer algorithm.

## Terms

| Term               | Definition                                                                                                                                                                                                                                                                                                             | How to Use in a Sentence                                                                                                   |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Divide and Conquer | An algorithm design strategy based on multi-branched recursion. We recursively break down a problem into two or more subproblems of the same or related type, until these become simple enough to be solved directly. The solutions to the subproblems are then combined to give a solution to the original problem. | "If multiple subproblems can be combined to solve a larger problem, we might try to apply a divide-and-conquer solution." |
| Pivot              | An element used in QuickSort to divide the array into two sections, one section less than the pivot and the other greater than the pivot. The choice of the pivot has enormous implications for the efficiency of QuickSort.                                                                                            | "We should be careful about how we pick the pivot so that we avoid worst-case performance for our typical inputs."                                  |

## Example: QuickSort

QuickSort is an algorithm which takes a divide-and-conquer approach to sorting an array by using the following steps:

1. If the array is only one element or empty, we are done, the array is sorted.
1. Pick an element from the array as the _pivot_.
1. Move all elements smaller than the pivot to the left and all elements larger than the pivot to the right. Note that the pivot is now in the correct index. Picking a pivot and rearranging the elements is referred to as _partitioning_.
1. Perform QuickSort on the left and right sides of the pivot.

![QuickSorting the array (7, 3, 9, 1, 6, 8, 2, 5) where the pivot is chosen by taking the last element in the array. The first pivot is 5, which after rearranging gives the array (3, 1, 2, 5, 6, 8, 9, 7). The left array (3, 1, 2) and right array (6, 8, 9, 7) are QuickSorted. 2 is selected as the pivot, and after rearranging, the left array becomes (1, 2, 3). The left and right arrays are (1) and (3), which are both 1 element, meaning they are sorted. Returning to (6, 8, 9, 7), 7 is picked as the pivot. After rearranging, the array becomes (6, 7, 9, 8). The left array is (6), which is sorted. The right array is (9, 8). 8 is selected as the pivot. After rearranging, the array becomes (8, 9). There is no left array, and the right is (9), which is sorted. All subarrays have been sorted, meaning the whole array is sorted, having become (1, 2, 3, 5, 6, 7, 8, 9).](images/algorithmic-strategies_divide-and-conquer_quick-sort.png)  
_Fig. Tracing through an application of QuickSort in which the final element in a subarray is chosen as the pivot._

In terms of divide and conquer, we pick a pivot and move smaller elements to the left, and larger elements to the right. This leaves us with two smaller subproblems: sorting the elements on the left, and those on the right. We call QuickSort on each side.

If the pivot is relatively well chosen we will divide the list _log n_ levels deep, and shift at most _n_ elements with each level of division, arriving at a _O(n log n)_ runtime.

### Weakness of QuickSort: The Pivot

Again, QuickSort is _O(n log n)_ **if** the pivot is well-chosen. If the pivot does not break the list into two relatively equal subarrays, it will not arrive at a _O(n log n)_ runtime. Instead, it will approach a _O(n<sup>2</sup>)_ runtime.

For example, if with each iteration the pivot is the smallest remaining element in an array, rather than splitting the array into approximately _n/2_ sized pieces, instead we have one subarray of size _n-1_.

<br />

<details>

<summary>The example implementation provided here uses the approach of taking the final element as the pivot, then gradually growing the smaller list from the left side of the non-pivot elements.</summary>

```python
def quicksort(array, low=0, high=None):
    if high is None:
        high = len(array)

    # if the array has 0 or 1 elements, it's already sorted
    if high - low <= 1:
        return

    # partition the current list to find where one element goes
    partition_pos = partition(array, low, high)

    # sort the left and right sides
    quicksort(array, low, partition_pos)
    quicksort(array, partition_pos + 1, high)

def partition(array, low, high):
    # take the last item as the pivot
    last = high - 1
    pivot = array[last]

    # assume pivot will end up at the start
    # conceptually, this position marks the end of the smaller list
    p_index = low

    # iterate over the values not including the pivot
    i = low
    while i < last:
        # if the current value should be to the left of the pivot, swap
        # this value to the potential pivot location and advance that
        # location. conceptually this adds the value to the end of the
        # smaller list and tracks the new end of this list
        if array[i] < pivot:
            temp = array[i]
            array[i] = array[p_index]
            array[p_index] = temp
            p_index += 1
        i += 1

    # swap the pivot value to the end of the smaller list. after this
    # swap, we know that all values to the left of the pivot are smaller,
    # and all values to the right of the pivot are greater or equal
    temp = array[i]
    array[i] = array[p_index]
    array[p_index] = temp

    return p_index
```

</details>

### !callout-info

## Partitioning Is the Key

There are a variety of strategies for selecting the pivot, and for how to rearrange the elements around the pivot. We will not go into further detail about them here, but follow your curiosity!

### !end-callout

## Example: Merge Sort

Merge sort is another divide-and-conquer algorithm. It involves the following three stages:

1. _Divide_ the array into two subarrays at each step until each subarray is of size one.
2. _Sort_ each subarray with the merge sort algorithm. (An array of size one is trivially sorted.)
3. _Merge_ the subarrays into one array by combining two subarrays into one at each step.

This process is usually done by keeping track of three indices in the array: _starting index_, _ending index_ and _midway index_ as shown in the image below.

![Merge sort example. The list starts with the values (7, 2, 8, 1, 6, 5, 3, 9) (s=0, m=4, e=8). This is split into to lists with one having (7, 2, 8, 1) (s=0, m=2, e=4), and the other having (6, 5, 3, 9) (s=4, m=6, e=8). Each list of four values is split into two lists of 2 value, resulting in 4 total lists. (7, 2) (s=0, m=1, e=2), (8, 1) (s=2, m=3, e=4), (6, 5) (s=4, m=5, e=6), and (3, 9) (s=6, m=7, e=8). Finally, each list of two is split into two single item lists for a total of 8 single item lists. (7) (s=0, e=1), (2) (s=1, e=2), (8) (s=2, e=3), (1) (s=3, e=4), (6) (s=4, e=5), (5) (s=5, e=6), (3) (s=6, e=7), (9) (s=7, e=8). Now each array has only a single value, making it implicitly sorted. The individual subarrays are merged so that they preserve their sorted property by combining them into a temporary array, then copying the sorted values over the merged range until the entire array becomes sorted.](images/algorithmic-strategies_divide-and-conquer_merge-sort.png)  
_Fig. Example run of merge sort showing the index calculations used to split and merge the arrays. Note the convention used of the end index being exclusive._

As we can see in the image above, in the first _divide_ step, the original array of size eight gets divided into two subarrays of size four each. This is done by setting the _starting index_ to _0_, the index of the first element in the array, and the _ending index_ is set to one past the last element in the array, using the convention of the ending index being exclusive. The _midway index_ is then computed using the formula:

<div style="margin:auto;width:fit-content;">

_midway index_ = ⌊(_starting index_ + _ending index_) / 2⌋

</div>

Where ⌊⌋ denotes the mathematical _floor_ operation, or integer truncation.

### Divide

For the first _divide_ step, the _midway index_ will be _(0+8)/2_ = _4_.

In the next _divide_ step, we have two subarrays, one ranging in index from _0_ to _4_ and the other ranging in index from _4_ to _8_.

At this point, the subarrays are not yet of size one. So, the same action gets repeated to compute the _midway index_. This _divide_ stage continues until the original array of size _n_ is reduced to subarrays of size _1_ each.

A subarray of size one is trivially sorted, since there can be no elements out of place relative to the single value in the array.

### Sort and Merge

The _merge_ stage starts by combining two sorted subarrays at a time.

While combining the subarrays containing _7_ and _2_ respectively, the value in each is compared, the smaller value, i.e. _2_, is written to the lower index, and the higher value, i.e. _7_, is written to the higher index.

Larger merges would continue by comparing the values to be merged element by element, taking the smaller until one subarray is "empty." At that point, the remainder of the other array can be copied over!

### !callout-info

## Copying and Merging Arrays

How do we efficiently merge two arrays? An auxiliary array of size _n_ is often used to facilitate the merge steps, after which the values are copied from the auxiliary array back to the original array.

### !end-callout

The two-way merging continues until there are no more subarrays and the original array is completely sorted.

### Divide and Conquer Complexity in Merge Sort

Since merge sort always divides the list in half at each divide step, there will be _log n_ levels in the division phase. By keeping data in place, and only adjusting indices to keep track of where the subarrays are located, at each level, there are at most _n_ calculations, for a time complexity of the division phase of _O(n log n)_.

In the merge phase, there will still be _log n_ levels of mergers, and at each level of the merge, there are _n_ copies from the split arrays into the auxiliary array, and _n_ copies back into the original array, giving a total complexity for the merge phase of _O(2n log n)_.

Combining the divide and merge phases, we get a total complexity of _O(3n log n)_, which after dropping the coefficient gives us _O(n log n)_.

<br />

<details>

<summary>We can view an example of merge sort making use of index tracking by expanding this section.</summary>

```python
def merge_sort(array, low=0, high=None):
    if high is None:
        high = len(array)

    # if the array has 0 or 1 elements, it's already sorted
    if high - low <= 1:
        return

    # find the midway point where we will divide
    mid = (low + high) // 2

    # apply merge sort to each half of the array
    merge_sort(array, low, mid)
    merge_sort(array, mid, high)

    # merge the sorted left and right subarrays
    merge(array, low, mid, high)

def merge(array, low, mid, high):
    merged = []
    l = low
    r = mid

    # continue merging by comparison until one subarray is empty
    while l < mid and r < high:
        # take either the left or right value
        if array[l] <= array[r]:
            merged.append(array[l])
            l += 1
        else:
            merged.append(array[r])
            r += 1

    # if there was data remaining in the left array take the rest
    while l < mid:
        merged.append(array[l])
        l += 1

    # or if there was data remaining in the right array take the rest
    while r < high:
        merged.append(array[r])
        r += 1

    # copy from the auxiliary array back to the main array
    m = 0
    l = low
    while l < high:
        array[l] = merged[m]
        l += 1
        m += 1
```

</details>

## Example: Binary Search (Decrease-and-Conquer)

Binary search can be considered a decrease-and-conquer algorithm because it decreases the size of the array by half with each step. No matter how large the original array was, at each step we'll be able to discard half the remaining data from consideration! The half-sized array will then be analyzed with the same step as the full-sized array.

Binary search is technically not considered a divide-and-conquer algorithm but instead a decrease-and-conquer algorithm because divide-and-conquer algorithms typically have *two or more* subproblems which are generated from the main problem. In contrast, the binary search algorithm decreases to one sub-problem.

Here's a description of the binary search algorithm:

1. Starting with a sorted array, we check whether it contains a particular value by comparing the search value with the element in the middle of the array.
1. If we find the value we return the position where it was found.
1. If we don't find the value, we determine whether it would be in the left or right half of the array by seeing whether it is smaller or larger than the middle element. Remember, we can make this decision because _we assume the array is sorted!_ Then we perform a binary search on the selected half.
1. If at any point, we end up with an empty range, we know the value was not in the array, and we can return a result indicating the value was not found, such as `None`. Other variations of binary search may return the index of where the value _should_ have been, but as a negative value to indicate that it was missing.
1. Each recursion divides the array in half and performs the binary search on a smaller subproblem.

![Performing binary search for the value 5 in the sorted list (1, 2, 3, 5, 6, 7, 8, 9). Looking for 5. Check the value at the midway index (s=0, m=4, e=8). 5 is less than 6. Adjust the ending index to rule out the right half. Check the value at the updated midway index (s=0, m=2, e=4). 5 is greater than 3. ADjust the starting index to rule out the left half. Check the value at the updated midway index (s=3, m=3, e=4). The value, 5, was found. Return the position, 3.](images/algorithmic-strategies_divide-and-conquer_binary-search.png)  
_Fig. Looking for the position of the value 5 in a sorted array using binary search._

<br />

<details>

<summary>We can view a recursive implementation of binary search by expanding this section.</summary>

```python
def recursive_binary_search(array, to_find, low=0, high=None):
    if high is None:
        high = len(array)

    if high <= low:
        return None

    mid = (high + low) // 2

    if array[mid] == to_find:
        return mid
    elif array[mid] > to_find:
        high = mid
    else:
        low = mid + 1

    return recursive_binary_search(array, to_find, low, high)
```

</details>

## Check for Understanding

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 645bad5d-af5f-42a9-a7e4-c70412972ab1
* title: Time Complexity of Quicksort

##### !question

What is the *Worst-Case* time complexity for Quicksort?

##### !end-question

##### !options

a| O(NlogN)
b| O(N)
c| O(N<sup>2</sup>)

##### !end-options

##### !answer

c|

##### !end-answer


##### !explanation

The worst-case time complexity for Quicksort is O(N<sup>2</sup>) because picking the worst pivot (e.g. the smallest or biggest remaining element) for each step will result in one array of size n-1 as opposed to two arrays that are approximately n/2 in length.

##### !end-explanation 

### !end-challenge

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: checkbox
* id: 25522151-56d9-4495-9691-da53700f896e
* title: Divide and Conquer Algorithms

##### !question

Select all of the following which would be considered Divide/Decrease and Conquer algorithms.

##### !end-question

##### !options

a| Mergesort
b| Dijkstra's Algorithm
c| Insertion sort
d| Quicksort
e| Binary Search

##### !end-options

##### !answer

a|
d|
e|

##### !end-answer

#### !explanation

Dijkstra's Algorithm is not considered a divide and conquer algorithm because at no point are we breaking the problem into subproblems of the same type and recursively solving the subproblems.
<br>

Similarly, <a href="https://www.geeksforgeeks.org/insertion-sort/">Insertion Sort</a> is not a divide and conquer algorithm because the algorithm does not involve breaking down the problem into subproblems.

#### !end-explanation 

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

## Summary

Divide and conquer is an algorithmic strategy which involves breaking down a large problem into easier-to-solve subproblems.

In a divide and conquer solution we break a large problem into one or more smaller subproblems and then use the solution to the subproblems to solve the larger problem.

## Resources

- [Wikipedia: Divide & Conquer](https://en.wikipedia.org/wiki/Divide-and-conquer_algorithm)
- [Daniel Liang's Binary Search Animation](https://yongdanielliang.github.io/animation/web/BinarySearchNew.html)
- [Geeks for Geeks: Python Program for QuickSort](https://www.geeksforgeeks.org/python-program-for-quicksort/)
- [hackerearth: QuickSort Animation](https://www.hackerearth.com/practice/algorithms/sorting/quick-sort/visualize/)
