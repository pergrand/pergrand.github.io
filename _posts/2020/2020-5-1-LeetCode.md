---
layout:     post
title:      LeetCode
subtitle:   LeetCode
date:       2020-5-1
author:     lowe
header-img: img/post-bg-github-cup.jpg
keywords_post:  "LeetCode"
catalog: true
tags:
    - LeetCode

---
><br/>两数之和
><br/>三数之和

[题库两数之和](https://leetcode-cn.com/problems/two-sum/)

************<两数之和>方法一************

    1.思路：num2 = target -num1 判断num2是否在list ;如果在查找num2的索引
    2.优化1遍历list时 在num1时只看num1之前或者之后是否有 num2
    3.优化2 字典直接取num1和num2的下标
   ```python
   def twoSum(nums, target):
       dct={}
       for i,num in enumerate(nums):
           if target - num in dct:
               return [i, dct[target - num]]
           dct[num] = i
   nums = [2,7,6,9]
   target = 9
   ```    

************<两数之和>方法二************
   ```python
   def twoSum2(nums, target):
       lens = len(nums)
       j=-1
       for i in range(1,lens):
           temp = nums[:i]
           if (target - nums[i]) in temp:
               j = temp.index(target - nums[i])
               break
       if j>=0:
           return [j,i]
   ```

************<三数之和>************
```python
 def threeSum(nums:[int],target) -> [[int]]:  输入数组list和目标，返回[[]]
       n = len(nums)
       if (not nums or n < 3):  如果长度小于3 或者空返回空
           return []
       nums.sort()  数组排序
       res = []
       for i in range(n):   遍历数组
           if (nums[i] > target):  如果当前元素大于目标值就可以终止了
               return res
           if (i > 0 and nums[i] == nums[i - 1]):   重复元素跳过
               continue
           L = i + 1   左指针
           R = n - 1   右指针
           while (L < R):   循环 L<R  时间复杂度：n方
               if (nums[i] + nums[L] + nums[R] == target):   等于目标值
                   res.append([nums[i], nums[L], nums[R]])
                   while (L < R and nums[L] == nums[L + 1]):  判断左界和右界是否和下一位置重复，去除重复解。并同时将 L,RL,R 移到下一位置，寻找新的解
                       L = L + 1
                   while (L < R and nums[R] == nums[R - 1]):
                       R = R - 1
                   L = L + 1
                   R = R - 1
               elif (nums[i] + nums[L] + nums[R] > target):   三数之和大于目标，说明 nums[R] 太大，R左移
                   R = R - 1
               else:   三数之和小于目标，说明 nums[L] 太小，L右移
                   L = L + 1
       return res
   
   
   nums = [-1, -2, 3, 4,-3]
   target = 0
   print(threeSum(nums, target))
  
``` 