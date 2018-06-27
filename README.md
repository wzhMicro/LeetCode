# LeetCode 学习笔记</br>从easy到Mid到Hard。每日不定更新

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
                        
## 7. Reverse Integer</br> `倒置数`
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
### Note: </br>重点是y=y*10+x%10;x//=10。可将x依次倒置放入Y。2**31-1=2^31-1是int的最大限界



## 9. Palindrome Number`回文数`
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
### Note:</br>n是从后往前取值
              
## 13. Roman to Integer</br>`罗马到数字`
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
        
        
### Note:</br>字典     
## 14. Longest Common Prefix`最长公共前缀`
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
        
        
### Note:</br>重点是sort（），如果有公共前缀，排序之后可按公共字幕排序，则可拿出相同字符 

## 20. Valid Parentheses `有效括号`
> Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
>> Example 1:

Input: "()"
Output: true
Example 2:

Input: "()[]{}"
Output: true
Example 3:

Input: "(]"
Output: false
Example 4:

Input: "([)]"
Output: false
Example 5:

Input: "{[]}"
Output: true

       class Solution:
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        str=[]
        match={'(':')','{':'}','[':']'}
        for i in s:
            if i in match:
                str.append(i)
            else:
                if not str or match[str.pop()]!=i:
                    return False
        return not str

### Note:</br>利用栈遍历S将括号放入str(如果在match中有)，最后弹出S，作比较，如果身体乳不为空返回F。match[str.pop()]即为此括号的另一半（pop出的值在字典中Value为另一半）

## 21. Merge Two Sorted Lists
> Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

>> Example:

Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4

               prev=dummy=ListNode(None)
        while l1 and l2:
            if l1.val<l2.val:
                prev.next=l1
                l1=l1.next
            else:
                prev.next=l2
                l2=l2.next
            prev=prev.next

        prev.next=l1 or l2
        return dummy.next
        
## 26. Remove Duplicates from Sorted Array
> Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
>> Example 1:

Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
Example 2:

Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.

       n=0
       for i in range(len(nums)):
              if i==0 or nums[i]!=nums[i-1]:
                     nums[n]=nums[i]
                     n+=1
       return n
       
###返回类型和输入类型。！！ 第一个数肯定是不重复的，后一个数和之前不一样则将第N个变为那个数，同时N++。通过索引迭代List和string的元素要用range。注意返回的len不是这个列表。


##27. Remove Element
>Given an array nums and a value val, remove all instances of that value in-place and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.
>> Example 1:

Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.

It doesn't matter what you leave beyond the returned length.
Example 2:

Given nums = [0,1,2,2,3,0,4,2], val = 2,

Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.

Note that the order of those five elements can be arbitrary.

It doesn't matter what values are set beyond the returned length.

               n=0
        for i in range(len(nums)):
            if nums[i]!=val:
                nums[n]=nums[i]
                n+=1
        return n
### 和26题相似

## 28. Implement strStr()
> Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.
>> Example 1:

Input: haystack = "hello", needle = "ll"
Output: 2
Example 2:

Input: haystack = "aaaaa", needle = "bba"
Output: -1

          return haystack.find(needle)
          
### 神奇，python的魅力还可以这样写，一行搞定

## 35. Search Insert Position
> Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.
>> Example 1:

Input: [1,3,5,6], 5
Output: 2
Example 2:

Input: [1,3,5,6], 2
Output: 1
Example 3:

Input: [1,3,5,6], 7
Output: 4
Example 4:

Input: [1,3,5,6], 0
Output: 0
       
        left=0
        right=len(nums)
        while left<=right and left<len(nums) and right>=0:
            mid=(left+right)//2
            if target==nums[mid]:
                return mid
            if target <nums[mid]:
                right=mid-1
            else:
                left=mid+1
        return left
        
### 类似排序第二种方法：
       num=[i for i in nums if i<target]
        return len(num)
        
## 38. Count and Say
> The count-and-say sequence is the sequence of integers with the first five terms as following:

1.     1
2.     11
3.     21
4.     1211
5.     111221
1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.
>>Example 1:

Input: 1
Output: "1"
Example 2:

Input: 4
Output: "1211"
>>其实就是对上一个数进行遍历统计有多少个“几”。思路就是进行遍历从第一个数开始，记录为j，如果下一个数相同，就计数+1，直到不相同，将j重新设置为最新的数字，最新的数字变为计数的count+num，并继续进行遍历，将count重新置为1.

        if n==0:
            return '0'
        if n==1:
            return '1'
        curnum='11'
        for _ in range(2,n):
            oldnum=curnum
            curnum=''
            count=1
            firstnum=oldnum[0]
            for j in range(1,len(oldnum)):
                if oldnum[j]==firstnum:
                    count+=1
                else: 
                    curnum += str(count)+firstnum
                    firstnum=oldnum[j]
                    count=1
            curnum += str(count)+firstnum
        return curnum
###注意count是int型，要变成str才可以相加

## 53. Maximum Subarray
> Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.
>> Example:

Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
>> 输出一组数中连续的数字最大和。从第一个开始加 *num[-2,1,-3,4,-1,2,1,-5,4]</br>f[-2,1,-2,4,3,5,6,1,5]</br>主要判断条件：f[i]=f[i-1]>0?num[i]+f[i-1]:num[i].如果之前一个数小于0，这部加，从本身重新开始

       for i in range(1,len(nums)):
              if num[i-1]>0:
                     num[i]+=num[i-1]
              ##else不变不用写
       return max(nums)
###主要思想是要和前一个数相加或者放弃比较难想到
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


### Note:</br>设置前后两个哨兵
