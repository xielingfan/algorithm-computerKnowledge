#### [26.删除排序数组中的重复项]({https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/})

# 题目描述

给定一个排序数组，你需要在 原地 删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。

**示例:**

```
给定数组 nums = [1,1,2], 
函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。 
你不需要考虑数组中超出新长度后面的元素。
```

# 代码

```c++
//Java
//执行用时：1ms
//内存消耗：40.5MB
//利用快慢指针求解
class Solution {
    public int removeDuplicates(int[] nums) {
        if(nums.length == 0) return 0;
        int i = 0;
        for(int j = 1; j < nums.length; j++){
            if(nums[j] != nums[i]){//当快慢指针所指元素不相同时，更新慢指针并复制元素
                i++;
                nums[i] = nums[j];
            }
        }
        return i + 1;//返回值为慢指针的下标+1，因为数组元素下标从0开始
    }
}
```