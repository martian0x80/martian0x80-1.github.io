---
title: "137. Single Number I (Leetcode)"
date: 2024-01-16T18:40:00+05:30
draft: true
author: "martian0x80"
---

# [137. Single Number I](https://leetcode.com/problems/single-number/)

### GDSC Day 1: Leetcode Practice

## Description:

Given a non-empty array of integers `nums`, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use *only constant extra space*.

#### Example 1:
````
Input: nums = [2,2,1]
Output: 1
````
#### Example 2:
````
Input: nums = [4,1,2,1,2]
Output: 4
````
#### Example 3:
````
Input: nums = [1]
Output: 1
````
 
#### Constraints:

- ```1 <= nums.length <= 3 * 104```
- ```-3 * 104 <= nums[i] <= 3 * 104```
- Each element in the array appears twice except for one element which appears only once.

## Solutions:

### Solution 1: Using XOR (Time Complexity: `O(n)`, Space Complexity: `O(1)`)
**TLDR**: Use the following relations to find the element which is not repeated in the array.

- `a XOR a = 0`
- `a XOR 0 = a`
- `a XOR b = c` then `c XOR b = a`

The third relation is the most important one, imho. If we XOR two numbers, we get a third number. If we XOR the third number with one of the two numbers, we get the other number. This is very common in cryptography, and used for xor encryption, where we encrypt a message by XORing it with a key, and decrypt it by XORing it with the same key. Shellcodes are also often encoded using XOR and decrypted at runtime to avoid detection (I have used this technique before while writing a shellcode loader).

#### Explanation:

Let's say we have an array `nums = [2, 2, 1, 3, 3]`. We need to find the element which is not repeated in the array. Let's call this element `ans`. We can use the following relations to find `ans`:

```
((((2 XOR 2) XOR 1) XOR 3) XOR 3)
= (((0 XOR 1) XOR 3) XOR 3)
= ((1 XOR 3) XOR 3)
= (2 XOR 3)
= 1
```

We can see that the order of XORing does not matter. We can also see that the repeated elements cancel out each other. This is because `a XOR a = 0`. So, if we XOR two equal numbers, we get 0. If we XOR 0 with a number, we get the number itself. So, if we XOR all the elements of the array, we will get the element which is not repeated in the array. Also, when both the numbers are different, we get a third number, which returns back if we encounter one of the two numbers again. This is because `a XOR b = c` then `c XOR b = a`.

#### CPP:
```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int ans = 0;
        for (int i = 0; i < nums.size(); i++){
            ans ^= nums[i];
        }
        return ans;
    }
};
```

#### Python:
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        ans = 0
        for i in nums:
            ans ^= i
        return ans
```

#### Python:
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        return reduce(xor, nums)```
```

#### Rust:
```rust
impl Solution {
    pub fn single_number(nums: Vec<i32>) -> i32 {
        let mut ans = 0;
        for i in nums {
            ans ^= i;
        }
        ans
    }
}
```


### Not a Solution 1: Using Hash Map (Time Complexity: `O(n)`, Space Complexity: `O(n)`)

**TLDR**: Use a hash map to store the frequency of each element in the array. Then iterate over the array:
- If the element is not present in the hash map, add it to the hash map with frequency 1.
- If the element is present in the hash map, remove it from the hash map.

At the end, the hash map will contain only one element, which is the answer.

Or, we can use a hash map to store the frequency of each element in the array. Then iterate over the hash map and return the element with frequency 1.

#### CPP:
```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        unordered_map<int, int> mp;
        for (int i = 0; i < nums.size(); i++){
            if (mp.find(nums[i]) == mp.end()){
                mp[nums[i]] = 1;
            }
            else{
                mp.erase(nums[i]);
            }
        }
        return mp.begin()->first;
    }
};
```

#### C#:
```csharp
public class Solution {
    public int SingleNumber(int[] nums) {
        Dictionary<int, int> hashmap = new Dictionary<int, int>();
        foreach (var i in nums) {
            if (!hashmap.ContainsKey(i)) {
                hashmap.Add(i, 1);
            } else {
                hashmap.Remove(i);
            }
        }
        return hashmap.Keys.ElementAt(0);
    }
}
```

