
# DSA Problems

- [Arrays](#arrays)
  - [Two sum](#1-two-sum)
  - [Container with most water](#2-container-with-most-water)
  - [Trapping rain water](#3-trapping-rain-water)
- [Strings](#strings)
  - [Typed out strings](#1-typed-out-strings)
  - [Longest substring without repeating characters](#longest-substring-without-repeating-characters-medium)
  - [Palindromes](#palindromes)
- [Linked Lists](#linked-lists)
<!-- /code_chunk_output -->

 ***

> ## Arrays  

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

***

> ## Strings

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

***

> ## Linked Lists

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

***
