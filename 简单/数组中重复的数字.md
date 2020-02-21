找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

:利用set不含重复元素的特性

```Java
class Solution {
    public int findRepeatNumber(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for(int i = 0;i < nums.length;i++){
            set.add(nums[i]);
            if(set.size() == i) return nums[i];
        }
        return -1;
    }
}
```