
# DSA Problems
  - [Arrays](#arrays)
    - [1. Two Sum](#1-two-sum)
    - [2. Container with most water](#2-container-with-most-water)
    - [3. Trapping Rain water](#3-trapping-rain-water)
    - [4.  Find Common Characters](#4--find-common-characters)
  - [Strings](#strings)
    - [1. Typed out strings](#1-typed-out-strings)
    - [2. Longest Substring Without Repeating Characters (Medium)](#2-longest-substring-without-repeating-characters-medium)
    - [3. Palindromes](#3-palindromes)
    - [4. Split a String in Balanced Strings](#4-split-a-string-in-balanced-strings)
  - [Linked Lists](#linked-lists)
    - [1. Reverse a Linked List](#1-reverse-a-linked-list)
    - [2. M, N Reversals](#2-m-n-reversals)
    - [3. Flatten a Multilevel Doubly Linked List](#3-flatten-a-multilevel-doubly-linked-list)
    - [4. Cycle detecting in Linked List](#4-cycle-detecting-in-linked-list)
  - [Stacks](#stacks)
    - [1. Valid Parenthesis](#1-valid-parenthesis)
    - [2. Minimum Remove to Make Valid Parenthesis](#2-minimum-remove-to-make-valid-parenthesis)
  - [Queues](#queues)
    - [1. Implement Queue using Stacks](#1-implement-queue-using-stacks)
  - [Recursion(Sorting and Quickselect)](#recursionsorting-and-quickselect)
    - [1. Factorial](#1-factorial)
    - [2. Kth Largest Element in an Array](#2-kth-largest-element-in-an-array)
    - [3.  Binary Search](#3--binary-search)
    - [4.  Find First and Last Position of Element in Sorted Array](#4--find-first-and-last-position-of-element-in-sorted-array)
  - [2D Arrays](#2d-arrays)
    - [1. 2D Array(Matrix) traversal using DFS - Recursive Approach](#1-2d-arraymatrix-traversal-using-dfs---recursive-approach)
    - [2. 2D Array(Matrix) traversal using BFS - Recursive Approach](#2-2d-arraymatrix-traversal-using-bfs---recursive-approach)
    - [3. Number of Islands](#3-number-of-islands)
    - [4. Rotten Oranges](#4-rotten-oranges)
    - [5. Walls and gates](#5-walls-and-gates)
    - [6. Search a 2D Matrix](#6-search-a-2d-matrix)
    - [7. Set Matrix Zeroes](#7-set-matrix-zeroes)
    - [8. Transpose Matrix](#8-transpose-matrix)
  - [Binary trees](#binary-trees)
    - [1. Maximum Depth of Binary Tree](#1-maximum-depth-of-binary-tree)
    - [2. Binary Tree Level Order Traversal](#2-binary-tree-level-order-traversal)
    - [3. Binary Tree Right Side View](#3-binary-tree-right-side-view)
    - [4. Binary Tree Left Side View](#4-binary-tree-left-side-view)
    - [5.  Count Complete Tree Nodes](#5--count-complete-tree-nodes)
    - [6. Validate Binary Search Tree](#6-validate-binary-search-tree)
## Arrays  

### 1. Two Sum

[Q: Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.](https://leetcode.com/problems/two-sum/)

Logic: find the target-currentElement in the array is present in array, if yes return the indices, if not traverse again.

Brute Force Solution: Two nested for loops,  compare first element with other elements in the array.. and so on .. till we find the target [Repl](https://replit.com/@ZhangMYihua/two-sum-brute-force)

```javascript
const numsArray = [1, 3, 7, 9, 2];
const targetToFind = 11;


const findTwoSum = function(nums, target) {
  for(let p1 = 0; p1 < nums.length; p1++) {
    
    const numberToFind = target - nums[p1];

    for(let p2 = p1 + 1; p2 < nums.length; p2++) {
      if(numberToFind === nums[p2]) {
        return [p1, p2];
      }
    }
  }

  return null;
};

console.log(findTwoSum(numsArray, targetToFind));
```

Optimal Solution: Using hashmap, store the target-currentitem in hashmap, if it found return the value  [Repl](https://replit.com/@ZhangMYihua/two-sum-optimal-solution)

``` javascript
const numsArray = [1,3,7,9,2];
const targetToFind = 11;

const findTwoSum = function(nums, target) {
  const numsMap = {};
  
  for(let p = 0; p < nums.length; p++) {
    const currentMapVal = numsMap[nums[p]];

    if(currentMapVal >= 0) {
      return [currentMapVal, p];
    } else {
      const numberToFind = target - nums[p];
      numsMap[numberToFind] = p;
    }
  }

  return null;
}

console.log(findTwoSum(numsArray, targetToFind));
```

### 2. Container with most water

[Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of the line i is at (i, ai) and (i, 0). Find two lines, which, together with the x-axis forms a container, such that the container contains the most water.](https://leetcode.com/problems/container-with-most-water/)

Logic: find water between two points by calculating `water = Math.min(arr[i], arr[j]) * j-1` and then Maxwater= Math.max(maxwater, water) gives the max water container

Brute Force solution: Nested for loops [Repl](https://replit.com/@ZhangMYihua/maximum-water-container-brute-force-solution)

```javascript
const heightsArray = [4,8,1,2,3,9];

const getMaxWaterContainer = function(heights) {
  let maxArea = 0;

  for(let p1 = 0; p1 < heights.length; p1++) {
    for(let p2 = p1 + 1; p2 < heights.length; p2++) {
      const height = Math.min(heights[p1], heights[p2]);
      const width = p2 - p1;
      const area = height * width;
      maxArea = Math.max(maxArea, area);
    }
  };

  return maxArea;
}

console.log(getMaxWaterContainer(heightsArray));
```

Optimal solution:  two pointer solution, let p1 be the first item , p2 be the last item and traverse the elements using while loop. [Repl](https://replit.com/@ZhangMYihua/maximum-water-container-optimal-solution)

```javascript
const heightsArray = [4,8,1,2,3,9];

const getMaxWaterContainer = function(heights) {
  let p1 = 0, p2 = heights.length - 1, maxArea = 0;

  while(p1 < p2) {
    const height = Math.min(heights[p1], heights[p2]);
    const width = p2 - p1;
    const area = height * width;
    maxArea = Math.max(maxArea, area);
    
    if(heights[p1] <= heights[p2]) {
      p1++;
    } else {
      p2--;
    }
  }

  return maxArea;
}

console.log(getMaxWaterContainer(heightsArray));
```

### 3. Trapping Rain water

[Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.](https://leetcode.com/problems/trapping-rain-water/)

Logic: We need to find the water at a give point of element. let c be the current item.  maximum element of left side of c is maxLeft, and maximum element of right side of c is maxRight. and then water unit at that element can be calculated as `Math.min(maxLeft, maxRight) - arr[c]` where arr[c] is the current element height.

Brute force solution:  for loop is used to traverse all elements and while is used for find the maxRight and maxLeft [Repl](https://replit.com/@ZhangMYihua/trapping-rainwater-brute-force-solution#main.js)

```javascript
var heights = [0,1,0,2,1,0,1,3,2,1,2,1]

function getMax(heights){
 let total = 0;   

 for(let i=0; i<heights.length; i++){
  let maxL = 0;
  let maxR = 0;
  let right = i+1;
  let left = i-1;
  while(right < heights.length){
      maxR = Math.max(maxR, heights[right]);
      right++;   
  }
  while(left >= 0){
      maxL = Math.max(maxL, heights[left]);
      left--;
  }
  let waterunit = Math.min(maxL, maxR) - heights[i];
  total += waterunit < 0 ? 0: waterunit;
 }

 return total;
}

getMax(heights);
```

Optimal solution:using while loop and two pointers solution [Repl](https://replit.com/@ZhangMYihua/trapping-rainwater-optimal-solution)

```javascript
const getTrappedRainwater = function(heights) {

  let left = 0, right = heights.length - 1, totalWater = 0, maxLeft = 0, maxRight = 0;
  
  while(left < right) {
    if(heights[left] <= heights[right]) {
      if(heights[left] >= maxLeft) { 
        maxLeft = heights[left]
      } else { 
        totalWater += maxLeft - heights[left];
      }
      left++;
    } else {
      if(heights[right] >= maxRight) {
          maxRight = heights[right];
      } else {
          totalWater += maxRight - heights[right];
      }
        
      right--;
    }
  }

  return totalWater;
}
```

### 4.  Find Common Characters
[Given an array words of strings made only from lowercase letters, return a list of all characters that show up in all strings within the list (including duplicates).  For example, if a character occurs 3 times in all strings but not 4 times, you need to include that character three times in the final answer.You may return the answer in any order.](https://leetcode.com/problems/find-common-characters/)


```
Input: ["bella","label","roller"]
Output: ["e","l","l"]] 
```
Logic: From the given Array(A), we take the first item as the reference and add it to our result. then iterate all the items in the A.slice(1) and filter the result array by checking if char present in result is also present in the current item, then replace that char with empty string,and return    `return len > A[i] ` where len is the length of A[i] before performing operations.

Solution: [Leetcode](https://leetcode.com/submissions/detail/503044741/)
```javascript
var commonChars = function(words) {
    let result = [...words[0]];
    
    for(let i=1; i<words.length; i++){
        result = result.filter(char => {
            let len = words[i].length;
            words[i] = words[i].replace(char, "");
            return len>words[i].length;
        });
    }
    
    return result;
};
```

***

## Strings

### 1. Typed out strings

[Given two strings s and t, return true if they are equal when both are typed into empty text editors. '#' means a backspace character.
Note that after backspacing an empty text, the text will continue empty.
](https://leetcode.com/problems/backspace-string-compare/)

Logic: Using stacks. Traverse through the chars in the given string, if the current is not equal to "#" push it to the stack, and if it equals pop out the last element in the stack.

Brute force solution: [Repl](https://replit.com/@ZhangMYihua/typed-out-strings-brute-force#main.js)

```javascript
const backspaceCompare = (S, T) => convert(S) === convert(T);

const convert = String => {
    const temp = [];
    for(c of String){
        c !== "#" ?  temp.push(c) : temp.pop();
    }
    return temp.join("");
}
```

Optimal solution: Two pointer solution, initially p1 is pointing to lastelement in the firstArray, p2 is pointing to lastelement in the secondArray.. if p1 === p2 then increment the counters.[Repl](https://replit.com/@ZhangMYihua/backspace-string-compare-optimal)

```javascript
const string1 = "ab#z"
const string2 = "az#z"

var backspaceCompare = function(S, T) {
    let p1 = S.length - 1, p2 = T.length - 1;
    
    while(p1 >= 0 || p2 >= 0) {
        if(S[p1] === "#" || T[p2] === "#") {
            if(S[p1] === "#") {
                let backCount = 2;
                
                while(backCount > 0) {
                    p1--;
                    backCount--;
                    
                    if(S[p1] === "#") {
                        backCount += 2;
                    }
                }
            }
            
            if(T[p2] === "#") {
                let backCount = 2;
                
                while(backCount > 0) {
                    p2--;
                    backCount--;
                    
                    if(T[p2] === "#") {
                        backCount += 2;
                    }
                }
            }
        } else {
            if(S[p1] !== T[p2]) {
                return false;
            } else {
                p1--;
                p2--;
            }
        }
    }
    
    return true;
};

console.log(backspaceCompare(string1, string2));
```

### 2. Longest Substring Without Repeating Characters (Medium)

[Given a string s, find the length of the longest substring without repeating characters.](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

Logic: store the chars one by one in temp variable, and longest  = temp.length, if it encounters repeating char, then slice the string.

Solution 1: Using temp variable

```javascript
const lengthOfLongestSubstring = str => {
 const strLen = str.length;
 if(strLen < 2) return strLen;
 let longest = 0, temp = "";
 for(i = 0; i < strLen; i++){
   if(temp.indexOf(str[i]) >= 0){
      temp = temp.slice(temp.indexOf(str[i])+1) + str[i];
   }
   else{
       temp = temp + str[i];
       longest = Math.max(longest, temp.length);
   } 
 }
 return longest
}
```

Solution 2: Using hashmap [Repl](https://replit.com/@ZhangMYihua/longest-substring-without-repeat-characters-optimal)

```javascript
const string = "au"

const lengthOfLongestSubstring = function(s) {
    if(s.length <= 1) return s.length;
    
    const seen = {};
    let left = 0, longest = 0;
    
    for(let right = 0; right < s.length; right++) {
        const currentChar = s[right];
        const previouslySeenChar = seen[currentChar];
        
        if(previouslySeenChar >= left) {
          left = previouslySeenChar + 1;
        }
        
        seen[currentChar] = right;
        
        longest = Math.max(longest, right - left + 1);
    }
    
    return longest;
};

console.log(lengthOfLongestSubstring(string));

```

### 3. Palindromes

Approaches: Following are some of approaches to find if a string is palindrome or not.

1. Approach: Two pointers technique.let p be the first char in the given string and q be the last char in the given string. and compare p === q if true then do p++ and q-- ... if it is false then return not a palindrome. Inward pointers, in this case pointers move inwards
2. Approach: Instead of inward pointer, in this case pointers are at center position and they move outward
3. Approach: Given string is S. In this apporach we reverse the given string and store it in variable S'.  let p pointer is pointing to first char in the S and q pointer is pointing to first char in S'. then compare p and q.
4. Approach: Using builtin methods. reverse the string and compare `str === str.reverse()`

[Q1: Valid Palindromes - 1](https://leetcode.com/problems/valid-palindrome/)

Solutions:
  
- [outward pointers](https://replit.com/@ZhangMYihua/Valid-Palindrome-2-pointers-from-center#main.js)
- [inward pointers](https://replit.com/@ZhangMYihua/Valid-Palindrome-2-pointers-from-outside)
- [string reverse](https://replit.com/@ZhangMYihua/Valid-Palindrome-compare-against-reverse#main.js)

[Q2: Valid Palindrome - 11](https://leetcode.com/problems/valid-palindrome-ii/)

Solution: [Repl](https://replit.com/@ZhangMYihua/Almost-palindrome-solution#main.js)

```javascript
var validPalindrome = function(s) {
    let p=0,
        q=s.length-1;
    while(p <= q){
        if(s[p] !== s[q]){
            return isValid(s,p+1, q) || isValid(s, p, q-1);
        }
        p++;
        q--;
    }
    return true;
};

function isValid(s, p, q){
  while(p < q){
      if(s[p] !== s[q]){
          return false
      };
      p++;
      q--;
  }
  return true
}

validPalindrome(abca);
```

### 4. Split a String in Balanced Strings
[Balanced strings are those that have an equal quantity of 'L' and 'R' characters.Given a balanced string s, split it in the maximum amount of balanced strings.Return the maximum amount of split balanced strings.](https://leetcode.com/problems/split-a-string-in-balanced-strings/)

Logic: Using stack, we will push the first char in the given string to the stack, then  we will push again if we the see the same character else pop out the last element. then check stack length if it zero push it to our results array.

Solution: [Leetcode](https://leetcode.com/submissions/detail/502989590/)

```javascript
var balancedStringSplit = function(s) {
    let stack = [];
    stack.push(s[0]);
    let result = 0;
    for(let i=1; i<s.length; i++){
        if(stack.includes(s[i]) || stack.length === 0){
            stack.push(s[i]);
        }
        else{
            stack.pop();
            if(!stack.length){
                result += 1;
            }
        }
    }
    return result;
};
```

***

## Linked Lists

### 1. Reverse a Linked List

[Given the head of a singly linked list, reverse the list, and return the reversed list.](https://leetcode.com/problems/reverse-linked-list/)

Solution: [Repl](https://replit.com/@ZhangMYihua/reverse-linked-list#main.js)

```javascript
var head = {
  value: 1,
  next: {
    value: 2,
    next: {
      value: 3,
      next: {
        value: 4,
        next: {
          value: 5,
          next: null
        }
      }
    }
  }
}

function reverseLL(head){
  let prev = null;
  let cn = head;
  while(cn){
    let next = cn.next;
    cn.next = prev;
    prev = cn;
    cn = next;
  }
  while(prev){
    console.log(prev.value);
    prev = prev.next;
  }
}

console.log(reverseLL(head));

```

### 2. M, N Reversals

[Given the head of a singly linked list and two integers left and right where left <= right, reverse the nodes of the list from position left to position right, and return the reversed list.](https://leetcode.com/problems/reverse-linked-list-ii/)

Solution: [Repl](https://replit.com/@ZhangMYihua/M-N-reversals)

```javascript
var reverseBetween = (head, left, right) => {
    let start = head, cn = head, currentPos = 1;
    while(currentPos < left){
        start = cn;
        cn = cn.next;
        currentPos++;
    }
    let tail = cn, newList = null;
    while(currentPos >= left && currentPos <= right){
        next = cn.next;
        cn.next = newList;
        newList = cn;
        cn = next;
        currentPos++;
    }
    start.next = newList;
    tail.next = cn;
    if(left > 1){
        return head;
    }
    else{
        return newList;
    }
    
}
```

### 3. Flatten a Multilevel Doubly Linked List

[You are given a doubly linked list which in addition to the next and previous pointers, it could have a child pointer, which may or may not point to a separate doubly linked list. These child lists may have one or more children of their own, and so on, to produce a multilevel data structure, as shown in the example below.Flatten the list so that all the nodes appear in a single-level, doubly linked list. You are given the head of the first level of the list.](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/)

Solution: [Repl](https://replit.com/@ZhangMYihua/merge-multi-level-doubly-linked-list#main.js)

```javascript
var flatten = function(head) {
    if(!head) return head;
    let cn = head, start = head, tail = null;
    
    while(cn){
        if(cn.child){
            start = cn;
            let temp = cn.child;
            while(temp){
                tail = temp;
                temp = temp.next;
            }
            if(tail){
                next = start.next;
                start.next = start.child;
                tail.next = next;
                if(next) next.prev = tail;
                start.child.prev = start;
                start.child = null;  
            }
        }
        cn = cn.next;
    }
    return head;
};
```

### 4. Cycle detecting in Linked List

[Given a linked list, return the node where the cycle begins. If there is no cycle, return null.There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.Notice that you should not modify the linked list.](https://leetcode.com/problems/linked-list-cycle-ii/)

Brute force solution: Using set, add the each node to the set, if the element is present in set then return element. [Repl](https://replit.com/@ZhangMYihua/cycle-detection-with-Set)

```javascript
var detectCycle = function(head) {
    if(!head) return head;
    let cn = head, set = new Set();
    while(cn){
        if(set.has(cn)){
            return cn;
        }
        else{
            set.add(cn);
        }
        cn = cn.next;
    }
    return null;
};
```

Optimal solution: Using tortoise and hare(rabbit) alogirthm, the idea here is to increase the tortoise pointer by 1 and hare pointer by 2; if hair reaches the last value and it is null, then no cycle is detected.if hare and tortoise meets(equal), then cycle is detected. from there let p1 be the head and p2 be the last meeting point of hare and tortoise, if both p1===p2 return p1 or p2;[Repl](https://replit.com/@ZhangMYihua/cycle-detection-Flyods-tortoise-and-hare#main.js)

```javascript
var detectCycle = function(head) {
        if(!head) return null;
        let tortoise = head, hare = head;
        while(true){
            tortoise = tortoise.next;
            hare = hare.next;
            if(hare === null || hare.next === null){
                return null;
            }
            else{
                hare = hare.next;
            }
            if(tortoise === hare) break;
        }
        let p1 = head, p2 = hare;
        while(p1 !== p2){
            p1 = p1.next;
            p2 = p2.next;
        }
        return p1;
};
```
***

## Stacks

### 1. Valid Parenthesis
[Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.An input string is valid if:Open brackets must be closed by the same type of brackets.Open brackets must be closed in the correct order.](https://leetcode.com/problems/valid-parentheses/)

Solution: Using stacks and hashmaps. Hashmap is used to mapping pairs and when we encounter open element we push that to the stack, and when we see close we pop the stack `map[stack.pop()] !== c` return false. else if the stack length is empty true. [Repl](https://replit.com/@ZhangMYihua/valid-parentheses#main.js)

```javascript
var isValid = function(s) {
    var map = {
        "(" : ")",
        "[" : "]",
        "{" : "}",
    };

    let stack = [];
    for(c of s){
        if(c === "(" || c === "{" || c === "["){
            stack.push(c);
        }
        else{
            if(map[stack.pop()] !== c){
                return false;
            }
        }
    }
    return stack.length === 0;
};
```

### 2. Minimum Remove to Make Valid Parenthesis

[Given a string s of '(' , ')' and lowercase English characters. Your task is to remove the minimum number of parentheses ( '(' or ')', in any positions ) so that the resulting parentheses string is valid and return any valid string.](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/)

Solution:
```javascript
var minRemoveToMakeValid = function(s) {
    let res = s.split(""),
        stack = [];
    
    for(let i=0; i<res.length; i++){
        if(res[i] === "("){
            stack.push(i);
        }
        else if(res[i] === ")" && stack.length){
            stack.pop();
        } else if(res[i] === ")"){
            res[i] = "";
        }
    }
    
    while(stack.length){
        const ci = stack.pop();
        res[ci] = "";
    }
    
    return res.join("");
};
```
***

## Queues

### 1. Implement Queue using Stacks
[Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).](https://leetcode.com/problems/implement-queue-using-stacks/)

Solution: [Repl](https://replit.com/@ZhangMYihua/Create-Queue-using-stacks)
```javascript
var MyQueue = function() {
    this.stackIn = [];
    this.stackOut = [];
};

MyQueue.prototype.push = function(x) {
    this.stackIn.push(x);
};

MyQueue.prototype.pop = function() {
    console.log(this.stackOut);
    if(this.stackOut.length === 0){
        while(this.stackIn.length){
            this.stackOut.push(this.stackIn.pop());
        }
    }
    return this.stackOut.pop();
};

MyQueue.prototype.peek = function() {
    if(this.stackOut.length === 0){
        while(this.stackIn.length){
            this.stackOut.push(this.stackIn.pop());
        }
    }
    return this.stackOut[this.stackOut.length-1];
};

MyQueue.prototype.empty = function() {
    if(this.stackIn.length === 0 && this.stackOut.length === 0){
        return true;
    }
    else{
        return false;
    }
};
```
***

## Recursion(Sorting and Quickselect)

### 1. Factorial 

**Normal Recursion**

Solution: Space complexity O(n), as call stack needs to remember previous value in every step. Here original function call is waiting for the subsequent recursive calls. so it has to store all the function calls in the stack.
```javascript
function factorial(n){
    if(n <= 1){
        return 1;
    }
    return n * factorial(n-1);

}

factorial(5);
```

**TailRecursion**

Solution: Space complexity is O(1), we return the value of function call every time, we dont need to store the previous value. Here original function dont need to store anything, when original call is executed it passes the value by performing some calculations to the next recursive calls. so we dont store anything here. 

```javascript
function factorial(n, total=1){
    if(n === 0){
        return total;
    }
    return factorial(n-1, total * n);

}

factorial(5);
```
### 2. Kth Largest Element in an Array
[Given an integer array nums and an integer k, return the kth largest element in the array.Note that it is the kth largest element in the sorted order, not the kth distinct element.](https://leetcode.com/problems/kth-largest-element-in-an-array/)

Solution 1: Using built in methods:
```javascript
var findKthLargest = function(nums, k) {
    if(nums.length === 1) return nums;
    return nums.sort((a,b) => a-b)[nums.length-k];
};
```

Solution 2:  Using quicksort [Repl](https://replit.com/@ZhangMYihua/Find-kth-largest-element-Quicksort#main.js)

Solution 3: Using quickselect[Repl](https://replit.com/@ZhangMYihua/Find-kth-largest-element-Quickselect#main.js)



### 3.  Binary Search
[Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.You must write an algorithm with O(log n) runtime complexity.](https://leetcode.com/problems/binary-search/)

Solution:
```javascript
var search = function(nums, target) {
    let left = 0, right = nums.length-1;
    while(left <= right){
        let middle = Math.floor((left+right)/2);
        const foundVal = nums[middle];
        if(foundVal === target){
           return middle;
        }
        if(foundVal < target){
            left = middle+1;
        }
        else{
            right = middle-1;
        }
    }
    return -1;
};
```

### 4.  Find First and Last Position of Element in Sorted Array
[Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value.If target is not found in the array, return [-1, -1].You must write an algorithm with O(log n) runtime complexity.](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

Solution: [Repl](https://replit.com/@ZhangMYihua/Find-start-and-end-of-target-OlogN#main.js)

```javascript
var searchRange = function(N, T) {
    const find = (target, arr, left=0, right=arr.length) => {
        while (left <= right) {
            let mid = left + right >> 1
            if (arr[mid] < target) left = mid + 1
            else right = mid - 1
        }
        return left
    } 
    let Tleft = find(T, N)
    if (N[Tleft] !== T) return [-1,-1]
    return [Tleft, find(T+1, N, Tleft) - 1]
};
```

***

## 2D Arrays

### 1. 2D Array(Matrix) traversal using DFS - Recursive Approach

```
input:
const testMatrix = [
  [1,    2,     3,    4,    5],
  [6,    7,     8,    9,   10],
  [11,  12,  13,  14,  15],
  [16,  17,  18,  19,  20]
];
output: 
[
  1,  2,  3,  4,  5, 10, 15,  20, 19, 14, 9,  8, 13, 18, 17, 12,  7, 6, 11, 16
]
```

Solution: [Repl](https://replit.com/@kantesrikanth/2DArraysDFS#index.js)

```javascript
const input = [
  [1, 2, 3, 4, 5],
  [6, 7, 8, 9, 10],
  [11, 12, 13, 14, 15],
  [16, 17, 18, 19, 20]
];

const traversalDFS = (matrix) => {
  let seen = Array(matrix.length).fill(0)
              .map(() => Array(matrix[0].length).fill(false));
  
  let output = [];

  helper(matrix, 0, 0, seen, output);

  return output;
}

const helper = (matrix, row, col, seen, output) => {
  if(row < 0 || col < 0 || row >= matrix.length || col >= matrix[0].length || seen[row][col]) return;
  output.push(matrix[row][col]);
  seen[row][col] = true;

  helper(matrix, row-1, col, seen, output);
  helper(matrix, row, col+1, seen, output);
  helper(matrix, row+1, col, seen, output);
  helper(matrix, row, col-1, seen, output);
}



traversalDFS(input);
```

### 2. 2D Array(Matrix) traversal using BFS - Recursive Approach

```
input:
const testMatrix = [
  [1,    2,     3,    4,    5],
  [6,    7,     8,    9,   10],
  [11,  12,  13,  14,  15],
  [16,  17,  18,  19,  20]
];
output: 
[
   1,  2,  5,  3, 6,  9,  4,  7, 10, 13, 8, 11, 14, 12, 15, 16
]
```

Solution: [Repl](https://replit.com/@kantesrikanth/2DArrayBFSTraversal)

```javascript
const input = [
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9, 10, 11, 12],
  [13, 14, 15, 16]
];

const traversalBFS = (matrix) => {
  const seen = Array(matrix.length).fill(0)
                .map(() => Array(matrix[0].length).fill(false));
  const output = [];
  const queue = [[0,0]];
  while(queue.length){
    const [row, col] = queue.shift();
    if(row < 0 || col < 0 || row >= matrix.length || col >= matrix[0].length || seen[row][col]) continue;
    output.push(matrix[row][col]);
    seen[row][col] = true;

    queue.push([row-1, col]);
    queue.push([row, col+1]);
    queue.push([row+1, col]);
    queue.push([row, col-1]);
  }
  return output;
}

traversalBFS(input);
```

### 3. Number of Islands
[Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.](https://leetcode.com/problems/number-of-islands/)

Logic: Using nested for loops, and if `grid[row][col] === "1",` then increment do `countIslands++` and then we need to convert all the 1's that are connected into 0's. This is to ensure that we don't count duplicate islands. to do this we need to perform either BFS/DFS. and after for loop execution is done return the `countIslands`;

Initially we are performing sequential traverse by using nested for loops, and then using BFS/DFS to traverse the adjacent top/down/left/right values.

Approach using Sequential + DFS:

Solution: 
    - [Leetcode](https://leetcode.com/submissions/detail/503097503/)
    - [Repl](https://replit.com/@ZhangMYihua/Number-of-Islands-DFS#main.js)


```javascript
const numIslands = (grid) => {
    let count = 0;
    for(let row=0; row<grid.length; row++){
        for(let col=0; col<grid[0].length; col++){
            if(grid[row][col] === "1"){
                count++;
                traverse(grid, row, col);
            }
        }
    }
    return count;
};

const traverse = (grid, row, col) => {
    if(row < 0 || col < 0 || row >= grid.length || col >= grid[0].length) return;
    if(grid[row][col] === "1"){
        grid[row][col] = "0";    
        traverse(grid, row-1, col);
        traverse(grid, row, col+1);
        traverse(grid, row+1, col);
        traverse(grid, row, col-1);
    }
}
```

Approach using Sequential + BFS:

Solution: [Repl](https://replit.com/@ZhangMYihua/Number-of-Islands-BFS#main.js)

```javascript
const input = [
  [1, 1, 1, 0, 0],
  [1, 1, 1, 0, 1],
  [0, 1, 0, 0, 1],
  [0, 0, 0, 1, 1]
];

const directions = [
  [-1, 0], //up
  [0, 1], //right
  [1, 0], //down
  [0, -1] //left
]

const numberOfIslands = function(matrix) {
  if(matrix.length === 0) return 0;
  let islandCount = 0;

  for(let row = 0; row < matrix.length; row++) {
    for(let col = 0; col < matrix[0].length; col++) {
      if(matrix[row][col] === 1) {
        islandCount++;
        matrix[row][col] = 0;
        const queue = [];
        queue.push([row, col]);

        while(queue.length) {
          const currentPos = queue.shift();
          const currentRow = currentPos[0];
          const currentCol = currentPos[1];

          for(let i = 0; i < directions.length; i++) {
            const currentDir = directions[i];
            const nextRow = currentRow + currentDir[0];
            const nextCol = currentCol + currentDir[1];

            if(nextRow < 0 || nextRow >= matrix.length || nextCol < 0 || nextCol >= matrix[0].length) continue;

            if(matrix[nextRow][nextCol] === 1) {
              queue.push([nextRow, nextCol]);
              matrix[nextRow][nextCol] = 0;
            }
          }
        }
      }
    }
  }

  return islandCount;
}

console.log(numberOfIslands(input));
```

### 4. Rotten Oranges
[You are given an m x n grid where each cell can have one of three values:0 representing an empty cell,1 representing a fresh orange, or 2 representing a rotten orange.Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten. Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return -1.](https://leetcode.com/problems/rotting-oranges/)

Logic: First we need to push the rotten oranges [row, col]into new queue and store total no of fresh orange in a variable by using sequential traversal(nested for loops). then after that  we need to run BFS on the queue, then decrease the fresh orange count when we see it. and also we need to keep track of minutes variable, if single BFS is completed then minutes++. finally if the freshOrange > 0 then we need to return -1, else return minutes.

Solution: [Repl](https://replit.com/@ZhangMYihua/Rotting-Oranges-Solution#main.js)

```javascript
const testMatrix = [
  [2, 1, 1, 0, 0],
  [1, 1, 1, 0, 0],
  [0, 1, 1, 1, 1],
  [0, 1, 0, 0, 1]
];

const directions = [
  [-1, 0], //up
  [0, 1], //right
  [1, 0], //down
  [0, -1] //left
]

const ROTTEN = 2;
const FRESH = 1;
const EMPTY = 0;


const orangesRotting = function(matrix) {
  if(matrix.length === 0) return 0;

  const queue = [];  
  let freshOranges = 0;
  
  for(let row = 0; row < matrix.length; row++) {
    for(let col = 0; col < matrix[0].length; col++) {
      if(matrix[row][col] === ROTTEN) {
        queue.push([row, col])
      }
      
      if(matrix[row][col] === FRESH) {
        freshOranges++;
      }
    }
  }
    
  let minutes = 0;
  let currentQueueSize = queue.length;
  
  while(queue.length > 0) {
    if(currentQueueSize === 0) {
      currentQueueSize = queue.length;
      minutes++;
    }

    const currentOrange = queue.shift();
    currentQueueSize--;
    const row = currentOrange[0];
    const col = currentOrange[1];
    
    for(let i = 0; i < directions.length; i++) {
      const currentDir = directions[i];
      const nextRow = row + currentDir[0];
      const nextCol = col + currentDir[1];
      
      if(nextRow < 0 || nextRow >= matrix.length || nextCol < 0 || nextCol >= matrix[0].length) {
        continue;
      }

      if (matrix[nextRow][nextCol] === FRESH) {
        matrix[nextRow][nextCol] = 2;
        freshOranges--;
        queue.push([nextRow, nextCol]);
      }
    }
  }
  
  if(freshOranges !== 0) {
    return -1;
  }
  
  return minutes;
};

console.log(orangesRotting(testMatrix)
```

### 5. Walls and gates

Q: Suppose we have one m x n 2D grid, and that is initialized with these three possible values.-1 for a wall or an obstacle.0 for a gate.INF This is infinity means an empty room.Here 2^31 - 1 = 2147483647 is INF as we may assume that the distance to a gate is less than 2147483647. Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, it should be filled with INF.
[GFG](https://www.geeksforgeeks.org/find-shortest-distance-guard-bank/)
[Leetcode](https://leetcode.com/problems/walls-and-gates/)

Logic: The idea is to perform sequential search and perform BFS/DFS. In the sequential search if current element is equal to GATE(0), then we need to perfrom the BFS/DFS and replace the current[row][col] = count; if count > current[row][col] we skip. if not perform BFS/DFS.

Solution: 
- [Repl](https://replit.com/@kantesrikanth/2DArrayWallsgate#index.js)
- [Repl](https://replit.com/@ZhangMYihua/Walls-and-Gates-Solution#main.js)

```javascript
const input = [
  [Infinity, -1, 0, Infinity],
  [Infinity, Infinity, Infinity, 0],
  [Infinity, -1, Infinity, -1],
  [0, -1, Infinity, Infinity]
];

const wallsAndGates = (arr) => {
  for(let row=0; row<arr.length; row++){
    for(let col=0; col<arr[0].length; col++){
      if(arr[row][col] === 0){
        dfs(arr, row, col, 0);
      }
    }
  }
  return arr;
}

const dfs = (arr, row, col, count) => {
  if(row<0 ||  row>=arr.length  || col<0 || col>=arr[0].length || count > arr[row][col]) return;
     arr[row][col] = count;
     dfs(arr, row-1, col, count+1);
     dfs(arr, row, col+1, count+1);
     dfs(arr, row+1, col, count+1);
     dfs(arr, row, col-1, count+1);
}

wallsAndGates(input);

output: 
[ [ 3, -1, 0, 1 ], [ 2, 2, 1, 0 ], [ 1, -1, 2, -1 ], [ 0,-1, 3, 4 ] ]

```

### 6. Search a 2D Matrix
[Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:Integers in each row are sorted from left to right.The first integer of each row is greater than the last integer of the previous row.](https://leetcode.com/problems/search-a-2d-matrix/)

### 7. Set Matrix Zeroes
[Given an m x n matrix. If an element is 0, set its entire row and column to 0. Do it in-place.](https://leetcode.com/problems/set-matrix-zeroes/)

### 8. Transpose Matrix
[Given a 2D integer array matrix, return the transpose of matrix.The transpose of a matrix is the matrix flipped over its main diagonal, switching the matrix's row and column indices.](https://leetcode.com/problems/transpose-matrix/)

***

## Binary trees

### 1. Maximum Depth of Binary Tree
[Given the root of a binary tree, return its maximum depth.A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

Approach:  Using recursion, we traverse through all the elements until it is null, and return the max count of lefttraversal and righttraversal.

Solution: 
- [Repl](https://replit.com/@ZhangMYihua/Maximum-depth#main.js)
- [Leetcode](https://leetcode.com/submissions/detail/499406238/)
- [Leetcode](https://leetcode.com/submissions/detail/503281533/)

```javascript
var maxDepth = function(root) {
    return traverse(root, 0);
};
const traverse = (node, count) => {
    if(!node) return count;
    count++;
    return Math.max(traverse(node.left, count), traverse(node.right, count));
}
```
**or**
```javascript
var maxDepth = function(root) {
  function height(node){
     if(!node) return 0;
     var lh = height(node.left);
     var rh = height(node.right);
     return Math.max(lh, rh)+1; 
  }
  return height(root);
};
```

### 2. Binary Tree Level Order Traversal
[Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).](https://leetcode.com/problems/binary-tree-level-order-traversal/)

Solution: 
- [Leetcode](https://leetcode.com/submissions/detail/503291226/)
- [Repl](https://replit.com/@ZhangMYihua/Level-Order)

```javascript
const levelOrder = (root) => {
    if(!root) return [];
    const result = [], queue = [root];
    while(queue.length){
        let count  = 0, length = queue.length, currentLevelArrays = [];
        while(count < length){
            const currentNode = queue.shift();
            currentLevelArrays.push(currentNode.val);
            if(currentNode.left) queue.push(currentNode.left);
            if(currentNode.right) queue.push(currentNode.right);
            count++;
        }
        result.push(currentLevelArrays);        
    }
    return result;
};
```
### 3. Binary Tree Right Side View
[Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.](https://leetcode.com/problems/binary-tree-right-side-view/)


Approach: Using BFS and we need to check for if the currentNode is right most element or not, if yes push it to the output array else do nothing. To check if the element in the level is right most or not, we need to keep track of node level using `Count` property as shown in the below.

Solution:
- [Leetcode](https://leetcode.com/submissions/detail/503306990/)
- [Repl](https://replit.com/@ZhangMYihua/Binary-tree-right-side-view-BFS#main.js)


```javascript
const rightSideView = (root) => {
    if(!root) return [];
    let output= [], queue = [root];
    while(queue.length){
        let count=0, length = queue.length;
        while(count < length){
            const currentNode  = queue.shift();
            if(currentNode.left) queue.push(currentNode.left);
            if(currentNode.right) queue.push(currentNode.right);
            count++;
            if(count === length){
                output.push(currentNode.val);
            }
        }
    }
    return output;
};
```


Approach: Using DFS [Repl](https://replit.com/@ZhangMYihua/Binary-tree-right-side-view-DFS#main.js)

```javascript
const dfs = (node, currentLevel, result) => {
  if(!node) return;
  if(currentLevel >= result.length) {
    result.push(node.value);
  }

  if(node.right) {
    dfs(node.right, currentLevel + 1, result);
  }
  
  if(node.left) {
    dfs(node.left, currentLevel + 1, result);
  }
}

const rightSideViewDFS = function(root) {
  const result = [];
  
  dfs(root, 0, result);
  return result;
};

console.log(rightSideViewDFS(tree))
```

### 4. Binary Tree Left Side View
[Given a Binary Tree, print left view of it. Left view of a Binary Tree is set of nodes visible when tree is visited from left side.](https://www.geeksforgeeks.org/print-left-view-binary-tree/)

Approach:  Using BFS and we need to check for if the currentNode is left most element or not, if yes push it to the output array else do nothing. To check if the element in the level is left most or not, we need to keep track of node level using `Count` property as shown in the below. if `count===1` that means it is the first element in the left view.

Solution: [Repl](https://replit.com/@kantesrikanth/BinaryTreeLeftView#index.js)

```javascript
const leftSideView = (root) => {
    if(!root) return [];
    let output= [], queue = [root];
    while(queue.length){
        let count=0, length = queue.length;
        while(count < length){
            const currentNode  = queue.shift();
            if(currentNode.left) queue.push(currentNode.left);
            if(currentNode.right) queue.push(currentNode.right);
            count++;
            if(count === 1){
                output.push(currentNode.val);
            }
        }
    }
    return output;
};
```

### 5.  Count Complete Tree Nodes
[Given the root of a complete binary tree, return the number of the nodes in the tree.According to Wikipedia, every level, except possibly the last, is completely filled in a complete binary tree, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.Design an algorithm that runs in less than O(n) time complexity.](https://leetcode.com/problems/count-complete-tree-nodes/)

Brute Force: Traversing each node in the tree and keep track of count. [Leetcode](https://leetcode.com/submissions/detail/503333512/)
```javascript
var countNodes = (root) => {
    if (!root) return 0;
    if (root.left == null && root.right == null) return 1;
    return countNodes(root.left) + countNodes(root.right) + 1;
}
```

Optimal solution: Find the left most depth and right most depth, if equal return `Math.pow(s, leftLen)-1`; [Leetcode](https://leetcode.com/submissions/detail/503333762/)

```javascript
const countNodes = (root) => {
    const leftDepth = (node) => {
        if(!node) return 0;
        return leftDepth(node.left)+1;
    }
    
    const rightDepth = (node) => {
        if(!node) return 0;
        return rightDepth(node.right)+1;
    }
    
    const traverse = (node) => {
        const leftLen = leftDepth(node);
        const rightLen = rightDepth(node);
        if(leftLen === rightLen) return Math.pow(2, leftLen)-1;
        return traverse(node.left) + traverse(node.right) + 1;
    }
    
    return traverse(root);
};
```

### 6. Validate Binary Search Tree
[Given the root of a binary tree, determine if it is a valid binary search tree (BST).](https://leetcode.com/problems/validate-binary-search-tree/)

Apporach: Check if each element is within the range of Min, Max if yes true, then again perfrom the same check for node.left and node.right element, if yes return true, else false;

Solution:
- [Leetcode](https://leetcode.com/submissions/detail/503340525/)
- [Repl](https://replit.com/@ZhangMYihua/Validate-Binary-Search-Tree#main.js)

```javascript
var isValidBST = function(root) {
    if(!root) return null;
    const isBst = (node, min, max) => {
        if(node === null) return true;
        if(node.val > min && node.val < max && isBst(node.left, min, node.val) && isBst(node.right, node.val, max)){
            return true
        }
        else return false;
    }
    return isBst(root, Math.max(), Math.min());
};

```

***
