给出一个整数数组 nums 和一个整数 k。划分数组（即移动数组 nums 中的元素），使得：

    - 所有小于k的元素移到左边
    - 所有大于等于k的元素移到右边
返回数组划分的位置，即数组中第一个位置 i，满足 nums[i] 大于等于 k。

## 快速选择算法

通过头尾指针跳过小于k的前缀和大于等于k的后缀，可以找到与第一个大于等于k的值和最后一个小于k的值。进行交换后可达到划分数组的目的，直到找到两个指针相遇为止。

伪代码：

1. 令left = 0，right = length-1。
2. 当nums[left] < k时，left指针向右移动。
3. 当nums[right] >= k时，right指针向左移动。
4. 如果left <= right，交换两个值。
5. 如果left > right，返回left作为最终结果，否则返回第二步。

```Java
public int partitionArray(int[] nums, int k) {
    if (nums == null) {
        return 0;
    }
    int left = 0, right = nums.length - 1, temp;
    while (left <= right) {
        while (left <= right && nums[left] < k) {
            left++;
        }
        while (left <= right && nums[right] >= k) {
            right--;
        }
        if (left <= right) {
            temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;
            left++;
            right--;
        }
    }
    return left;
}
```