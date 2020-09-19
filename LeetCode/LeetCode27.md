```java
//Java
//双指针方法，慢指针i记录新数组元素的个数，快指针j用于遍历原数组
//会有不必要的元素复制
class Solution {
    public int removeElement(int[] nums, int val) {
        int i = 0;
        for(int j = 0; j < nums.length; j++){
            if(nums[j] != val){
                nums[i] = nums[j];
                i++;
            }
        }
        return i;
    }
}
```

```java
//Java
//双指针，分左指针和右指针，当数组中等于val的元素个数较少时效率高，因为可以减少不必要的元素复制
class Solution {
    public int removeElement(int[] nums, int val) {
        int i = 0;//左指针
        int n = nums.length;//右指针，同时还可以记录新数组的元素个数
        while(i < n){
            if(nums[i] == val){//当左指针元素等于val时，进行元素复制，并更新数组元素个数
                nums[i] = nums[n-1];
                n--;
            }else{//当左指针元素不等于val时，更新左指针
                i++;
            }
        }
        return n;
    }
}
```

