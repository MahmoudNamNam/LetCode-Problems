
# Memoize

[Link to the problem on LeetCode](https://leetcode.com/problems/memoize/description/?envType=study-plan-v2&envId=30-days-of-javascript)

## Problem Description

Write a function `memoize` that takes a function as input and returns a memoized version of that function. A memoized function caches its results based on the arguments passed to it, so that if the function is called again with the same arguments, it returns the cached result instead of recalculating it.

The `memoize` function should adhere to the following specifications:

```javascript
/**
 * @param {Function} func - The input function to be memoized.
 * @returns {Function} - The memoized function.
 */
function memoize(fn) {
   const cache = new Map();
    return function(...args) {
        const key = JSON.stringify(args);
        if(cache.has(key)){
            return cache.get(key)
        }else{
            const result = fn(...args)
            cache.set(key, result)
            return result
        }
    }
}
````
Let's break down the code and explain each part:

1. **`const cache = new Map();`**: 
   - `Map` is a built-in JavaScript object that allows you to store key-value pairs where both the keys and the values can be any type of data.
   - In this case, it is used to store the results of function calls. The keys are generated by stringifying the arguments passed to the function, and the values are the results of the function calls.

2. **`return function(...args) { ... }`**:
   - This is an example of a closure in JavaScript. It defines and returns an anonymous function that has access to the `cache` variable due to closure.

3. **`const key = JSON.stringify(args);`**:
   - `JSON.stringify` is a method in JavaScript that converts a JavaScript object or value to a JSON string.
   - Here, it's used to convert the `args` (arguments passed to the function) into a string. This string will be used as the key in the `Map` to uniquely identify each set of arguments.

4. **`if(cache.has(key)) { return cache.get(key); }`**:
   - Checks if the cache already has a value associated with the generated key.
   - If the key is found in the `Map` (indicating that the function has been called with the same arguments before), it returns the cached result.

5. **`const result = fn(...args); cache.set(key, result); return result;`**:
   - If the key is not found in the cache, it means the function hasn't been called with these arguments before.
   - It then calls the original function (`fn`) with the provided arguments (`...args`) and stores the result in the `cache` with the corresponding key.
   - Finally, it returns the result.

In summary, this code defines a higher-order function `memoize` that takes another function (`fn`) as an argument and returns a memoized version of that function. The memoized function caches the results of previous calls based on the arguments passed to it, avoiding redundant calculations for the same inputs.

-----

## Two Sum



**Introduction:**
The Two Sum problem is a classic algorithmic challenge that falls under the "Easy" category, yet it is widely used to test a programmer's problem-solving skills. In this article, we will explore the problem, discuss some important topics related to it, mention the companies that frequently ask this question in interviews, provide hints to approach the problem, and finally, present a Python solution.

**Problem Description:**
Given an array of integers `nums` and an integer `target`, the task is to return the indices of two numbers in the array such that they add up to the target. It is assumed that each input has exactly one solution, and the same element cannot be used twice.

**Examples:**
1. Input: `nums = [2,7,11,15], target = 9`
   Output: `[0,1]`
   Explanation: `nums[0] + nums[1] == 9`, so the indices are [0, 1].

2. Input: `nums = [3,2,4], target = 6`
   Output: `[1,2]`
   
3. Input: `nums = [3,3], target = 6`
   Output: `[0,1]`


**Hint:**
A brute-force approach involves checking every pair of numbers to see if they add up to the target. However, we can optimize this process using a hash table to store the indices of the numbers we have seen so far.

**Solution:**
Below is a Python solution to the Two Sum problem using the hash table approach:

```python
class Solution:
    def twoSum(self, nums, target):
        num_dict = {}
        for i, num in enumerate(nums):
            complement = target - num
            if complement in num_dict:
                return [num_dict[complement], i]
            num_dict[num] = i
        return []
```

**Explanation:**
1. We iterate through the array `nums` using the `enumerate` function to get both the index and the value of each element.
2. For each element, we calculate its complement by subtracting it from the target.
3. If the complement is already in our `num_dict`, we have found the pair, and we return the indices.
4. If not, we store the current number along with its index in the `num_dict`.
5. If no solution is found, we return an empty list.

**Conclusion:**
The Two Sum problem serves as a great introduction to problem-solving and algorithmic thinking. By understanding and implementing efficient solutions, one can build a strong foundation for tackling more complex coding challenges.