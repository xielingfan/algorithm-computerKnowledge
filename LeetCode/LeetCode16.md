[16.最接近的三数之和](https://leetcode-cn.com/problems/3sum-closest/)

# 题目描述

给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

**示例:**

```
输入：nums = [-1,2,1,-4], target = 1
输出：2
解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。
```

# 题解

暴力解法的时间复杂度为O(n³)，会超过题目时间限制。

使用排序+双指针方法，可以将算法的时间复杂度优化为O(n²)。

不妨设排序后数组升序排列，固定a（a一开始为排序后数组的第一个元素，并利用a做遍历），每轮遍历中a的下标为i，a+b+c的目标值为target；令双指针中左指针元素为b，右指针元素为c，b初始下标为i+1，c初始下标为n-1，其中n为数组元素个数。那么当a+b+c>=target时，令右指针左移一位；当a+b+c<target时，令左指针右移一位。那么为什么这么做呢？分析可知，当a+b+c>=target时，因为数组升序排列，如果令左指针右移，那么三数之和与target的差距会越来越大，所以当c的位置为pc时，此时b的位置pb就是可以令三数之和最接近target；这时就不用在考虑pc，直接领pc-1即可。

两个**小优化**，只能优化运行时间，不能优化时间复杂度。

1. 当三数之和等于target时，直接返回结果，不再继续循环
2. 因为排序后数组有序，所以更新左右指针时可以判断是否与之前指针指向的值相同，相同则继续更新该指针。

# 代码

```java
//Java
//执行用时：8ms
//内存消耗：39.1MB
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int n = nums.length;
        int ans = 0;
        int diff = 100010;
        for(int first = 0; first < n; first++){
            int second = first + 1;
            int third = n - 1;
            while(second < third){
                if(Math.abs(nums[first] + nums[second] + nums[third] - target) < diff){
                        diff = Math.abs(nums[first] + nums[second] + nums[third] - target);
                        ans = nums[first] + nums[second] + nums[third];
                        if(ans == target){
                            return ans;
                        }
                }
                if(nums[first] + nums[second] + nums[third] >= target ){
                    third--;
                    if(nums[third] == nums[third+1]){
                        third--;
                    }
                }else{
                    second++;
                    if(nums[second] == nums[second-1]){
                        second++;
                    }
                }
            }
        }
        return ans;
    }
}
```

