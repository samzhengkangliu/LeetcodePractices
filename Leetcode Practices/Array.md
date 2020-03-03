## Array

## 217. Contains Duplicate 
Given an array of integers, find if the array contains any duplicates.

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

>Example 1:
>Input: [1,2,3,1]
>Output: true

>Example 2:
>Input: [1,2,3,4]
>Output: false

>Example 3:
>Input: [1,1,1,3,3,4,3,2,4,2]
>Output: true

Set:
```
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        if not nums or len(nums) == 1: 
            return False
        seen = set()
        for num in nums:
            if num not in seen:
                seen.add(num)
            else:
                return True
        return False
```
Hashset
```
class Solution:  
""" 
@param nums: the given array 
@return: if any value appears at least twice in the array 
"""  
def containsDuplicate(self, nums):  
	hashset = {} 
	for num in nums: 
		if num in hashset: 
			return True 
			hashset[num] = True  
	return False
```
Time, Space Complexity: O(n)


## 189. Rotate Array
Given an array, rotate the array to the right by k steps, where k is non-negative.

>Example 1:
>Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4] 

解法一：插入
```
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        k %= n
        for _ in range(k):
            nums.insert(0, nums.pop())
```

解法二：拼接
```
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        k %= n
        nums[:] = nums[-k:] + nums[:-k]
```

## 26. Remove Duplicates from Sorted Array

Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

>Example 1:
>Given nums = [1,1,2],
>Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.

双指针：
```
class Solution:
    def removeDuplicates(self, nums: [int]) -> int:
        if not nums: return 0
        k = 1
        for i in range(1, len(nums)):
            if nums[i] != nums[i - 1]:
                nums[k] = nums[i]
                k += 1
        return k
```

## 122. Best Time to Buy and Sell Stock II
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

>Example 1:
Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.

>Example 2:
Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.

Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are engaging multiple transactions at the same time. You must sell before buying again.

```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        profit = 0
        for i in range(1, len(prices)):
            tmp = prices[i] - prices[i-1]
            if tmp > 0: profit += tmp
        return profit
```

## 225. Implement Stack using Queues
Implement the following operations of a stack using queues.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
empty() -- Return whether the stack is empty.

思路：用两个Queue，一个为主Queue一个为辅助Queue，辅助Queue每次都存入从主Queue pop出来的元素，从而辅助Queue的内容是主Queue的倒转，以实现FILO
```
import queue
class MyStack:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.q1 = queue.Queue()
        self.q2 = queue.Queue()

    def push(self, x: int) -> None:
        """
        Push element x onto stack.
        """
        self.q1.put(x)

    def pop(self) -> int:
        """
        Removes the element on top of the stack and returns that element.
        """
        # pop all q1 elements and push it into q2 to achieve FILO
        while self.q1.qsize() > 1:
            self.q2.put(self.q1.get())

        # set the top element        
        top = self.q1.get()

        # set back q1 as the primary queue and q2 as the empty one
        self.q1, self.q2 = self.q2, self.q1
        return top

    def top(self) -> int:
        """
        Get the top element.
        """
        while self.q1.qsize() > 1:
            self.q2.put(self.q1.get())
        top = self.q1.get()
        
        self.q2.put(top)
        self.q1, self.q2 = self.q2, self.q1

        return top

    def empty(self) -> bool:
        """
        Returns whether the stack is empty.
        """
        return self.q1.empty()

# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()
```

## 10.01 Sorted Merge LCCI
You are given two sorted arrays, A and B, where A has a large enough buffer at the end to hold B. Write a method to merge B into A in sorted order.

Initially the number of elements in A and B are m and n respectively.

>Example:
Input:
A = [1,2,3,0,0,0], m = 3
B = [2,5,6],       n = 3
Output: [1,2,2,3,5,6]

两个数组看作队列，每次从两个数组头部取出比较小的数字放到结果中
```
class Solution:
    def merge(self, A: List[int], m: int, B: List[int], n: int) -> None:
        """
        Do not return anything, modify A in-place instead.
        """
        sorted = []
        pa = 0
        pb = 0
        while pa < m or pb < n:
            if pa == m: 
                sorted.append(B[pb])
                pb +=1
            elif pb == n:
                sorted.append(A[pa])
                pa +=1
            elif A[pa] < B[pb]:
                sorted.append(A[pa])
                pa += 1
            else:
                sorted.append(B[pb])
                pb += 1
        A[:] = sorted
```
Time, Space Complexity: O(m+n)

## 136. Single Number
Given a non-empty array of integers, every element appears twice except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

>Example 1:
Input: [2,2,1]
Output: 1

>Example 2:
Input: [4,1,2,1,2]
Output: 4

遍历 nums 中的每一个元素
查找 hash_table 中是否有当前元素的键
如果没有，将当前元素作为键插入 hash_table
最后， hash_table 中仅有一个元素，用 popitem 获得它

```
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        hash_table = {}
        for i in nums:
            try:
                hash_table.pop(i)
            except:
                hash_table[i] = 1
        return hash_table.popitem()[0]
```
Time, Space complexity: O(n)



