在数组中找到第 k 大的元素。

***

```Java
class Solution {
    public int kthLargestElement(int k, int[] nums) {
        if (nums == null || nums.length == 0){
            return -1;
        }
        return partition(nums, 0, nums.length - 1, nums.length - k);
    }
    
    private int partition(int[] nums, int start, int end, int k) {
        if (start >= end) {
            return nums[k];
        }
        
        int i = start, j = end;
        int pivot = nums[(start + end) / 2];
        
        while (i <= j) {
            while (i <= j && nums[i] < pivot) {
                i++;
            }
            while (i <= j && nums[j] > pivot) {
                j--;
            }
            if (i <= j) {
                swap(nums, i, j);
                i++;
                j--;
            }
        }
        
        if (k <= j) {
            return partition(nums, start, j, k);
        }
        if (k >= i) {
            return partition(nums, i, end, k);
        }
        return nums[k];
    }    
    
    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```