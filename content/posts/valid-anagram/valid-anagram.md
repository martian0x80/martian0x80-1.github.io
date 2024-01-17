---
title: "242. Valid Anagram (Leetcode)"
date: 2024-01-17T23:09:00+05:30
draft: false
author: "martian0x80"
categories: ["DSA"]
description: "Leetcode problem 242. Valid Anagram Solution"
---

### GDSC Day 2: Leetcode Practice

#### [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)

## Description:

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

#### Example 1:
````
Input: s = "anagram", t = "nagaram"
Output: true
````
#### Example 2:
````
Input: s = "rat", t = "car"
Output: false
````

 
#### Constraints:

- ```1 <= s.length, t.length <= 5 * 104```
- ```s and t consist of lowercase English letters.```

**Follow up**: What if the inputs contain Unicode characters? How would you adapt your solution to such a case?


## Solutions:

### Solution 1: Using Hashmap (Time: `O(n)`, Space: `O(C)`, `C = 26`)

#### Procedure:

- Check if the length of both strings is equal. If not, return `false`.
- Create a hashmap or array of length 26 (for 26 alphabets).
- Iterate over both strings simultaneously.
- For each character in `s`, increment the count of that character in the hashmap.
- For each character in `t`, decrement the count of that character in the hashmap.
- If the count of any character in the hashmap is not equal to 0, return `false`.
- Else, return `true`.

#### CPP:
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.size() != t.size()) {
            return false;
        }
        vector<int> cnt(26);
        for (int i = 0; i < s.size(); ++i) {
            ++cnt[s[i] - 'a'];
            --cnt[t[i] - 'a'];
        }
        for (int i = 0; i < 26; ++i) {
            if (cnt[i] != 0) {
                return false;
            }
        }
    }
};
```

#### Java:
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }
        int[] cnt = new int[26];
        for (int i = 0; i < s.length(); ++i) {
            ++cnt[s.charAt(i) - 'a'];
            --cnt[t.charAt(i) - 'a'];
        }
        for (int i = 0; i < 26; ++i) {
            if (cnt[i] != 0) {
                return false;
            }
        }
        return true;
    }
}
```

#### Python:
```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        cnt = [0] * 26
        for i in range(len(s)):
            cnt[ord(s[i]) - ord('a')] += 1
            cnt[ord(t[i]) - ord('a')] -= 1
        for i in range(26):
            if cnt[i] != 0:
                return False
        return True
```

### Solution 2: Using Sorting (Time: `O(nlogn)`, Space: `O(1)`)

#### Procedure:

- Check if the length of both strings is equal. If not, return `false`.
- Sort both strings.
- If both strings are equal, return `true`.
- Else, return `false`.

#### CPP:
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.size() != t.size()) {
            return false;
        }
        sort(s.begin(), s.end());
        sort(t.begin(), t.end());
        return s == t;
    }
};
```

#### Java:
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }
        char[] s1 = s.toCharArray();
        char[] t1 = t.toCharArray();
        Arrays.sort(s1);
        Arrays.sort(t1);
        return Arrays.equals(s1, t1);
    }
}
```

#### Python:
```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        s1 = sorted(s)
        t1 = sorted(t)
        return s1 == t1
```
