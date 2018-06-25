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
                        
## 7. Reverse Integer</br><p style='color:red'>倒置数</p>
> Given a 32-bit signed integer, reverse digits of an integer.
>> Example 1:

Input: 123
Output: 321
Example 2:

Input: -123
Output: -321
Example 3:

Input: 120
Output: 21

       class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        n=x<0
        x=abs(x)
        res=0
        while x!=0:
            res=res*10+x%10
            x//=10
        if res>2**31-1:
            return 0
        return res if not n else -res
<p style='color:red'>Note:</br>重点是y=y*10+x%10;x//=10。可将x依次倒置放入Y。2**31-1=2^31-1是int的最大限界</p>
## 9. Palindrome Number<p style='color:red'>回文数</p>
> Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.
>> Input: 121
Output: true
Example 2:

Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
Example 3:

Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.

       class Solution:
       def isPalindrome(self, x):
              """
              :type x: int
              :rtype: bool
               """
              s=str(x)
              n=s[::-1]
              return n==s
              
## 13. Roman to Integer</br>
> For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as, XII, which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9. 
X can be placed before L (50) and C (100) to make 40 and 90. 
C can be placed before D (500) and M (1000) to make 400 and 900.
>> Symbol       Value</br>
I             1</br>
V             5</br>
X             10</br>
L             50</br>
C             100</br>
D             500</br>
M             1000</br>

       class Solution:
    def romanToInt(self, s):
        """
        :type s: str
        :rtype: int
        """
        dict1= {'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
        dict2= {'CM':900, 'CD': 400, 'XL': 40, 'XC': 90,'IV':4,'IX':9}            
        integer=0
        i=0
        while i<len(s):
            if i<len(s)-1 and s[i:i+2] in dict2:
                integer+=dict2[s[i:i+2]]
                i+=2
            else:
                integer+=dict1[s[i]]
                i+=1
        return integer
        
## 14. Longest Common Prefix
> Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".
>>Example 1:

Input: ["flower","flow","flight"]
Output: "fl"
Example 2:

Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
       
       class Solution:
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        if not strs:
            return ""
        
        strs.sort()
        first=strs[0]
        last=strs[-1]
        i=0
        while i<len(first) and i<len(last) and first[i]==last[i]:
            i+=1
        return first[:i]
        
## 167. Two Sum II - Input array is sorted</br>
> Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.</br>The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.</b>Note:</br>Your returned answers (both index1 and index2) are not zero-based.</br>You may assume that each input would have exactly one solution and you may not use the same element twice.</br>
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
