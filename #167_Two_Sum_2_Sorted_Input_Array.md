# Problem:

## Two Sum 2 - Input array is sorted

Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number. 

The function twoSum should return indices of the two numbers such that they add up to the target, where index 1 must be less than index 2.

**Note:**
- Your returned answers (both index 1 & 2) are not zero-based.
- you may assume that each input would have *exactly* one solution and you may not use the *same* element twice.

**Example:**

	Input: numbers = [2,7,11,15], target = 9
	Output: [1,2]
	Explanation: The sum of 2 and 7 is 9. Therefore, index_1 = 1,index_2 = 2.

# Solutions:

### Solution 1

- Basic idea: for each element in the array, find the index of (target - element).
	- Time complexity is *O(N^2)*

```python
class Solution(object):
    def TwoSum2(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype List[int]
        """
        i, j = 0, 0

        while i < len(numbers)-1:
            for j in range(i+1, len(numbers)-1):
                if numbers[i] + numbers[j] == target:
                    return [i, j]
            i += 1
``` 

### Solution 2

- Improved idea: two keys can point toward the head and the end of the array, moving to the mid accordingly. 
	- Time complexity is *O(N)*.

```python
class Solution(object):
    def TwoSum2(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype List[int]
        """
        low, high = 0, len(numbers) - 1

        while low < high:
            if numbers[low] + numbers[high] == target:
                return [low, high]
            elif numbers[low] + numbers[high] > target:
                high -= 1
            else:
                low += 1

```

### Solution 3

- Improved idea 2: using dictionary.
	- Time complexity is *O(N)*.

```python
class Solution(object):
    def TwoSum2(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype List[int]
        """

        Dict = {}
        for i in range(len(numbers)):  # using xrange() here is faster than range()
            x = numbers[i]
            if target - x in Dict:
                return [Dict[target - x], i]
            Dict[x] = i

```

### Solution 4

- Improved idea 3: using binary search.
	- Time complexity is *O(N\*log(N))*.

```python
class Solution4(object):
    def TwoSum2(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype List[int]
        """
        for i in range(len(numbers)):
            left, right = i+1, len(numbers)-1
            tmp = target - numbers[i]
            while left <= right:
                mid = (left + right) // 2
                if numbers[mid] == tmp:
                    return [i, mid]
                elif numbers[mid] < tmp:
                    left = mid + 1
                else:
                    right = mid - 1

```
