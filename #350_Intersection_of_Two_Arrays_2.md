# Problem

## Intersection of Two Arrays 2

Given two arrays, write a function to compute their intersection.



**Example 1:**

​	**Input:** nums1 = [1,2,2,1], nums2 = [2,2]

​	**Output:** [2,2]



**Example 2:**

​	**Input:** nums1 = [4,9,5], nums2 = [9,4,9,8,4]

​	**Output:** [4,9]



**Note:**

- Each element in the result should appear as many times as it shows in both arrays.
- The result can be in any order.



**Follow up:**

- What if the given array is already sorted? How would you optimize your algorithm?
- What if nums1's size is small compared to nums2's size? Which algorithm is better?
- What if elements of nums2 are sorted on disk, and the memory is limited such athat you cannot load all elelments into the memory at once?



# Solutions

**Analysis:**

- For the sorted array, using the binary search is an optimized solution.

- If nums1's size is smaller than nums2's, then do the binary search on nums2.

- Two solutions found online: 

  - Sort + 2 Pointers
  - Use Counter on array with the smaller size. This method won't load all elements of nums2 into the memory at once.

- <span style="color:red">The binary search method will be updated later.</span>

  

## Solution 1:

- Basic idea: sort these arrays first, then use two pointers to check the equalled elements one by one.

  - The time complexity is *O(N log N)*; the sort() function uses *O(n log n)*, while the pointers use *O(n)*.

  ```python
  class Solution(object):
    def intersection(self, nums1, nums2):
      """
      :type nums1: List[int]
      :type nums2: List[int]
      :rtype: List[int]
      """
      nums1.sort()
      nums2.sort()
      p1 = p2 = 0 #pointers
      ans = [] #store the intersection
      while p1 < len(nums1) and p2 < len(nums2):
        if nums1[p1] < nums2[p2]:
          p1 += 1
        elif nums1[p1] > nums2[p2]:
          p2 += 1
        else:
          ans.append(nums1[p1])
          p1 += 1
          p2 += 1
      return ans
           
  ```

  

  ## Solution 2:

- Basic idea: exchange the arrays to make sure nums1 has smaller size; do the counter on nums1; for each element in nums2, check any counts in the collection, if yes, append the element.

  - The time complexity is *O(N)*

  ```python
  class Solution(object):
    def intersection(self, nums1, nums2):
      """
      :type nums1: List[int]
      :type nums2: List[int]
      :rtype: List[int]
      """
      if len(nums1) > len(nums2):
        nums1, nums2 = nums2, nums1
      collect_nums1 = collections.Counter(nums1)
      ans = []
      for element in nums2:
        if collect_nums1[x] > 0:
          ans.append(x)
          collect_nums1[x] -= 1
      return ans
    
  ```

  
