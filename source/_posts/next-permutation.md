---
title: Leetcode 31 下一个排列
date: 2020-02-17 19:10:18
tags:
categories:
  - 算法
---
## 题目
整数数组的一个 排列  就是将其所有成员以序列或线性顺序排列。
<!--more-->
- 例如，arr = [1,2,3] ，以下这些都可以视作 arr 的排列：[1,2,3]、[1,3,2]、[3,1,2]、[2,3,1] 。
整数数组的 下一个排列 是指其整数的下一个字典序更大的排列。更正式地，如果数组的所有排列根据其字典顺序从小到大排列在一个容器中，那么数组的 下一个排列 就是在这个有序容器中排在它后面的那个排列。如果不存在下一个更大的排列，那么这个数组必须重排为字典序最小的排列（即，其元素按升序排列）。

- 例如，arr = [1,2,3] 的下一个排列是 [1,3,2] 。
- 类似地，arr = [2,3,1] 的下一个排列是 [3,1,2] 。
而-  arr = [3,2,1] 的下一个排列是 [1,2,3] ，因为 [3,2,1] 不存在一个字典序更大的排列。
给你一个整数数组 nums ，找出 nums 的下一个排列。

必须 原地 修改，只允许使用额外常数空间。

## 算法
1. 从后向前查找第一个相邻升序的元素对(i，j), A[i] < A[j] =>(j,end)必然降序 (无升序元素对=>[begin,end]降序，直接步骤4逆转)
2. 在[j,end) 从后向前找第一个满足A[k] > A[i]
3. 交换A[i],A[k] => (j,end)必然降序
4. 逆转(j,end)

![](step1.png)
![](step2.png)
![](step3.png)
![](step4.png)

## code
```java
class Solution {
    public void nextPermutation(int[] nums) {
        int len = nums.length;
        if(len<=1) return;
        int j = len-1;
        int i = j-1;
        while(i>=0 && nums[i]>=nums[j]) {
            i--;
            j--;
        }
        if(i>=0) {
            int k=len-1;
            while(k>j && nums[k]<=nums[i]) {
                k--;
            }
            swap(nums, i, k);
        }

        reverse(nums, j, len-1);
    }

    private void reverse(int[] nums, int begin, int end) {
        int len = end-begin+1;
        if(len == 1) return;
        int start = len/2+len%2+begin;
        while (start<=end) {
            swap(nums, start, begin+end-start);
            start++;
        }
    }

    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i]=nums[j];
        nums[j]=tmp;
    }
}
```