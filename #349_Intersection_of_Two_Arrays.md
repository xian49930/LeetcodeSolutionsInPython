# Problem

## Intersection of Two Arrays

Give two arrays, write a function to compute their intersection.

**Example 1:**

	Input: nums1 = [1,2,2,1], nums2 = [2,2]
	Ouptut: [2]

**Example 2:**

	Input: nums1 = [4, 9, 5], nums2 = [9,4,9,8,4]
	Output: [9,4]

**Note:**

- Each element in the result must be unique.
- The result can be in any order.

# Solutions

### Solution 1

- Basic idea: for every element in array 1, find if it is in array 2; yes, return to the results; no, jump to another element.
	- The time complexity is *O(M\*N)*

```python
class Solution(object):
	def intersectionOfTwoArrays(self, nums1, nums2):
		"""
		:type nums1: List[int]
		:type nums2: List[int]
		:rtype List[int]
		"""
		result = []
		for i in nums1:
			if i not in result and i in nums2:
				result.append(i)
		return result

```

### Solution 2

- Improved idea: using basic idea, but sort array 2 first; for each checking, using binary search, which is similar to the problem of #1064 - Fixed Point.
	- The time complexity is *O(nlog(n) + M\*log(n))*
	- In Python, list.sort() uses Timsort algorithm, which has a time complexity of *O(nlog(n))*
	- <span style="color:red">It doesn't work properly and needs to be updated!</span>.

```python
class Solution(object):
	def intersectionOfTwoArrays(self, nums1, nums2):
		"""
		:type nums1: List[int]
		:type nums2: List[int]
		:rtype List[int]
		"""
		result = []
		low, high = 0, len(nums2) - 1

		nums2.sort()

		for i in nums1:
			if i not in result:
				while low <= high:
					mid = (low + high) // 2
					if nums2(mid) == i:
						result.append(i)
					if nums2(mid) <= i:
						low = mid + 1
					if nums2(mid) >= i:
						high = mid - 1
		return result

```

### Solution 3

- Using the built-in set function in Python to do, very neat but the time complexity is not optimized!
	- The time complexity is *O(M\*N)*. 

```python
class Solution(object):
	def intersectionOfTwoArrays(self, nums1, nums2):
		"""
		:type nums1: List[int]
		:type nums2: List[int]
		:rtype List[int]
		"""

		return list(set(nums1) & set(nums2))

```

### Solution 4

- <span style="color:blue">Other solutions will be updated soon...</span>.
