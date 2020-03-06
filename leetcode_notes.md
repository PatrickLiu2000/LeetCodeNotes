# LeetCode Notes
[Coderust: Hacking the Coding Interview](https://www.educative.io/courses/coderust-hacking-the-coding-interview)
https://github.com/bephrem1/backtobackswe
https://www.youtube.com/user/tusharroy2525
# Arrays
## Binary Search
- know that `(left + right) / 2` can cause integer overflow - use `(right - left) / 2 + left` instead
    - know iterative/recursive solution better
    - remember to update mid pointer
    - KEY ALGO IN A LOT OF ARRAY SEARCHING
## Maximum in Sliding Window
- first tried iterative solution - worked, but need to realize there is a lot of repeated work - reading same element from array multiple times
- think about what data structure can store data properly; in this case, deque was perfect because we needed to be able to add and remove from the front and back of a list quickly
- know the stack and queue methods (both can be used in deque)
    - stack:
        - push and pop: add/remove from top of stack
    - queue:
        - add: adds to end of queue
        - offer: adds to queue
## Search In Rotated Sorted Array
- Go with your gut, think about best possible runtime
- Knew that we had to use binary search
- think about the different possible cases that can happen when doing binary search
    - check if a side is strictly increasing = have we found the pivot point

## Rotating Array
- just know the trick 4Head-don't bang ur head against a wall, just look at solution
- simply reverse entire array, then first k elements, then the rest

## Move Zeros Right
- use a 2 pointer strategy- 1 to keep track of zero index, 1 to iterate through all elements
    - swap if element is not zero

## Quicksort
- first call partition - picks an element to be the pivot (moves elements less than it to left, more than it to right)
    - either move pivot to the end of the array or pick the last element to be pivot
    - keep 2 pointers i and j
    - i keeps track of last element of left side (values less than pivot)
    - j explores to compare value to pivot
    - swap i and j if value at j is less than pivot (swap tail of last item less than the pivot), then increment i
    - always increment j
    - return i+1 to be index of pivot
- job of j is to put items less than pivot back to i
- [backtobackswe/Quicksort.java at master · bephrem1/backtobackswe · GitHub](https://github.com/bephrem1/backtobackswe/blob/master/Sorting%2C%20Searching%2C%20%26%20Heaps/Quicksort/Quicksort.java)
- basically 2 recursive calls itself on the left and right side of pivot

## Overlapping Intervals
- when thinking about overlapping intervals with start and end times, preprocess data - create array of start times, array of end times, and sort them accordingly
    - if next start time is greater than previous end time,  merge the intervals
    - else, put current interval as-is

## Two Sum
- take advantage of the fact that you know there is only 1 distinct solution
- use hashmap with keys as values of the array, and value as index of array
- search hashmap by seeing if there contains the `target - currentvalue` key
# LinkedLists
## Reverse LinkedList
- iterative: 3 pointers - prev, cur, next
    - store next value; set `cur.next = prev`, and advance all pointers
    - once you reach end, set prev to head (because cur is at the end null value) 
- recursive way: 
    - base case: return last node of list
    - recursive step: have a "reversed" part of list, and current node you need to add to reversed list; set the current node's next node's next value to the current node (because the current node's next node technically is the previous node in the reversed list), then set the current node's next to null (because it's at the end of the reversed list now), then return the head of the entire reversed part of the list
## Delete Node Given a the Node to be deleted
- simply copy next value into current, and set current's next to current's next.next
## Insertion Sort LinkedList
- again, use cur, previous, and next pointer
- create new list by using dummy node
## Intersection of 2 LinkedLists
- must realize there is no possible faster solution than `O(n)`

## Remove Nth Node From End of List
- 2 pointer logic
- again, when you see remove, need a prev pointer, and to remove, set prev.next = cur.next.next
## Swap Pair Nodes
- cannot have faster soln than O(n)
- realize that you need pointer to 3 nodes 
- whenever you want to make a new list, create dummy node and simply return dummy.next 
## Merge 2 Sorted Lists
- make dummy node list
- advance pointers for list1 and list2 only when they have been added to combined list
- watch out for last node

## Rotate List
- simply make array circular by connecting head and tail, and the interate to pivot point and make it the head, while making the previous node's next null
- watch out for edge cases - k == 0 or length of list

## Reverse Every K nodes
- simply have a check to see if counter is a multiple of k, keep track of beginning and end of the current interval, and reverse the interval

## LinkedList Deep Copy with Random Pointers
- to deep copy, simply do `new Node(node.value)`
- use hashmap to have constant access to cloned node given the original node

# Math Problems

## Next Permutation
- https://www.youtube.com/watch?v=quAS1iydq7U
- do a case analysis - how is the next permutation generated?
- the must swap the element before a strictly decreasing section with the maximum in that decreasing section, then reverse the section to become increasing

## Pythagorean triplets
- given array, see if there are elements i,j,k such that $a^2+b^2=c^2$
## Combination Sum
- since solution asks for `all` possible combinations, think backtracking
- iterate through decision space by solving all possible combinations that include current element in array
- recursive step is to add current value to combo list, and subtract current value from target
- base case-if the remaining target value is less than 0, simply return - means current combo doesn't match
- if combo matches, then current remaining target value = 0; add the current combination to list

## Missing Number
- know geometric series of sum of 0 to n: $\frac{n(n+1)}{2}$
- subtract difference from current sum of array ez
## Permute String
- another backtracking problem
- decision space: characters that make up given string
- constraints: no constraints, just cannot use same character twice
- goal/base case: if current string is same as given string length
## Subsets
- yay backtracking
- make sure to sort the array!
- decision space - numbers in array given
- constraints - no constraints
- goal - simply add every element you come across
## Valid Number
- dumb question, if asked, literally just skip
## Square Root
- use binary search
- watch out for integer overflow
# String Problems
## Reverse Words Within Sentence
https://leetcode.com/problems/reverse-words-in-a-string/
- reverse string, reverse words, then trim whitespace

# Trees
## Same Trees
- case analysis
    - if both nodes are null, we have reached end of comparison; return true
    - if only 1 node is null, we know they are not the same; return false
    - if vals match, return true
    - recursive step; conpare 1st's trees' left to 2nd trees' left, and 1st trees' right to 2nd trees' right

## Inorder traversal
- recursive
    - base case: if node is null, return
    - recurse on left node, add node to list , then recurse on right node
- iterative -
    - instead of using recursive stack, use data structure
    - add keep adding left nodes to stack until reach null
        - once you reach null, pop off of the stack, add it's value to traversal list, then go to right node
## Level Order Traversal - N-nary Tree
- use queue, and add root then while queue is not empty, iterate through the respective level's nodes (using the current queue's size)
## Valid BST
- set lower and upper bounds (null initially), making them tighter and tighter as your recourse down children
# Backtracking 
https://www.youtube.com/watch?v=Zq4upTEaQyM&t=609s
- identifying backtracking problems: when they ask for "all" or "generate all possible" solutions
- overall blueprint: iterate through decision space by solving a subproblem (example: solving a tile on a sudoku board) 
- make a choice, and see if constraints are satisfied, then recurse on that decision
- find goal-which is our base case
- make sure to remove our decision if it doesn't satisfy the constraints