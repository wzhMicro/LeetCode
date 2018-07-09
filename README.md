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
>> 输出一组数中连续的数字最大和。从第一个开始加 *num[-2,1,-3,4,-1,2,1,-5,4]</br>f[-2,1,-2,4,3,5,6,1,5]</br>主要判断条件：f[i]=f[i-1]>0?num[i]+f[i-1]:num[i].如果之前一个数小于0，不加，从本身重新开始

       for i in range(1,len(nums)):
              if num[i-1]>0:
                     num[i]+=num[i-1]
              ##else不变不用写
       return max(nums)
###主要思想是要和前一个数相加或者放弃比较难想到

## 58. Length of Last Word
> Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.
>> Example:

Input: "Hello World"
Output: 5
       
        count=0
        for i in range(len(s)-1,-1,-1):
            if s[i]!=' ':
                count+=1
            elif count!=0 and s[i]==' ':
                break
        return count
 ###遇到空格就停止。个人以为还可以用split（）[-1]。返回最后一项的长度。如果类似‘a ’,判断最后一项为空格，n+=1。直到！= ‘ ’。
 
## 66. Plus One
> Given a non-empty array of digits representing a non-negative integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.
>> Example 1:

Input: [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Example 2:

Input: [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
###开始我认为取出最后一项加一，可是想到【1，2，9，9】无法实现。所以分为3步，1.数字依次取出变成整数2.加一3.变为数组
        
        num=0
        for i in range(len(digits)):
            num+=digits[i]*10**(len(digits)-i-1)
            
        newnum=num+1
        str=[]
        while newnum>0:
            str.append(newnum%10)
            newnum//=10
        str.reverse()
        return str
        
## 67. Add Binary `2进制相加返回二进制`
> Given two binary strings, return their sum (also a binary string).

The input strings are both non-empty and contains only characters 1 or 0.
>> Example 1:

Input: a = "11", b = "1"
Output: "100"
Example 2:

Input: a = "1010", b = "1011"
Output: "10101"
###这个方法感觉有些作弊，不过这是python
       
        i=int(a,2)
        j=int(b,2)
        n=i+j

        return bin(n)[2:]
        
## 69. Sqrt(x)
> Implement int sqrt(int x).

Compute and return the square root of x, where x is guaranteed to be a non-negative integer.

Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.
>> Example 1:

Input: 4
Output: 2
Example 2:

Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since 
             the decimal part is truncated, 2 is returned.

        n=math.sqrt(x)
        return int(n)
或者不用import math也可以
           
           return int(x**0.5)
           
## 70. Climbing Stairs
> You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.
>> Example 1:

Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
Example 2:

Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step

        a=1
        b=1
        for _ in range(n):
            a,b=b,a+b
        return a
      ###这是根据斐波那契做的。如果n = 1层，可以有[1] ,   f(1) = 1种方法

如果n = 2层，可以有[1,1] ,[2],  f(2) =  2种方法

如果n = 3层，可以有[1,1,1],[1,2],[2,1], f(3) = f(1) + f(2) = 3种方法。

如果n = 4层，可以有[1,1,1,1],[1,2,1],[1,1,2],[2,1,1],[2,2] , f(5)  = f(4) + f(3) = 5种方法。

可以发现 f(n) = f(n-1) + f(n-2)</br>设S(n)表示走n级台阶的走法数量。走n级台阶，第一步只有两种选择：可以选择走1阶，然后还有S(n-1)种走法；选择走2阶，那么接下来有S(n-2)种走法。那么S(n) = S(n-1) + S(n-2)。


自己的思路一直在如何算出每层台阶的不同走法数量。但重点应该放在数量的排序上，应简单列出几个简单的看排序。

## 83. Remove Duplicates from Sorted List
> Given a sorted linked list, delete all duplicates such that each element appear only once.
>> Example 1:

Input: 1->1->2
Output: 1->2
Example 2:

Input: 1->1->2->3->3
Output: 1->2->3

### 最基本的删除操作，主要学习的是“摘链”的过程。所谓删除一个元素实际上是令这个节点的前一个元素直接指向这个节点的后一个元素（python特性是当一块内存无引用时，自动清空）。
       prex=head
        while prex and prex.next:
            if prex.val==prex.next.val:
                prex.next=prex.next.next
            else:
                prex=prex.next
        return head
## 88. Merge Sorted Array
> Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:

The number of elements initialized in nums1 and nums2 are m and n respectively.
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2.
>> Example:

Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
       
         i,j,k=m-1,n-1,m+n-1 ##i,j,k为数组中元素的位置，倒着取
        while i>=0 and j>=0:
            if nums1[i]>nums2[j]:
                nums1[k]=nums1[i]
                i-=1
            else:
                nums1[k]=nums2[j]
                j-=1
            k-=1
    
        if i<0:##如果从nums1中不取，则nums1就是nums2的n个项
             nums1[:k+1]=nums2[:j+1]
             
 ###第二种方法比较简单：
       
       nums1[:m+n]=nums1[0:m]+nums2[0:n]
       nums1.sort()

## 100. Same Tree
> Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.
>> Example 1:

Input:     1         1
          / \       / \
         2   3     2   3
        [1,2,3],   [1,2,3]

Output: true
Example 2:

Input:     1         1
          /           \
         2             2
        [1,2],     [1,null,2]

Output: false
Example 3:

Input:     1         1
          / \       / \
         2   1     1   2
        [1,2,1],   [1,1,2]

Output: false

        if not p and not q:
            return True
        if not p or not q:
            return False
        if p.val!=q.val:
            return False
        return self.isSameTree(p.left,q.left) and self.isSameTree(p.right,q.right)
        
## 101. Symmetric Tree `对称树`
> Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).
>> For example, this binary tree [1,2,2,3,4,4,3] is symmetric:
    1
   / \
  2   2
 / \ / \
3  4 4  3
But the following [1,2,2,null,3,null,3] is not:
    1
   / \
  2   2
   \   \
   3    3
   
### 其实就是把same tree相同树的return改了一下，相同树是左=左，右=右。对称树是左=右，右=左。只要稍作修改即可             
        def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if not root:
            return True
        return self.mirror(root.left, root.right)
    
    def mirror(self, left, right):
        if not left and not right:
            return True
        if not left or not right:
            return False
        if left.val != right.val:
            return False
        return self.mirror(left.right, right.left) and self.mirror(left.left, right.right)

## 104. Maximum Depth of Binary Tree `二叉树最大深度`
> Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Note: A leaf is a node with no children.
>> Example:

Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its depth = 3.

       def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        left=1 ##左右各有一个计数器
        right=1
        if not root:##到此为止
            return 0
        if root.left:
            left=1+self.maxDepth(root.left)
        if root.right:
            right=1+self.maxDepth(root.right)
        
        return max(left,right)##返回一个最大值
        
## 107. Binary Tree Level Order Traversal II `二叉树遍历（从底部）`
> Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
>> Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its bottom-up level order traversal as:

[
  [15,7],
  [9,20],
  [3]
]
        
        def levelOrderBottom(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        str=[]
        self.order(root,0,str)
        return str[::-1]
    
    def order(self,node,depth,str):
        if not node:
            return #循环下面的if直到没有左右子树就返回输出
        
        if len(str)==depth:  #到达这一层后加入一个空的[]
                str.append([])
                
        self.order(node.left,depth+1,str) #继续遍历左子树
        str[depth].append(node.val) #插入根节点的值到str的第‘depth’个位置的[]
        self.order(node.right,depth+1,str) #遍历右边
            #先遍历左边再插入再遍历右边这样保证输入顺序
       
## 108. Convert Sorted Array to Binary Search Tree `数组变二叉查找树`

> Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
>> Example:

Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:
      0
     / \
   -3   9
   /   /
 -10  5
       
       ###从中间切开，从右往左，
         
         def sortedArrayToBST(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        return self.convert(nums,0,len(nums)-1)
    
    def convert(self,nums,left,right):
        if left > right:
            return None
        mid=(left+right)//2
        root=TreeNode(nums[mid])
        root.left= self.convert(nums,left,mid-1)
        root.right=self.convert(nums,mid+1,right)
        return root
## 110. Balanced Binary Tree `题目意思是给定一颗树，判断是否高度平衡，即左右子树的高度差不超过1`
> Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

>>Example 1:

Given the following tree [3,9,20,null,null,15,7]:


    3
    
   / \
   
  9  20
  
    /  \
    
   15   7
Return true.

Example 2:

Given the following tree [1,2,2,3,3,null,null,4,4]:
      
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
Return false.
###根据定义，递归地判断
       
        def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        
        return self.test(root)!=-1 ##if==-1False.else true
    
    def test(self,node):
        if not node:
            return 0
        
        lh=self.test(node.left)
        rh=self.test(node.right)
        if lh==-1 or rh==-1:
            return -1
        if abs(lh-rh)>1:
            return -1
        
        return 1+max(lh,rh)
        
###节点为空 树高度为零  否则树的高度为左子树的高度和右子树的高度中最大的那个加一，加一的意思就是加上自身这个节点的高度

判断左子树和右子树高度是否相差大于一  如果大于一 返回一个标记数  可以用-1标记

## 111. Minimum Depth of Binary Tree `找最小深度`
> Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Note: A leaf is a node with no children.
>> Example:

Given binary tree [3,9,20,null,null,15,7],
    3
    
   / \
   
  9  20
  
    /  \
    
   15   7
   
return its minimum depth = 2.

        def minDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        return self.min(root)
    
    def min(self,node):
        if not node:
            return 0
        lh=self.min(node.left)
        rh=self.min(node.right)
        if not lh or not rh:
            return 1+lh+rh #2.运行至子树为空，返回最终值，加1为根节点的高度
        return min(lh,rh)+1 #1.将左右子树小的加1返回minhanshu，大的不管-->2
        
## 112. Path Sum `路径之和等于sum返回TRUE`
> Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

Note: A leaf is a node with no children.
>> Example:

Given the below binary tree and sum = 22,

      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.

       def hasPathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: bool
        """
        if not root:
            return False
        
        sum -= root.val
        if sum==0 and not root.left and not root.right:
            return True
        return self.hasPathSum(root.left,sum) or self.hasPathSum(root.right,sum)
### 自己的思想是在通过加法得到。实际用减法更好，当自减到0并且没有子树时返回真。

## 118. Pascal's Triangle `生成杨辉三角形`
> Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.


In Pascal's triangle, each number is the sum of the two numbers directly above it.
>> Example:

Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
       
       def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
        if numRows==0:
            return []
        str=[[1]]
        for i in range(1,numRows):
            str.append([1]) #向str数组中插入【1】
           for j,k in zip(str[-2][:-1],str[-2][1:]):#J,K分别为str中倒数第二个数组中的最后一个起和第【1】个起（不是第‘0’个，因为numRows=2时，不存在，保证第二个数组是【1，1】）
                str[-1].append(j+k) #向最后一个数组中插入J+K
            str[-1].append(1) #最后一个数组再加一个1
        return str
        
## 119. Pascal's Triangle II `杨辉三角形(只生成需要的那一行)`
> Given a non-negative index k where k ≤ 33, return the kth index row of the Pascal's triangle.

Note that the row index starts from 0.
>> Example:

Input: 3
Output: [1,3,3,1]

        def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
        if rowIndex==0:
            return [1]
        
        str=[1]
        for i in range(rowIndex):
            str=[1]+[x+y for x,y in zip(str[:],str[1:])]+[1] #'+'的拼接作用了解一下
        return str
## 121. Best Time to Buy and Sell Stock
> Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.
>> Example 1:

Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
Example 2:

Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.

       profit=0
       buy=float('inf')
       for i in prices:
              if i>buy:
                     profit= max(profit,i-buy)
              else:
                     buy=i
       return profit
## 122. Best Time to Buy and Sell Stock II
> Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).
>> Example 1:

Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
Example 2:

Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
Example 3:

Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.

       return sum([max(prices[i]-prices[i-1],0) for i in range(1,len(prices))])
       
   ###solution 2
        
        profit=0
        if not prices:
            return 0
        lastp=prices[0]
        for i in prices:
            if lastp<i:
                profit+=i-lastp
            lastp=i
        return profit
       
## 125. Valid Palindrome `有效回文`
> Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

Note: For the purpose of this problem, we define empty string as valid palindrome.
>> Example 1:

Input: "A man, a plan, a canal: Panama"
Output: true
Example 2:

Input: "race a car"
Output: false
###意思是只保留数字和字母，忽略符号，剩下的为回文字符串</br>
思路分为2步：1.大小写统一。2.过滤符号。放入list  !isalnum()方法检测字符串是否由字母和数字组成。

        clean=[i for i in s.lower() if i.isalnum()]
        t=clean[::-1]
        return clean==t
        
## 136.Single Number
> Given a non-empty array of integers, every element appears twice except for one. Find that single one.

Note:

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?
>> Example 1:

Input: [2,2,1]
Output: 1
Example 2:

Input: [4,1,2,1,2]
Output: 4

###我的方法，比较笨，比较慢。排序后前后都不同的就是那个数

       def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        nums.sort()
        if len(nums)==1:
            return nums[0]
        for i in range(0,len(nums)-1):
            if i!=0 and i!=len(nums)-1 and nums[i-1]!=nums[i] and nums[i]!=nums[i+1]:
                return nums[i]
            elif nums[0]!=nums[1]:
                return nums[0]
            elif nums[-1]!=nums[-2]:
                return nums[-1]
 ### 第二种方法：利用位操作。位操作的异或（^)，他的其中一个属性是，n^n = 0, 0^n = n。只要将所有的数都进行异或就得到出现一次的数。
       if len(nums)==1:
              return nums[0]
       result=0
       for i in nums:
            result^=i
       return result

## 141. Linked List Cycle
> Given a linked list, determine if it has a cycle in it.
       
       def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        fast=slow=head
        while fast and fast.next:
            slow=slow.next
            fast=fast.next.next
            if fast is slow: ##is faster than==
                return True            
        return False
 ### 设置一慢一快两个指针，当快的追上慢的，存在循环   
## 155. Min Stack
> Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
getMin() -- Retrieve the minimum element in the stack.
>> Example:
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.


        def __init__(self):
        """
        initialize your data structure here.
        """
        self.stack=[]  #正常栈
        self.min=[]         #只放最小值
              
    def push(self, x):
        """
        :type x: int
        :rtype: void
        """
        self.stack.append(x)       #正常操作入栈
        if not self.min or x<=self.min[-1]:      #如果比之前小或等于，放入MIN 栈中
            self.min.append(x)
    def pop(self):
        """
        :rtype: void
        """
        x=self.stack.pop()  #出
        if x==self.min[-1]:
            self.min.pop()  #如果正常栈出了，最小值栈也出去

    def top(self):
        """
        :rtype: int
        """
        return self.stack[-1]      #返回最后一项

    def getMin(self):
        """
        :rtype: int
        """
        if not self.min:
            return None
        return self.min[-1]        #返回最小值的最后一项
##  157. Read N Characters Given Read4
> The API: int read4(char *buf) reads 4 characters at a time from a file.

The return value is the actual number of characters read. For example, it returns 3 if there is only 3 characters left in the file.

By using the read4 API, implement the function int read(char *buf, int n) that reads n characters from the file.

Note:
The read function will only be called once for each test case.
>> 每次可以从一个文件中最多读出4个字符，如果文件中的字符不足4个字符时，返回准确的当前剩余的字符数。
              
              def read(self,buff,n):
                     total_chars,last,chars=0,1
                     while last_chars ==4 and total_chars<n:
                            buf4=[""]*4
                            last_chars=min(read4(buf4),n-total_chars)
                            buf[total:total_chars+last_chars]=buf4
                            total_chars+=last_chars
                     return total_chars
## 160. Intersection of Two Linked Lists
> Write a program to find the node at which the intersection of two singly linked lists begins.
>> For example, the following two linked lists:

A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
begin to intersect at node c1.

Notes:

If the two linked lists have no intersection at all, return null.
The linked lists must retain their original structure after the function returns.
You may assume there are no cycles anywhere in the entire linked structure.
Your code should preferably run in O(n) time and use only O(1) memory.

        if not headA or not headB:
            return None
        A,B=headA,headB
        
        while A is not B:
            A=headB if not A else A.next
            B=headA if not B else B.next
        return A

## 168. Excel Sheet Column Title
> Given a positive integer, return its corresponding column title as appear in an Excel sheet.
>>  For example:

    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
    ...
Example 1:

Input: 1
Output: "A"
Example 2:

Input: 28
Output: "AB"
Example 3:

Input: 701
Output: "ZY"

       def convertToTitle(self, n):
        """
        :type n: int
        :rtype: str
        """
        res=''
        while n>0:
            n,rem=divmod(n-1,26)
            res+=chr(ord('A')+rem)
        res2=res[::-1]
        return res2

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
## 169. Majority Element
> Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.
>> Example 1:

Input: [3,2,3]
Output: 3
Example 2:

Input: [2,2,1,1,1,2,2]
Output: 2

###这个题非常有意思。因为这个数字出现的次数最少为n/2次。所以有一半以上是这个数字。将数组排序后中间那个数一定是这个数

       nums.sort()
       return nums[len(nums)//2]
       
## 170 - Two Sum III
> Design and implement a TwoSum class. It should support the following operations: add and find.
>> add - Add the number to an internal data structure.
find - Find if there exists any pair of numbers which sum is equal to the value.

For example,

add(1); add(3); add(5);
find(4) -> true
find(7) -> false

       def __init__(self):
        self.dic = {}

    def add(self, number):
        if number not in self.dic:
            self.dic[number] = 1
        else:
            self.dic[number] += 1

    def find(self, value):
        dic = self.dic
        for num in dic:
            if value - num in dic and (value - num != num or dic[num] > 1):
                return True
        return False

## 171. Excel Sheet Column Number
> Given a column title as appear in an Excel sheet, return its corresponding column number.
>> For example:

    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...
Example 1:

Input: "A"
Output: 1
Example 2:

Input: "AB"
Output: 28
Example 3:

Input: "ZY"
Output: 701

       def titleToNumber(self, s):
        """
        :type s: str
        :rtype: int
        """
        sum=0
        for i in range(len(s)):
            if i is not s[len(s)-1]:
                sum+=26**(len(s)-1-i)*(ord(s[i])-64)
            else:
                sum+=ord(s[i])-64
        return sum
        
 ## 172. Factorial Trailing Zeroes
 > Given an integer n, return the number of trailing zeroes in n!.
 >> Example 1:

Input: 3
Output: 0
Explanation: 3! = 6, no trailing zero.
Example 2:

Input: 5
Output: 1
Explanation: 5! = 120, one trailing zero.
###实际是返回2*5的个数，由于含有2的因数个数多于5，所以只有选取有5的。但是25=5*5，所有有两个5.所以不仅计算n/5个数，还要n/5/5,n/5/5/5.......
       count=0
       i=1
       while n//5**i>0:
              count+=n//5**i
              i+=1
       return count
       
## 189. Rotate Array
> Given an array, rotate the array to the right by k steps, where k is non-negative.
>> Example 1:

Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
Example 2:

Input: [-1,-100,3,99] and k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
       
       n=len(nums)
       k%=n
       nums[:]=nums[n-k:]+nums[:n-k]
       
## 190. Reverse Bits
> Reverse bits of a given 32 bits unsigned integer.
>> Example:

Input: 43261596
Output: 964176192
Explanation: 43261596 represented in binary as 00000010100101000001111010011100, 
             return 964176192 represented in binary as 00111001011110000010100101000000.
             
              num=bin(n)[:1:-1]
              return int(num+'0'*(32-len(num)),2)
              
## 191. Number of 1 Bits  `二进制中1的个数`
> Write a function that takes an unsigned integer and returns the number of '1' bits it has (also known as the Hamming weight).
>> Input: 11
Output: 3
Explanation: Integer 11 has binary representation 00000000000000000000000000001011 
Example 2:

Input: 128
Output: 1
Explanation: Integer 128 has binary representation 00000000000000000000000010000000


### 多种做法
1.            
              
                     return bin(n).count('1')
2.
                     
                     num=bin(n)[2:]
                     count=0
                     for i in num:
                            if i=='1':
                                   count+=1
                      return count
3. 
### n&n-1非常重要
将二进制最低位1换为0.更换次数即为结果
                     
                     count=0
                     whilr n>0:
                            count+=1
                            n&n-1
                     return count
                     
## 198. House Robber
> You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.
>> Example 1:

Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
Example 2:

Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
### 假设有n家，那么你要判断“偷第n家不偷第n-1家且前n-2家尽量多的偷”和“不偷第n家且前n-1家尽量多的偷”，哪个得到的钱多偷哪个。 
       def rob(self, nums):
              """
        :type nums: List[int]
        :rtype: int
        """
        
              n=len(nums)
              if n==0:
                     return 0
              if n==1:
                     return nums[0]
              if n==2:
                     return max(nums[0],nums[1])
               
              money =[0]*n #total money
              money[0]=nums[0]
              money[1]=max(nums[0],nums[1])
              for i in range(2,n):
                     money[i]=max(money[i-2]+nums[i],money[i])
              return money[n-1]
              
## 202. Happy Number  
> Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

>> Example: 

Input: 19
Output: true
Explanation: 
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1

       dic={}
       while True:
              dic[n]=True
              sum=0
              while n:
                     sum+=(n%10)**2
                     n//10
              if sum==1:
                     return True
              elif sum in dic:
                     return False
              else:
                     n=sum
           
           
  ###第二种不太明白
              while true:
                     if n==1:
                            return True
                     if n==4:
                            return False
                     n=sum([int(c)**2  for c in str(n)])

## 203. Remove Linked List Elements
> Remove all elements from a linked list of integers that have value val.
>> Example:

Input:  1->2->6->3->4->5->6, val = 6
Output: 1->2->3->4->5

      class ListNode:
       #     def __init__(self, x):
       #         self.val = x
       #         self.next = None

       class Solution:
              def removeElements(self, head, val):
        """
        :type head: ListNode
        :type val: int
        :rtype: ListNode
        """
                     pre=now=ListNode(0)
                     pre.next=head
                     while head:
                            if head.val==val:
                                   pre.next=head.next
                            else:
                                   pre=pre.next
                            head=head.next
                     return now.next
## 204. Count Primes
> Count the number of prime numbers less than a non-negative number, n.
>> Example:

Input: 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
       
       if n<3:
              return 0
       str=[1]*n
       str[0]=str[1]=0
       for i in range(2,int(n**0.5)):
              if str[i]==1:
                     str[i**2:n:i]=[0]*len(str[i**2:n:i])
        return sum(str)
## 205. Isomorphic Strings
> Given two strings s and t, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.
>> Example 1:

Input: s = "egg", t = "add"
Output: true
Example 2:

Input: s = "foo", t = "bar"
Output: false
Example 3:

Input: s = "paper", t = "title"
Output: true

       hashmap={}
       mapval={}
       for i in range(len(s)):
              if s[i] in hashmap:
                     if hashmap[s[i]]!=t[i]:
                            return False
              elif t[i] in mapval:
                     return False
                     
              else:
                     hashmap[s[i]]=t[i]
                     mapval[t[i]]=True
        return True
## 206. Reverse Linked List
> Reverse a singly linked list.

Example:

Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
Follow up:

A linked list can be reversed either iteratively or recursively. Could you implement both?


       prev=None
       curr=head
       while curr!=None:
              temp=curr.next
              curr.next=prev
              prev= curr
              curr=temp
       return prev
       
  ### 压栈再出个弹出
  
       curr=head
       new=[]
       while curr:
              new.insert(0,curr.val)
              curr=curr.next
       
       p=head
       for i in new:
              p.val=i
              p=p.next
       return head

## 217. Contains Duplicate
> Given an array of integers, find if the array contains any duplicates.

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.
>> Example 1:

Input: [1,2,3,1]
Output: true
Example 2:

Input: [1,2,3,4]
Output: false
Example 3:

Input: [1,1,1,3,3,4,3,2,4,2]
Output: true


###第一种，排序后有没有相邻一样的

       def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        nums.sort()
        for i in range(0,len(nums)-1):
            if nums[i]==nums[i+1]:
                return True
        return False
### 第二种，没有重复的数组相当于集合，利用Python的set，将数组转换成集合，若长度与原来相等则说明没有重复。

              
              return len(nums)!=len(set(nums))
### 第三种，利用字典记录

       dic={}
        for i in nums:
            if i in dic:
                return True
            dic[i]=True
        return False
 
## 219. Contains Duplicate II
> Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k.
>> Example 1:

Input: nums = [1,2,3,1], k = 3
Output: true
Example 2:

Input: nums = [1,0,1,1], k = 1
Output: true
Example 3:

Input: nums = [1,2,3,1,2,3], k = 2
Output: false

       dic={}
       for i in range(len(nums)):
              if nums[i] in dic and i-dic[nums[i]]<=k:
                     return True
              else:
                     dic[nums[i]]=i
       return False
       
   ### 第二种用enumerate（）
## 226. Invert Binary Tree
> Example:

Input:

     4
   /   \
  2     7
 / \   / \
1   3 6   9
Output:

     4
   /   \
  7     2
 / \   / \
9   6 3   1
       
       def tree(self,root):
              if root:
                     left=self.tree(root.left)
                     right=self.tree(root.right)
                     root.left,root.right= right,left
              return root

## 231 power of two `2次幂`
       
    简单的题：n&n-1
       
              if n>0:
                     return n&(n-1)==0
              return False
