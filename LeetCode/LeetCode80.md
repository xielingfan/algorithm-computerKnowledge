#### [80. 删除排序数组中的重复项Ⅱ](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array-ii/)

# 题目描述

给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素最多出现两次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

**示例：**

```
给定 nums = [1,1,1,2,2,3],

函数应返回新长度 length = 5, 并且原数组的前五个元素被修改为 1, 1, 2, 2, 3 。

你不需要考虑数组中超出新长度后面的元素。
```

# 代码

```java
//Java
//执行用时：1ms
//内存消耗：39.1MB
class Solution{
    public int removeDuplicates(int[] nums){
        int j = 1, count = 1;//count用于记录相同元素的个数
        for(int i = 1; i < nums.length; i++){
            if(nums[i] == nums[i-1]){//当前元素与前一个元素相同
                count++;
            }
            else{//当前元素与前一个元素不同
                count = 1;
            }
            //如果count的值小于等于2，说明
            if(count <= 2){
                nums[j++] = nums[i];
            }
        }
        return j;
    }
}
```