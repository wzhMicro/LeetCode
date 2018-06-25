# LeetCode

## 1. Two Sum</br>
> Given an array of integers, return indices of the two numbers such that they add up to a specific target.You may assume that each input would have exactly one solution, and you may not use the same element twice.

>> Example:
Given nums = [2, 7, 11, 15], target = 9,</br>
Because nums[0] + nums[1] = 2 + 7 = 9,</br>
return [0, 1]. 

       class Solution:
        def twoSum(self, nums, target):
            """
             :type nums: List[int]
            :type target: int
            :rtype: List[int]
         """
            n=len(nums)
            for i in range(n):
                j = target-nums[i]
                if j in nums:
                    k=nums.index(j)
                    if i !=k:
                        return [i,k]

## ## 167. Two Sum II - Input array is sorted</br>
> Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.</br>

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.</br>

Note:</br>

Your returned answers (both index1 and index2) are not zero-based.</br>
You may assume that each input would have exactly one solution and you may not use the same element twice.</br>
>> Example:
Input: numbers = [2,7,11,15], target = 9</br>
Output: [1,2]</br>
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.</br>
       class Solution:
    def twoSum(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype: List[int]
        """
        i = 0
        j = len(numbers)-1
        while True:
            psum = numbers[i] + numbers[j]
            if psum == target:
                return [i+1, j+1]
            elif psum > target:
                j -= 1
            else:
                i += 1
        return None
