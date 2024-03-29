# Problem

## Is Subsequence

Given a string **s** and a string **t**, check if **s** is subsequence of **t**.

You may assume that there is only lower case English letters in both **s** and **t**. **t** is potentially a very long (length \~= 500,000) string, and s is a short string (<=100).

A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, *"ace"* is a subsequence of *"abcde"* while *"aec"* is not).

**Example 1:**

	s = 'abc', t = 'ahbgdc'
	Return true.

**Example 2:**

	s = 'axc', t = 'ahbgdc'
	Return false

**Follow up:**
If there are lots of incoming S, say S1, S2, ... , Sk where k >= 1B, and you want to check one by one to see if T has its subsequence. In this scenario, how would you change your code?

# Solutions

## Solution 1
- Idea: s is short, while t is long. So, check every item in t for once. Use a collection to keep evert item in s, then check t, if an item in t has been found in the collection, pop out the head of the collection.

```python
class Solution(object):
	def isSubsequence(self, s, t):
		"""
		:type s: str
		:type t: str
		:rtype: bool
		"""
		queue = collections.deque(s)
		for c in t:
			if not queue:
				return True
			if c == queue[0]:
				queue.popleft()
			return not queue
```

## Solution 2
- Idea: using two pointers, instead of the collections. Two pointers point to s and t, correspondingly. If the item in s has been found in t, then move the pointer of s forward; otherwise, only move t's pointer forward.

```python
class Solution(object):
	def isSubsequence(self, s, t):
		"""
		:type s: str
		:type t: str
		:rtype: bool
		"""
		pointer_s, pointer_t = 0, 0
		while pointer_s < len(s) and pointer_t < len(t):
			if t[pointer_t] == s[pointer_s]:
				pointer_s += 1
		return pointer_s == len(s)

```

