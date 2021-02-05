1. 在n个物品中挑选若干物品装入背包，最多能装多满？假设背包的大小为m，每个物品的大小为A[i] (01背包)

```Java
public int backPack(int m, int[] A) {
    int[] dp = new int[m + 1];
    for (int i = 0; i < A.length; i++) {
        for (int j = m; j >= A[i]; j--) {
            dp[j] = Math.max(dp[j], dp[j - A[i]] + A[i]);
        }
    }
    return dp[m];
}
```

***

2. 有 n 个物品和一个大小为 m 的背包. 给定数组 A 表示每个物品的大小和数组 V 表示每个物品的价值.问最多能装入背包的总价值是多大? (01背包)

```Java
public int backPackII(int m, int[] A, int[] V) {
    int[] dp = new int[m + 1];
    for (int i = 0; i < A.length; i++) {
        for (int j = m; j >= A[i]; j--) {
            dp[j] = Math.max(dp[j], dp[j - A[i]] + V[i]);
        }
    }
    return dp[m];
}
```

***

3. 给定 n 种物品, 每种物品都有无限个. 第 i 个物品的体积为 A[i], 价值为 V[i]. 再给定一个容量为 m 的背包. 问可以装入背包的最大价值是多少? (完全背包)

```Java
public int backPackIII(int[] A, int[] V, int m) {
    int[] dp = new int[m + 1];
    for (int i = 0; i < A.length; i++) {
        for (int j = A[i]; j <= m; j++) {
            dp[j] = Math.max(dp[j], dp[j - A[i]] + V[i]);
        }
    }
    return dp[m];
}
```

***

4. 给出 n 个物品, 以及一个数组, nums[i]代表第i个物品的大小, 保证大小均为正数并且没有重复, 正整数 target 表示背包的大小, 找到能填满背包的方案数。每一个物品可以使用无数次。 (完全背包)

```Java
public int backPackIV(int[] nums, int target) {
    int[] dp = new int[target + 1];
    dp[0] = 1;
    for (int i = 0; i < nums.length; i++) {
        for (int j = nums[i]; j <= target; j++) {
            dp[j] += dp[j - nums[i]];
        }
    }
    return dp[target];
}
```

***

5. 给出 n 个物品, 以及一个数组, nums[i] 代表第i个物品的大小, 保证大小均为正数, 正整数 target 表示背包的大小, 找到能填满背包的方案数。每一个物品只能使用一次。 (01背包)

```Java
public int backPackV(int[] nums, int target) {
    int[] dp = new int[target + 1];
    dp[0] = 1;
    for (int i = 0; i < nums.length; i++) {
        for (int j = target; j >= nums[i]; j--) {
            dp[j] += dp[j - nums[i]];
        }
    }
    return dp[target];
}
```

***

6. 假设你身上有 n 元，超市里有多种大米可以选择，每种大米都是袋装的，必须整袋购买，给出每种大米的重量，价格以及数量，求最多能买多少公斤的大米。(多重背包)

```Java
public int backPackVII(int n, int[] prices, int[] weight, int[] amounts) {
    int[] dp = new int[n + 1];
    for (int i = 0; i < prices.length; i++) {
        for (int j = n; j > 0; j--) {
            for (int k = 1; k <= amounts[i] && k * prices[i] <= j; k++) {
                dp[j] = Math.max(dp[j], dp[j - k * prices[i]] + k * weight[i]);
            }
        }
    }
    return dp[n];
}
```